### Node Authentication Demo

- Checking so everything is green and happy from the sessions yesterday

```
$ yarn add -D nodemon
```
- for hot reload, which we dont really use since we run our tests, right?

- checkout a new branch, we are going to work on a way to authenticate users
- In this feature we will close down the books route for any users that are not authenticated 

```
describe('for none authenticated user', () => {
  it('should respond with 401', () => {
    expect(response.status).to.equal(401)
  })
})
describe('for authenticated user', () => {
 // move all your it blocks into this describe block
})
```
- this will fail ofc
```
// move your beforeEach block for the get request into your describe block for none authenticated users and write this in your block for authenticated users

beforeEach(async()=> {
  response = await request.get('/api/v1/books').set('Authorization', 'somerandomtoken'), 
})
```
- to get the token do this in your beforeEach for the auth users

```
beforeEach(async()=> {
  await request
  .post('//api/v1/auth/login')
  .send({email: 'user@random.com', password: 'password'})
  .then((response) => { token = response.body.token })

  response = await request.get('/api/v1/books').set('Authorization', token), 
})
```
- go to app.js
```
app.use('/api/v1/auth', authentication)

// change all your vars to const in the app.js

const authentication = require(./routes/authentication)
```
```
$ touch routes/authentication.js
```
```
// routes/authentication.js

const express = require('express')
const router = express.Router()

router.post('/login', (req, res) => {
  res.send({token: 'whatever'})
})

module.exports = router
```
- check what response.body is in the debug console, got object token: whatever

- talking about encrypting the passwords
- We will today focus on that what we send in will generate a token, and NOT encrypting the password just yet
- We want to use this email and password to create something that could later identify the user

- we are sending of the information in a postrequest, and receiving a token, which is not how we want to do it 
- go to authentication.js 
```
const express = require('express')
const router = express.Router()
const authenticationsController = require('../controllers/authenticationsController')

router.post('/login', authenticationsController
})

module.exports = router
```
```
$ touch controllers/authenticationsController.js
```
- move into that file
```
const authenticationsController = {
  login(req, res) {res.send({ token: 'whatever' })
  }
}

module.exports = authenticationsController
```

```
const express = require('express')
const router = express.Router()
const authenticationsController = require('../controllers/authenticationsController')

router.post('/login', authenticationsController.login
})

module.exports = router
```
- the req.body in the debug console should be the same after this refactoring 
```
$ yarn add jsonwebtoken
```
```
// authentications controller

const jwt = require('jsonwebtoken')
const salt = 'thisismysecretstringthelongerthebetter'

const authenticationsController = {
  async login(req, res) {
    const { email } = req.body 
    const token = await jwt.sign({email: email}, salt)
    res.send({ token: token })
  }
}

module.exports = authenticationsController
```
- put a debugger on the response and run the test and see the token
- go to jwt.io 
- copy the token, and paste it in the window, and then you can see the user email

*experiments with the payload to see different results on jwt.io, and showcasing that the password should be hashed*

```
// authentications controller

const jwt = require('jsonwebtoken')
const salt = 'thisismysecretstringthelongerthebetter'

const authenticationsController = {
  login(req, res) {
    const { email } = req.body 
    const token = jwt.sign({email: email}, salt, {expiresIn: 36000})
    res.send({ token: `Bearer ${token}` })
  }
}

module.exports = authenticationsController
```
- the real authentication would be done by passport, which is like device for Rails. We wont be able to touch upon that now

**TAKE A LOOK AT THE EXPIRE THING, changed in the code snippets so took away the async await and added the expiresIn,**

**The first argument(the payload), MUST be an object, not a string**