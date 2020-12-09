## Node Notes
### Demo: Node second part after lunch

- Now we will set up tests for what we just did
- We do not only want to test the endpoints but also test the models, like in rails

*branching off* unit_test_setup or what ever you want. 

- creating our test helpers in the root folder
  ```
  $ mkdir tests/test_helper
  $ touch tests/test_helper/index.js
  ```

- Go into that file and *i didn't catch the code to put in there*

- in the test folder, create a subfolder and call it models
  ```
  $ mkdir tests/models
  $ touch tests/models/Books.spec.js
  ```

- in package.json:
  ```
  "test": "NODE_ENV=test NODE_NO_WARNINGS=1 mocha --recursive --exit tests"
  ```

  ```
  $ yarn add -D sequelize-test-helpers
  ```
- bare the warning about sinon in mind :)

 - go back to books.spec 

 ```
// tests/Models/Book.spec.js

const {
  sequelize,
  dataTypes,
  checkModelName,
  checkPropertyExists,
} = require("sequelize-test-helpers");

const Book = require("../../models/book");

describe("Book", () => {
  const DescribedModel = Book(sequelize, dataTypes);
  const subject = new DescribedModel();

  // here we want to check for the checkModelName
  // so this is actually a test with a testhelper
  checkModelName(DescribedModel)("Book");
  checkPropertyExists(subject)("title");
})
```
```
$ yarn test
```
- should get error about missing sinon, which is a stubbing and mocking

```
  $ yarn add -D sinon sinon-chai
```
- go to testhelpers/index.js

```
const sinonChai = require('sinon-chai')
chai.use(sinonChai)
```
- run test again, should get some green output
- go back to the test and break it, write the wrong names and see that the test failes

- we want to run the tests directly from the editor instead of the terminal 

- go the degub runner and add another configuration in the launch.js :
"Node JS Mocha Tests"
```
"name": "Mocha - All"
  "args": [
    // (remove u and tdd and leave the rest)
    "${workspaceFolder}/**/*.spec.js"
  ]
  *create a new one*
  "env": {
    "NODE_ENV": "test",
    "NODE_NO_WARNINGS": "1"
  },
  "console": "integratedTerminal"
  "internalConsoleOptions": "neverOpen"
```

- copy everything and paste in down bellow
- change the name from 'Mocha - All' to 'Mocha - Current File'
- on the arg change {workspacefolder} to {file} and delete the rest after that on that line

- go to the runner and choose Mocha - All, should go green. And the test should run in the editors terminal
- Run the same thing with mocha current file and it should still go smooth, if you are running the correct file

BOOOM! 