## Node Notes
### Demo: Node first part after lunch

- Go to Books.spec.js and add:

  ```
  describe("constraints", () => {
    it("rejects null value for title", async () => {
      try {
        await factory.create("Book", { title: null });
        expect.fail();
      } catch (error) {
        expect(error.errors).to.containSubset([
          { message: "Book.title cannot be null" },
        ]);
      }
    });
  });
  ```
- Should get an error about the Subset if you run the test
  
  ```
  $ yarn add -D chai-subset
  ```
- go to tests/test_helper/indes.jx
  ```
  const chaiSubset = require('chai-subset')
  chai.use(chaiSubset)
  ```

- go to database/config/config.js
  ```
  "logging": false
  (unfortunately i do not know what it said before)
  ```
- run test again, make sure that the logs were silenced now and you should get an error

  ```
  $ yarn add -D factory-girl
  ```

- You should get a factories folder
- create an index.js inside of that folder and add this code: 
```
module.exports = (factory, Models) => {
  const normalizedPath = require('path').join(__dirname, '.')
  require('fs').readdirSync(normalizedPath).forEach(file => {
    if (file !== 'index.js') {
      require(`./${file}`)(factory, Models)
    }
  })
}
```
- create a new file factories/bookFacotory.js
```
$ touch factories/bookFactory.js
```
-  and add code into that file:
```
module.exports = (factory, Models) => {
  factory.define('Book', Models.Book, {
    title: 'FooBar'
  })
}
```
- Go to tests/test_helper/index.js and add code:
```
factory.setAdapter(adapter)
factory.cleanUp(); //???
factory.factories = [] //??

require('../factories')(factory, Models)

beforeEach((done) => {
  Models.sequelize.sync({ force: true }).then(() => {
    done();
  });
});

module.exports = {
  factory,
  Models,
  expect,
};

```
- Go to book.js in the models and put the title as an object and set allowNull to false in the title object along with the datatype string

- Go to books spec and code following:
```
  describe("constraints", () => {
    it("rejects null value for title", async () => {
      try {
        await factory.create("Book", { title: null });
        expect.fail();
      } catch (error) {
        expect(error.errors).to.containSubset([
          { message: "Book.title cannot be null" },
        ]);
      }
    });
  });

  describe("validations", () => {
    it("rejects empty string for title", async () => {
      try {
        await factory.create("Book", { title: "" });
        expect.fail();
      } catch (error) {
        expect(error).to.include({
          message: "Validation error: You need to set a title!",
        });
      }
    });
  });

```
- Run test and see it FAIL 
- Go to books model and add to the title object:
    ```
    validate: {
      notEmpty: { msg: 'You need to set a title' }
    }
    ```
- Run the test, and boyah- green. Hopefully??
**experiments away to try break the test**

```
$ git commit young padawans 
```