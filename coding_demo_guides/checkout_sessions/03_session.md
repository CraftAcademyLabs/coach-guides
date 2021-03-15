```
As a user
In order to start ordering food
I would like an order to be created when I add my first product
```
### User can create an order by adding the first product

- So now we are going to follow up this functionality in the client. We have written the implementation for the API so we know that we are going to make a POST request with a product in the params and some authentication headers. Let's do it!

```javascript
describe('Create and order by', () => {
  beforeEach(() => {
    cy.server()
    cy.route({
      method: "GET",
      url: "http://localhost:3000/api/products", // we always need to stub out the index request
      response: "fixture:product_data.json",
    });
     cy.route({
       method: "POST",
       url: "http://localhost:3000/api/auth", // we need to log in to be able to see the button to add anything to an order
       response: "fixture:register_user.json",
       headers: {
         uid: "user@mail.com",
       },
     });
     cy.route({
       method: "POST",
       url: "http://localhost:3000/api/orders", // and of course, the request to create the order. 
       response: 'fixture:first_product_to_order.json'
     });
     cy.visit('/')
     cy.get('[data-cy="register-button"]').click(); // in the before each block we make sure to register and click to order something and then we can test that we both get a success message but also that we give the user an indication of how many products that are in the order
     cy.get('[data-cy="email-field"]').type("user@mail.com");
     cy.get('[data-cy="password-field"]').type("password");
     cy.get('[data-cy="password-confirmation-field"]').type("password");
     cy.get('[data-cy="submit"]').click();
     cy.get('[data-cy="product-1"]').within(() => {
       cy.get('[data-cy="order-button"]').click();
     });
  });


  it('successfully adding a product', () => { 
    cy.get('[data-cy="success-message"]').should(
      "contain",
      "This pizza was added to your order!"
    );
  })

  it('displays the amount of products in the order', () => {
    cy.get('[data-cy="order"]').should('contain', 'You have 1 pizza in your order')
  });
})
```
- So we should start with adding an onclick event to our orders button.

```javascript
  <Button
    data-id={item.id} // declare the addToOrder function and set a debugger, then explain that we need to get hold of the product id to send as params (connect back to what we did in the API)
    data-cy="order-button"
    onClick={(event) => this.addToOrder(event)}
  >
    Add to order
  </Button>
```
- When we have reached the `addToOrder` function and got hold of the product id then we can start focusing on the API call

```javascript
addToOrder = async (event) => {
    let productId = parseInt(event.target.dataset.id); // we need to send the id as an integer and not a string
    let response = await createOrder(productId) // we will extract this to a separate module for practice
  };
```
- now, go ahead and create that separate module
```javascript
import axios from "axios";

const createOrder = async (productId) => {
  let authenticationHeaders = JSON.parse(localStorage.getItem("credentials")); // explain how we get the information to put in the headers, refer back to when we set the item
  let response = await axios.post(
    "/orders",
    { product_id: productId },
    { headers: authenticationHeaders }
  );
  return response.data
};;

export { createOrder };

```
- Once we have the `response.data` then we can return to the component and make use of it. We will start with displaying the message and then move over to display how many products that are in the order

```javascript
addToOrder = async (event) => {
  let productId = parseInt(event.target.dataset.id);
  let response = await createOrder(productId)
  this.setState({ message: response.message });
};
//....

return (
  <Container data-cy="menu">
    {message && <p data-cy="success-message">{message}</p>}
    {dataIndex}
  </Container>
);
```
- Now our first test should go green and we can now focus on the last thing, displaying how many products that are in the order.

```javascript
addToOrder = async (event) => {
  let productId = parseInt(event.target.dataset.id);
  let response = await createOrder(productId)
  this.setState({ message: response.message });
  let orderItemsLength = response.order.items.length;
  this.setState({ orderItems: orderItemsLength });
};

return (
  <Container data-cy="menu">
    {orderItems && (
      <Container data-cy="order">
        You have {orderItems} pizza in your order
      </Container>
    )}
    {message && <p data-cy="success-message">{message}</p>}
    {dataIndex}
  </Container>
);
```
- Now, the tests are going green, awesome!
- Let's connect the dots before we break to make sure that our implementation is working as it should! Embrace the importance of dry runs once in a while
