```
As a restaurant API
In order for the user to complete their order
I would like to be able to update their existing order to be finalized
```
### API provides functionality to finalize order

- This is an extra session if there is time on Friday. We will only show this in the API and then it is up to the students to follow the same flow as we have been during these sessions to get the functionality in the client. 

- Start with the test:

```ruby
RSpec.describe 'PUT /api/orders/:id', type: :request do
  let(:user) { create(:user) }
  let(:authentication_headers) { user.create_new_auth_token }
  let(:order) { create(:order, user: user) }
  let(:ordered_product) { create(:product) }

  describe 'successfully with valid params' do
    before do
      order.items.create(product: ordered_product)
      put "/api/orders/#{order.id}",
          params: { confirmed: true },
          headers: authentication_headers
    end

    it 'is expected to return 200 status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to return success message' do
      expect(response_json['message']).to eq 'Your order is confirmed and will be ready to pick up in 15 min to a quarter'
    end

    it 'is expected to update the confirmed status of order' do
      expect(order.reload.confirmed?).to eq true # explain the .reload, maybe even not have it from the beginning and then show them that we have to reload the resource to be able to see any updates 
    end
  end
end
```
- Now we have the route and the action already, so what we need to do is set a conditional to see what needs to be updated. 

```ruby
def update
  order = Order.find(params['id'])
  if params['confirmed']
    order.update(confirmed: true)
    render json: { message:
        'Your order is confirmed and will be ready to pick up in 15 min to a quarter' }
  else
    product = Product.find(params['product_id'])
    new_order_item = @order.items.create(product: product)
    order_response(new_order_item, @order, 200)
  end
end

```
- Now we get an error that confirmed doesn't exist, and of course it doesn't. So we need to migrate! 

```ruby
class AddConfirmedToOrder < ActiveRecord::Migration[6.0]
  def change
    add_column :orders, :confirmed, :bool, default: false
  end
end
```
- And now we should pretty much go green! 

- There is one interesting sad path and that is that you shouldn't be able to add anymore items to your order if it has been confirmed, right? 

- So let's go back to the test we wrote for adding a second product to an order and write a sad path for if an order has already been confirmed: 

```ruby
 describe 'unsuccessfully if order is confirmed' do
  let(:order) { create(:order, user: registered_user, confirmed: true) }
  before do
    order.items.create(product: ordered_pizza)
    put "/api/orders/#{order.id}",
        params: { product_id: pizza_to_order.id },
        headers: auth_headers
  end

  it 'is expected to return 403' do
    expect(response).to have_http_status 403
  end

  it 'is expected to return error message' do
    expect(response_json['message']).to eq 'This order has already been confirmed, to order more food, create a new order'
  end
end
```
- now, let's show them how to create our own custom made `before action`:

```ruby
before_action :order_confirmed?, only: [:update]

# ...

private 

def order_confirmed?
  @order = Order.find(params['id']) # by setting the order as an instance variable then we can use it as @order in create method and doesn't have to find that instance in the db over and over
  return unless @order.confirmed?

  render json: { message:
    'This order has already been confirmed, to order more food, create a new order' },
          status: 403
end

```

- and now we can also confirm an order! The circle is closed. 
