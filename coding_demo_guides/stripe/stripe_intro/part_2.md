Api

Start with creating a test

```ruby
RSpec.describe 'GET /api/subscriptions', type: :request do
  describe 'successfully' do
    let!(:registered_user) { create(:user) }
    let!(:user_headers) { registered_user.create_new_auth_token }
    before do
      post '/api/subscriptions',
           params: {
             stripeToken: '123456789'
           },
           headers: user_headers
    end

    it 'is expected to return 200 status' do
      expect(response).to have_http_status 200
    end

    it 'is expected to return a success message' do
      expect(JSON.parse(response.body)['message']).to eq 'Payment successfull'
    end

    it 'is expected to turn user into subscriber' do
      expect(registered_user.subscriber).to eq true
    end
  end
end

```

Add route, generate the controller (remember API namespace)
add a before action to authenticate the user

```ruby
def create
  payment_status = perform_payment

  if payment_status
    current_user.update_attribute(:subscriber, true)
    render json: { message: "Payment successfull" }
  else
    render json: { message: "Something went wrong" }, status: 422
  end
end

private 

def perform_payment
  customer = Stripe::Customer.create(
    email: current_user.email,
    source: params[:stripeToken],
    description: "For subscription"
  )
  charge = Stripe::Charge.create(
    customer: customer.id,
    amount: 100,
    currency: 'sek'
  )

  charge.paid
end
```
Add the stripe gem, `stripe-rails`
bundle
Runt the tests again

We need to encrypt these keys. 

`EDITOR="code --wait" rails credentials:edit`

```yaml
stripe
  publishable_key: bla bla
  secret_key: 
```

go to application.rb 

```ruby
config.stripe.publishable_key = Rails.application.credentials.stripe[:publishable_key]
config.stripe.secret_key = Rails.application.credentials.stripe[:secret_key]

```

should complain about token

add Stripe Mock. 
gem 'stripe-ruby-mock', require 'stripe_mock'

go to rails helper

```ruby
require 'stripe_mock'
config.before(:each) do
  StripeMock.start
end
config.after(:each) do
  StripeMock.stop
end
```

instead of the jibbberish token we do 
StripeMock.create_test_helper.generate_card_token

put a binding pry and look at the customer

Change the last test to reload the user in the test
