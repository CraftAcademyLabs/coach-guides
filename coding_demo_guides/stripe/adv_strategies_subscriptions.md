- Have a code base with devise token auth before starting
- Show the flow chart from the slide deck that is for the intro
- Explain that the client will behave exactly like before, except that we have to update the users role to subscriber in redux state
- Instead of submitting a payment we will initiate a subscription, that will charge the user regularly 

- and as always we start with a test

```ruby
RSpec.describe "POST /api/subscriptions", type: :request do


  let(:user) { create(:user) }
  let(:user_headers) { user.create_new_auth_token }

  describe "successfully with valid params" do
    before do
      post "/api/subscriptions",
           params: {
             stripeToken: 'sdfhkkjh38493djs',
           },
           headers: user_headers
    end

    it "is expected to return 201 response status" do
      expect(response.status).to eq 201
    end

    it "is expected to return success message" do
      expect(response_json["message"]).to eq "Subscription successfully created!"
    end

    it "is expected to make user a subscriber" do
      expect(user.subscriber?).to eq true
    end
  end
```

- Now let's add the stripe-ruby-mock gem as we did last time

```ruby
gem 'stripe-ruby-mock'
```

- on the top of the test add the following to make use of the test gem: 

- in the rails_helper require the gem as `stripe_mock`

```ruby
  let(:stripe_helper) { StripeMock.create_test_helper }
  let(:valid_stripe_token) { stripe_helper.generate_card_token }

  before(:each) { StripeMock.start }
  after(:each) { StripeMock.stop }

  #...

  post "/api/v1/subscriptions",
            params: {
              stripeToken: valid_stripe_token,
            },
```

- bundle and run the test and go through the usual steps
- Add the route, add the controller and the create action 
- Run the tests again and see that you are stopping at the binding.pry in the create action and look at the params, to show the mocked token

```ruby
before_action :authenticate_user!

  def create
    begin
      customer_id = get_customer(params[:stripeToken])
      subscription = Stripe::Subscription.create({ customer: customer_id, plan: "demo_subscription" })

      test_env?(customer_id, subscription)
      status = Stripe::Invoice.retrieve(subscription.latest_invoice).paid

      if status === true
        current_user.update_attribute(:role, "subscriber")
        render json: { message: "Subscription successfully created!" }, status: 201
      else
        render_stripe_error('Whoops this did not go right')
      end
    rescue => error
      binding.pry
    end
  end

  private

  def get_customer(stripe_token)
    customer = Stripe::Customer.list(email: current_user.email).data.first
    customer ||= Stripe::Customer.create({ email: current_user.email, source: stripe_token })
    customer.id
  end

  def render_stripe_error(error)
    render json: { message: "Transaction was not successfull. #{error}" }, status: 422
  end
```
- now we get an error because we don't have that plan
- let's do some configuration
- add gem `stripe-rails` and bundle
- now it will complain about not having the keys 
- `EDITOR='code --wait' rails credentials:edit`
- add the stripekeys: 
 
 ```yaml
stripe
  pk_key: bla bla
  secret_key: bla bla
 ```
- configure stripe in the application.rb

```ruby
config.stripe.publishable_key = Rails.application.credentials.stripe[:pk_key]
    config.stripe.secret_key = Rails.application.credentials.stripe[:secret_key]
```

- run `rails g stripe:install`
- it creates a folder and in there we can set up a plan

```ruby
Stripe.plan :demo_subscription do |plan|
  plan.name = 'Demo Subscription'

  plan.amount = 250

  plan.currency = 'sek'

  plan.interval = 'month'

  plan.interval_count = 1

  plan.trial_period_days = 0
end
```
- run `rails stripe:prepare`
- go to stripe and show the new subscription
- run the test and we get the same subscription

```ruby
  let(:product) { stripe_helper.create_product }
  let!(:plan) do
    stripe_helper.create_plan(
      id: "demo_subscription",
      amount: 50,
      currency: "usd",
      interval: "month",
      interval_count: 1,
      name: "Demo Subscription",
      product: product.id
    )
  end

```
- you shouldn't change implementation code depending on test, but sometime we have to

```ruby 
#above status is defined in the controller
test_env?(customer_id, subscription)
 #...
 private 

  def test_env?(customer, subscription)
    if Rails.env.test?
      invoice = Stripe::Invoice.create({ customer: customer, subscription: subscription.id, paid: true })
      subscription.latest_invoice = invoice.id
    end
  end
```
- run the tests again and now subscriber is not a valid role,
- add it to the user roles
- now we have to reload the user in the test, like we have done before

- but now we still have the sad path left if you guys have energy. 
- I can show you credit card is declined

```ruby
describe "unsuccessfully" do
    describe "credit card being declined" do
      before do
        StripeMock.prepare_card_error(:card_declined, :new_invoice)

        post "/api/v1/subscriptions",
            params: {
              stripeToken: valid_stripe_token,
            },
            headers: user_headers
      end

      it "is expected to return 422 response status" do
        expect(response.status).to eq 422
      end

      it "is expected to return unsuccessfull message" do
        expect(response_json["message"]).to eq "Transaction was not successfull. The card was declined"
      end

      it "is expected to become subscriber" do
        expect(user.reload.subscriber?).to eq false
      end
    end
  end

```
```ruby
  rescue => error
    render_stripe_error(error.message)
  end
```