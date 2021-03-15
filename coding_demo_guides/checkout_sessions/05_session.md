```
As a user
In order to order the food that I want
I would like to be able update my order with more products
```

### User can add several products to their order

- Now we will update the order with more products from the client side and as always we start with the test:

```javascript
describe('Update an order by', () => {
  describe('successfully adding a second product', () => {
    beforeEach(() => {
      cy.server()
      cy.route({
        method: "GET",
        url: "http://localhost:3000/api/products", // the usual stubs
        response: "fixture:product_data.json",
      });
      cy.route({
        method: "POST",
        url: "http://localhost:3000/api/auth", // the usual stubs
        response: "fixture:register_user.json",
        headers: {
          uid: "user@mail.com",
        },
      });
      cy.route({
        method: "POST",
        url: "http://localhost:3000/api/orders",// the usual stubs
        response: "fixture:first_product_to_order.json",
      });
      cy.route({
        method: "PUT",
        url: "http://localhost:3000/api/orders/**", // the request that we will work with this time around
        response: 'fixture:second_product_to_order.json'
      });
      cy.visit("/");
      cy.get('[data-cy="register-button"]').click();
      cy.get('[data-cy="email-field"]').type("user@mail.com");
      cy.get('[data-cy="password-field"]').type("password");
      cy.get('[data-cy="password-confirmation-field"]').type("password");
      cy.get('[data-cy="submit"]').click();
      cy.get('[data-cy="product-1"]').within(() => {
        cy.get('[data-cy="order-button"]').click();
      });
      cy.get('[data-cy="product-3"]').within(() => {
        cy.get('[data-cy="order-button"]').click();
      });
    });

    it('is expected to render a success message', () => {
      cy.get('[data-cy="success-message"]').should(
        "contain",
        "This pizza was added to your order!"
      );
    });

    it('is expected to update amount of pizzas in order', () => {
      cy.get('[data-cy="order"]').should('contain', 'You have 2 pizza in your order')
    }); 
  })
})
```
- Aand as usual we need to add a fixture: 
```json
{
  "message": "This pizza was added to your order!",
  "order": {
    "id": 1,
    "items": [
      {
        "id": 1,
        "name": "Vesuvio",
        "ingredients": "Cheese, Ham",
        "price": 12
      },
      {
        "id": 3,
        "name": "Funghi",
        "ingredients": "Cheese, Mushroom",
        "price": 7
      }
    ]
  }
}
```
- So we will add the same button as before, and therefor we need to have a conditional what to do in the function depending on if it is the first product or another product. 

```javascript
addToOrder = async (event) => {
    let response;
    let productId = parseInt(event.target.dataset.id);
    if (this.state.orderId) {
      response = await updateOrder(this.state.orderId, productId); // to the update module we also need to send the order id, since that is needed as route params to update a resource 
    } else {
      response = await createOrder(productId);
    }
    let orderItemsLength = response.order.items.length;
    this.setState({
      message: response.message,
      orderItems: orderItemsLength,
      orderId: response.order.id, // explain that we have to set the order id in state on the first create request, and by checking if we have an order id or not we can decide if we should make a PUT request or a POST
    });
  };
```
- And then we simply create that `updateOrder` function in our module:
```javascript 
const updateOrder = async (orderId, productId) => { 
  let response = await axios.put(
    `/orders/${orderId}`,
    { product_id: productId },
    { headers: authenticationHeaders }
  );
  return response.data;
};

export { createOrder, updateOrder };
```
- With this, we are actually done! We have a very dynamic code that gives the user the same experience in the UI no matter what is happening under neath the hood and that is just how we want to do it!