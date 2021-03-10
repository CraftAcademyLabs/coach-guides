```
As a user,
In order to be able to add product to an order
I would like to be able to register an account
```
### Visitor can register to see 'Add to order' button

- Use this [REPO](https://github.com/CraftAcademy/slowfood_checkout_client) and create a branch that you call month_year of the bootcamp. From that branch you will later branch off and create PR's to after each demo. Make sure to share links to the PR's after each session.  

- When starting with this feature make sure to have an API with an index action of products and devise token auth set up.
- In the client you need to have a corresponding feature of an index of products to start with for this session. 

- Explain to the students that you have already set up the corresponding feature to this one in the API (since that is devise token auth that they set up themselves during the weekend)

- Start with writing a test:

```javascript
describe("Add to order button", () => {
  beforeEach(() => {
    cy.server();
    cy.route({
      method: "GET",
      url: "http://localhost:3000/api/products",
      response: "fixture:product_data.json",
    });
    cy.visit("/");
  });
  describe("is visible", () => {
    it("for successfully authenticated user", () => {
      cy.get('[data-cy="register-button"]').click();
      cy.get('[data-cy="email-field"]').type("user@mail.com");
    })
  })
})
```
- we will start like this, just to first have button being clicked and once it is then we will fill in ONE field. 

- Import and render a `Registration` in the `App.jsx`

```javascript
// App.jsx

// ... 
 <>
      <Header as="h1" textAlign="center">
        Slowfood
      </Header>
      <Container>
        <Registration>
        <DisplayMenu />
      </Container>
    </>
```
```javascript
// Registration.jsx

import React, { Component } from "react";

class Registration extends Component {

  render() {
    return (
      <div>
        <button
          data-cy="register-button"
        >
          Sign up!
        </button>
      </div>
    );
  }
}

export default Registration;

```
- Once the test is clicking the button, then we add the first field and some state to show the field when the button is clicked. 

```javascript
import React, { Component } from "react";
import { registerUser } from "../modules/authenticationService";

class Registration extends Component {
  state = {
    renderForm: false,
  };

  render() {
    const { renderForm} = this.state;
    return (
      <div>
        {renderForm ? (
            <form>
              <input
                name="email"
                type="email"
                data-cy="email-field"
                placeholder="Email"
              />
            </form>  
        ) : (
          <button
            data-cy="register-button"
            onClick={() => this.setState({ renderForm: true })}
          >
            Sign up!
          </button>
        )}
      </div>
    );
  }
}

export default Registration;

```

