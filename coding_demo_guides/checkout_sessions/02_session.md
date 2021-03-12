```
As a restaurant API
In order for users to buy food they want from the restaurant
I would like to be able to create an order for a specific user
```
### API provides functionality for user to create order

- Use this [REPO](https://github.com/CraftAcademy/slowfood_checkout_api) and create a branch that you call month_year of the bootcamp. From that branch you will later branch off and create PR's to after each demo. Make sure to share links to the PR's after each session. Note that the client and the API is dealing with pizza...

- As always, we start with the test! 

```ruby
RSpec.describe 'POST /api/orders', type: :request do
  describe 'Successfully with valid product id' do
    let!(:product_to_order) { create(:product) }
    let!(:user) { create(:user) }
    let!(:authorisation_headers) { user.create_new_auth_token } # explain this to the students, what is going on

    before do
      post '/api/orders',
           params: {
             product_id: product_to_order.id
           },
           headers: authorisation_headers # and here, how we are sending the information that we stored in the localstorage in the previous session
    end

    it 'is expected to return 201 status' do
      expect(response).to have_http_status 201
    end

    it 'is expected to return success message' do
      expect(response_json['message']).to eq 'This pizza was added to your order!'
    end

    it 'is expected to return an array of the items' do
      expect(response_json['order']['items'].count).to eq 1 # talk the students through how we will structure the response
    end

    it 'is expected to return the products of the order' do
      expect(response_json['order']['items'].first['name']).to eq 'Vesuvio'
    end
  end
end
```
- First two errors will of course be regarding the route not existing and that the controller doesn't exist. Create those, one at the time to show the students the real TDD way. 
- Now we are ready to get cracking with the create action: 

```ruby
class Api::OrdersController < ApplicationController
  before_action :authenticate_user! #we know that the user will have to be authenticated since the button will not be displayed if that is not the case and our user story claims that a user and not a visitor can create an order

  def create
    product = Product.find(params['product_id'])
    order = current_user.orders.create
  end
end
```
- This till throw us an error, that `orders` is not defined, and it certainly isn't. 
- it is time for us to create the order model and also think about the data flow that we want. Explain the following to the students and try to use real life examples:
  - An order will belong to a user 
  - An order will be able to have one or many items in it
  - an order item will belong to a product, it will be like a copy of a product
  - an order item will also belong to an order, since there is no reason for an item to be created without an order to put it in

- So time to migrate and make this happen: 

```
$ rails g model order references:user 
```
```ruby
class CreateOrders < ActiveRecord::Migration[6.0]
  def change
    create_table :orders do |t|
      t.references :user, null: false, foreign_key: true

      t.timestamps
    end
  end
end
```
- migrate the database and then add the order items model as well:

```
$ rails g model item references:order references:product 
```
```ruby
class CreateItems < ActiveRecord::Migration[6.0]
  def change
    create_table :items do |t|
      t.references :order, null: false, foreign_key: true
      t.references :product, null: false, foreign_key: true

      t.timestamps
    end
  end
end
```
- Now we ned to update our models with all these references: 

```ruby
class Order < ApplicationRecord
  belongs_to :user
  has_many :items
  has_many :products, through: :items # explain this and play around in pry to show how it changes things
end
```
```ruby
class Item < ApplicationRecord
  belongs_to :order
  belongs_to :product
end
```
```ruby
class User < ActiveRecord::Base
  extend Devise::Models
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
  include DeviseTokenAuth::Concerns::User
  has_many :orders
end
```
```ruby
class Product < ApplicationRecord
  validates_presence_of :name, :ingredients, :price
  validates :price, presence: true, numericality: { only_integer: true }
  has_many :items
end
```
- now migrate that and we can get the show on the road again! 
- So now back to the controller

```ruby
 def create
    product = Product.find(params['product_id'])
    order = current_user.orders.create
    order.items.create(product: product)
   if order.persisted?
      render json: {
        message: 'This pizza was added to your order!',
        order: { id: order.id,
                 items: order.products }
      }, status: 201
    else
      render json: { message: 'Whoops, something went wrong!' }, status: 422
    end
  end

```
- All tests are green! we are good to continue with the client. A lot of new information with the associations but not that hard after all! 
