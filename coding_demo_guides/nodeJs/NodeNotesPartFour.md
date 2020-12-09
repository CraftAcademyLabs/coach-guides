## Node Notes
### Demo: Node Part second part after lunch

- We are done with configuration, lets dig into TDD/BDD
- In our request spec we are still looking for hardcoded values 
- the app is still responding with hardcoded values
- create a controllers folder and a books controller

```
$ mkdir controllers
```
```
$ touch controllers/booksController.js
```
- Go into that file:
```
const models = require('../models')

const booksController = {
  async index(req, res) {
    // query the db for all hooks
    // descide how the json object should look like: This should be a separate file, like AM serializers in Rails
    // And that descision is made in the serializer
    // send the json object to the requester
    res.json({books: booksIndex})

  }
}

module.exports = booksController
```

- Change the routes/books.js:

```
const express = require('express')
const router = express.Router()
const booksController = require('../controllers/bookController')

router.get('/', booksController.index)

module.exports = router
```

- create a serializers folder and a books serializer 

```
$ mkdir serializers
```
```
$ touch serializers/booksSerializer.js
```
- move into that file and write following code: 
```
const booksSerializer = {
  index() {
    return {
      attributes: ['id', 'title']
    }
  }
}

module.exports = booksSerializer
```

 - go back to the books controller:
 ```
 const booksSerializer = require('../serializers/booksSerializer')

  const booksController = {
    async index(req, res) { ....
    const eachSerializer = booksSerializer.index()
    const booksIndex = await models.Book.findAll(eachSerializer)
  ```
 - Run your tests

 - modify your booksEndPoints test file: 
 ```
 const {expect, factory} = require('./test_helper')

 beforeEach(async () => {
   await factory.createMany('Book', 2, [
    {
      title: 'The Bible
    } 
    {
      title: 'the Quran
    }
  ])
 }) 

 afterEach( async() => {
   await factory.cleanUp()
 })

```

- what have we missed?
- Debugging the controller, since we do not get any books
- Looking through the books controller
- something is up with the factory?
- (adding createdAt and updatedAt to the bot, didn't solve the problem)
- Adi gets a gold star, it needs to be a beforeEach in the describe block and not just a before block 

*important with the beforeEach and afterEach blocks*

*REMEMBER to change that in the notes about the section where we write the Booksendpoints test to get it right*




