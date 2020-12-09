## Node Notes
### Demo: Node part one second day

- Talking about the serializer that we have implemented and the flaws that it has
- Came up with a helpers method 
- takes the response and the attributes
- refactored the booksserializer, so in the index it is two functions
- one controlls the query and one that controlls the response
- not really want we want
- No good solution yet  
(putting these refactorings and experiments on a different branch)

- one endpoint, request specs, unit tests, learned debugging, 
- what we havent tested or explored is the associations
- scratching the surface there - start with small things
- set up an association with a author model
- author has many books and a book can only have one author

- lets branch of first 
- **Where should we start to do it TDD way?**

- Think from the users point of view, at all times, when developing a new feature. 

- go into tests/booksEndpoint.test.js and add the author

```
it('responds with a collection of books', () => {
  const expectedBody = {
    books:
    [
      { id: 1, title: 'The Bible', author: { name: 'A lot of bishops'}}
      { id: 2, title: 'The Quran', author: { name: 'Gabriel'}}
    ]
  }
})
```
- run the test and see it fail
- go into serializers/booksSerializer.js
```
return {
  attributes: ['id', 'title'],
  include: [
  model: models.Author,
  as: 'author',
  attributes: { exclude: ['id', 'createdAt', 'updatedAt'] }
  ]
}

```
- run test and now it will not even run
- If we try to run a test when the code can not be executed then mocha just hangs and you get nothing, thats a bit of a problem
- putting a try catch block where we query the db, it doesnt fly either
- we need to drive blind for a little bit, we acknowledge that the feature tests are not enough
- so now we will move to the book unit test, since we already have it, it is the right way to go
- that test should tell us tht the association doesnt excist 
- go to tests/models/books.spec.js and add another described block
```
const Author = require('../../models/author)


describe('associations', () => {
  before(() => {
    DescribedModel.associate({Author})
  })

  it('defines a belongs to association', () => {
    expect(DescribedModel.belongsTo)
      .to.have.been.calledWith({Author})
  })
})
```
- This will fail, and let enjoy watching it, because the module doesnt excist 
- showing the "it.only(....)" to only execute a specific test

```
$ sequelize model:generate --name Author --attributes name:string
```
- New model and new migration is created

```
$ sequelize db:migrate
```
- Run the test again now when we have the author model, should get an error about that the association is missing
- we need to define the association
- go to models/books.js

```
Book.associate = (models) => {
  Book.belongsTo(models.Author, { foreignKey: 'authorid', as: 'author'})
}
```
- run the test again (aaand we get the same error?)
- **Author has to be called as an obejct in the argument, it is corrected in the code snippets above**

- Run the feature test, and it still doesnt fly
- Now we need to have a look at the books factory and associate that little guy
```
// booksFactory.js 

factorye.define('Book', Models.Book, {
  ...
  authorId: factory.assoc('Author', 'id')
})
```
- we need a foreign key to books from author through a migration
- In rails we can name the migrations so it knows what to do, which we can not in node
```
$ sequelize migration:generate --name add_author_to_books
```
- Go to the new migration
```
// up query
return queryInterface.addColumn(
  'Books',
  'authorId',
  { 
    type: Sequelize.INTEGER,
    references: {
      model: 'Authors',
      as: 'author',
      key: 'id'
    }
  }
)

// down query
return queryInterface.removeColumn(
  'Books',
  'authorId',
)
```
```
$ sequelize db:migrate
```
 
- create a new factory for the author
```
// copy the code from Books factory and change the name from book to author

module.exports = (factory, Models) => {
  factory.define('Author', Models.Author, {
    name: 'Foo'
    ...
  })
}
```
- Now everything should go green on the books.spec.js
- Now we want to check the feature test and see if we have another output- and it is still the same
- go to the booksendpoint test: 
```
beforeEach(async () => {
  ... 
  const author = await factory.create('Author', {
    id: 100, name: 'Gabriel'
  })
})

//on each factory book
{ id: 1.... authorId: author.id}

// change on the assercion that gabriel is the author of both books
```
- Run the test
- looking in the serializer, looking in the controller

*adding the models as an import to the serializer*

Problem solved and tests are green!