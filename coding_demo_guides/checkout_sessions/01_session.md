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
    });
  });
});
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
        <button data-cy="register-button">Sign up!</button>
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
    const { renderForm } = this.state;
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

- now we are ready to add the password and password confirmation fields as well and also a button to submit the credentials.

- the first thing is to update the test and then the implementation

```javascript
// ...
cy.get('[data-cy="password-field"]').type("password");
cy.get('[data-cy="password-confirmation-field"]').type("password");
cy.get('[data-cy="submit"]').click();
```

```javascript
//Registration.jsx

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
              <input
                name="password"
                type="password"
                data-cy="password-field"
                placeholder="Password"
              />
              <input
                name="password_confirmation"
                type="password"
                data-cy="password-confirmation-field"
                placeholder="Password Confirmation"
              />
              <button type="submit" data-cy="submit">
                Register!
              </button>
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
```

- now we have reached the point where the interesting things will start happening, now we are clicking on the button to sign in and with that click we have to trigger a call to our api
- There are two things that I want to happen, I want to display a message that indicates to the user that he/she is now authenticated. But I also want to display the add to order button, like our user story states.

```javascript
cy.get('[data-cy="success-message"]').should(
  "contain",
  "Welcome to Slowfood user@mail.com"
);
cy.get('[data-cy="product-1"]').within(() => {
  cy.get('[data-cy="order-button"]').should("be.visible");
});
```

```javascript
  <form
    onSubmit={(event) => {
      this.signUpUser(event);
    }}
  >
```

- now define that function with `event` as an argument. Explain why we have to set `event.preventDefault()` the first thing we do in a function that deal with submitting a form.
- Set a debugger in the function to show in the console how we can get a hold of the values of the input fields.
- You should end up here:

```javascript
signUpUser = async (event) => {
  event.preventDefault();
  let credentials = {
    email: event.target.email.value,
    password: event.target.password.value,
    password_confirmation: event.target.password_confirmation.value,
  };
};
```

- now we need to use axios to send the request to our api with our credentials as params

```javascript
signUpUser = async (event) => {
  //...
  try {
    let response = await axios.post("/auth", credentials);
    debugger;
  } catch (error) {
    console.log(error);
  }
};
```

- now we have reached a problem, we are making a call to our api that is set to localhost:3000 which is not running, In order words we need to set in a new stub in our test.
- Explain that we don' need to set all the content that we get in the headers, but we will get information in the response headers that we need to save in our localstorage to be able to authenticate with requests

```javascript
describe("is visible", () => {
 beforeEach(() => {
    cy.route({
      method: "POST",
      url: "http://localhost:3000/api/auth",
      response: "fixture:register_user.json",
      headers: {
        uid: "user@mail.com",
      },
    });
  });
//...
```

- and add the fixture:

```json
{
  "status": "success",
  "data": {
    "id": 1,
    "email": "user@mail.com",
    "provider": "email",
    "uid": "user@mail.com",
    "allow_password_change": false
  }
}
```

```javascript
let response = await axios.post("/auth", credentials);
const userCredentials = {
  uid: response.headers["uid"],
  client: response.headers["client"],
  access_token: response.headers["access-token"],
  expiry: response.headers["expiry"],
  token_type: "Bearer",
};
localStorage.setItem("credentials", JSON.stringify(userCredentials));
```

- put a debugger before the try block and check what is in local storage and then check again with a debugger after we have set the credentials item

- now we need to set the message that tells the user and then also make sure that we can set a state that the user is authenticated that we can use in the menu component so decide if we will show the order button or not. We will start with the easy part:

```javascript
signUpUser = async (event) => {
  event.preventDefault();
  let credentials = {
    email: event.target.email.value,
    password: event.target.password.value,
    password_confirmation: event.target.password_confirmation.value,
  };
  try {
    let response = await axios.post("/auth", credentials);
    const userCredentials = {
      uid: response.headers["uid"],
      client: response.headers["client"],
      access_token: response.headers["access-token"],
      expiry: response.headers["expiry"],
      token_type: "Bearer",
    };
    localStorage.setItem("credentials", JSON.stringify(userCredentials));
    this.setState({
      message: `Welcome to Slowfood ${response.data.data.email}`,
      renderForm: false,
    });
  } catch (error) {
    console.log(error);
  }
};
```

- now change the conditional in the return:

```javascript
 //...
  ) : message ? (
    <div data-cy="success-message">{message}</div>
  ) : (
    <button
      data-cy="register-button"
      onClick={() => this.setState({ renderForm: true })}
    >
      Sign up!
    </button>
  )}
```

- now let's back up a little bit and head to our `App.jsx` where we will deal with the authentication state

```javascript
class App extends Component {
  state = {
    authenticated: false,
  };

  setAuthState = () => {
    this.setState({ authenticated: true });
  };
  render() {
    return (
      <>
        <Header as="h1" textAlign="center">
          Slowfood
        </Header>
        <Container>
          <Registration authenticatedStatus={() => this.setAuthState()} />
          <DisplayMenu />
        </Container>
      </>
    );
  }
}
```

- and then we need to call in that function when e register

```javascript
 signUpUser = async (event) => {
//...
this.props.authenticatedStatus()
 } catch (error) {
   //....
}
```

- now we can make use of this state by passing it as props to the `DisplayMenu` component.

```javascript
//App.jsx
return (
  <>
    <Header as="h1" textAlign="center">
      Slowfood
    </Header>
    <Container>
      <Registration authenticatedStatus={() => this.setAuthState()} />
      <DisplayMenu authenticated={this.state.authenticated} />
    </Container>
  </>
);
```
```javascript
//DisplayMenu
// add this in the map, so that every product get a button
{this.props.authenticated && (
  <Button data-cy="order-button">Add to order</Button>
)}
```

- And with that we are done! The feature is that the button should be visible when the user is authenticated, so at this stage we should not do more than this!
- Finish the session with firing up the API and connect the dots between the client and the api


