```
As an restaurant API
In order for users to add more than one product to their order
I would like to be able to update an existing order with new order items
```
### API provides functionality to add several products to an order

- Alright time to add som more products to the order, this restaurant can't ony be for singles. 
- It's important to understand why we now have to make a PUT request and not a POST request

- We will start with the test as always: 
```ruby
RSpec.describe 'PUT /api/orders/:id', type: :request do
  let(:registered_user) { create(:user) }
  let(:auth_headers) { registered_user.create_new_auth_token }
  let(:order) { create(:order, user: registered_user) } # to update the order, we need to have an order from start to update
  let(:ordered_pizza) { create(:product) } # make it clear to the students that we will create two products, one that is already ordered and one that we will order now
  let(:pizza_to_order) { create(:product, name: 'Funghi') } # and here we have the pizza that we want to order now! 

  describe 'successfully with valid params' do
    before do
      order.items.create(product: ordered_pizza) # create an order item in the order that is created so that it has 'one' product already
      put "/api/orders/#{order.id}",
          params: { product_id: pizza_to_order.id },
          headers: auth_headers
    end

    it 'is expected to return a 200 status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to have to have a product called Funghi' do
      expect(response_json['order']['items'].second['name']).to eq 'Funghi'
    end

    it 'is expected to have two products in the order' do
      expect(response_json['order']['items'].count).to eq 2 # we can see that the response will be very similar, in fact the exact same as when we added the first item, because we want to display the same information to the user no matter if it is the first or twentyfirst product
    end
  end
end
```
- and now of course we add the route and the `update` action to our controller

```ruby
 def update
    order = Order.find(params['id'])
    product = Product.find(params['product_id'])
    new_order_item = order.items.create(product: product)
    if new_order_item.persisted?
      render json: {
        message: 'This pizza was added to your order!',
        order: { id: order.id,
                 items: order.products }
      }, status: status
    else
      render json: { message: 'Whoops, something went wrong!' }, status: 422
    end
  end
```
- but now it is time for us to think about refactoring this. We have in principal the exact same response in both the `update` and `create` action, that is not very DRY

```ruby
# this is one example of refactoring where we are making the order response dynamic by sending in the arguments. Explain the solution and always comment out code when dealing with refactoring so that the students can get a good flow but also see the difference of the two implementations after. 
def create
  product = Product.find(params['product_id'])
  order = current_user.orders.create
  order.items.create(product: product)
  order_response(order, order, 201)
end

def update
  order = Order.find(params['id'])
  product = Product.find(params['product_id'])
  new_order_item = order.items.create(product: product)
  order_response(new_order_item, order, 200)
end

private

def order_response(resource, order, status) 
  if resource.persisted?
    render json: {
      message: 'This pizza was added to your order!',
      order: { id: order.id,
                items: order.products }
    }, status: status
  else
    render json: { message: 'Whoops, something went wrong!' }, status: 422
  end
end
```

- Et voilá! Tests are green, we have updated the order with yet another product in a very smooth way and also dealt with a bit of refactoring 
