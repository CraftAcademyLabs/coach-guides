starting with the client, once you are logged in there should be a button that you can become a subscriber
It will not really be a real subscription, we will pay once and be a subscriber for ever.

we will use the code base from the slowfood

we will start by creating a test!

```javascript
describe('User can become subscriber', () => {
  describe('successfully', () => {
    beforeEach(() => {
      cy.server();
      cy.route({
        method: "GET",
        url: "http://localhost:3000/api/products",
        response: "fixture:product_data_.json",
      });

      cy.route({
        method: "POST",
        url: "http://localhost:3000/api/auth",
        response: "fixture:successfull_sign_up.json",
        headers: {
          uid: "user@mail.com",
        },
      });

      cy.visit("/");

      cy.get('[data-cy="register-cta"]').click();
      cy.get('[data-cy="email"]').type('thomas@craft.com')
      cy.get('[data-cy="password"]').type('password')
      cy.get('[data-cy="password-confirmation"]').type('password')
      cy.get('[data-cy="register"]').click()
      });
    })

    it('by filling in valid credit card information', () => {
      cy.get("[data-cy=become-subscriber]").click()

      cy.get("[data-cy=payment-form]").should("exist")

  })
})
```

Obviously it can't find the button
in the App component:

```javascript
{ this.state.authenticated ? (
          <Elements>
            <BecomeSubscriber />
          </Elements>
        ) : (
          <Login
            <Login toggleAuthenticatedState={() => this.toggleAuthenticatedState()} />
          />
        )}
```

create that component

```javascript
import React, { Component } from 'react'

class BecomeSubscriber extends Component {
  state = {
    renderForm: false,
  }

  render() {

    return (

            <>
              { this.state.renderForm ? (
                <form data-cy="payment-form" onSubmit={this.payWithStripe}>
                  <div> GIVE ME YOUR CREDIT CARD INFO! </div>
                </form>
              ) : (
                  <button data-cy="become-subscriber" onClick={() => this.setState({ renderForm: true })}>
                    Become subscriber
                  </button>
                )
              }
            </>
          )

  }
}

export default BecomeSubscriber
```

- yarn add react-stripe-elements

Add this script to the index.html <script src="https://js.stripe.com/v3/"></script>

In the cypress.json: chromeWebSecurity: false
It doesn't work without setting this setting

```javascript
// index.js

import { StripeProvider } from 'react-stripe-elements'

ReactDOM.render(
  <StripeProvider apiKey="">
    <App />
  </StripeProvider>,
  document.getElementById('root')
);

```
Show Stripes dashboard to get the right key

Add the elements around the BecomeSubscriber in the App.jsx

We need to inject stripe into out BecomeSubscriber component. 

```javascript
import React, { Component } from 'react'
import {
  injectStripe,
  CardNumberElement
} from "react-stripe-elements";

class BecomeSubscriber extends Component {
  state = {
    renderForm: false
  }

  render() {

    return (
            <>
              { this.state.renderForm ? (
                <form data-cy="payment-form" onSubmit={this.payWithStripe}>
                  <div id="card-number">
                    <label>Card Number</label>
                    <CardNumberElement />
                  </div>
                </form>
              ) : (
                  <button data-cy="become-subscriber" onClick={() => this.setState({ renderForm: true })}>
                    Become subscriber
                  </button>
                )
              }
            </>

    )
  }
}

export default injectStripe(BecomeSubscriber)
```
```javascript
cy.wait(1000)

cy.get("#card-number").within(() => {
  cy.get('iframe[name^="__privateStripeFrame"]').then($iframe => {
    const $body = $iframe.contents().find("body");
    cy.wrap($body)
      .find('input[name="cardnumber"]')
      .type("4242424242424242", { delay: 50 });
  });
})
    
```
make sure it goes green

```javascript
  cy.get("#card-expiry").within(() => {
        cy.get('iframe[name^="__privateStripeFrame"]').then(($iframe) => {
          const $body = $iframe.contents().find("body");
          cy.wrap($body).find('input[name="exp-date"]').type("1222", { delay: 10 });
        });
      })

      cy.get("#card-cvc").within(() => {
        cy.get('iframe[name^="__privateStripeFrame"]').then(($iframe) => {
          const $body = $iframe.contents().find("body");
          cy.wrap($body).find('input[name="cvc"]').type("999", { delay: 10 });
        });
      })

```
add the card expiry and the card cvc to the component

add the button and the message to the test

```javascript
      cy.get("button").contains("Submit payment").click()

      cy.get("[data-cy=payment-message]").contains("Payment successfull")
```
We will also create a fixture and add the stubb 
```

```javascript

      cy.route({
        method: "POST",
        url: "http://localhost:3000/api/subscriptions",
        response: "fixture:stripe_response.json"
      });
```
```json
stripe_response.json

{
  "paid": true,
  "message": "Payment successfull"
}
```
```javascript
<form data-cy="payment-form" onSubmit={this.payWithStripe}>
                  <div id="card-number">
                    <label>Card Number</label>
                    <CardNumberElement />
                  </div>
                  <button>Submit payment</button>
                </form>

```

create the function, prevent default and put a debugger

```javascript
  payWithStripe = async (event) => {
    event.preventDefault()

    let stripeReponse = await this.props.stripe.createToken()
    // put debugger
    stripeReponse.token && (
      this.performPayment(stripeReponse.token.id)
    )
  }
```

create the performPayment function and put a debugger

```javascript
  performPayment = async (stripeToken) => {
    let headers = localStorage.getItem("userData")
    headers = JSON.parse(headers)
    headers = {
      ...headers,
      "Content-type": "application/json",
      Accept: "application/json"
    }

    let response = await axios.post("/subscriptions", {
      stripeToken: stripeToken
    }, {
      headers: headers
    })

    if (response.data.paid) {
      this.setState({ message: response.data.message })
    }
  }
```

```javascript
{ this.state.message ? (
          <p data-cy="payment-message" >{this.state.message}</p>
        ) : (
            <>
              { this.state.renderForm ? (
                <form data-cy="payment-form" onSubmit={this.payWithStripe}>
                  <div id="card-number">
                    <label>Card Number</label>
                    <CardNumberElement />
                  </div>

                  <div id="card-expiry">

                    <label>Card Expiry</label>
                    <CardExpiryElement />
                  </div>

                  <div id="card-cvc">
                    <label>Card CVC</label>
                    <CardCVCElement />
                  </div>

                  <button>Submit payment</button>
                </form>
              ) : (
                  <button data-cy="become-subscriber" onClick={() => this.setState({ renderForm: true })}>
                    Become subscriber
                  </button>
                )
              }
            </>
          )
        }
```
