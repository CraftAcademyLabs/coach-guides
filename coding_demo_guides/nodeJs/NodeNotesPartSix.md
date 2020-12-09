## Node Notes
### Demo: Node Part after lunch (should have been about profiling)

- tie up loose ends
- imagine i want to change my seeds
```
$ sequelize db:drop
```
```
$ NODE_ENV=test sequelize db:drop
```
```
$ sequelize db:create
```
```
$ NODE_ENV=test sequelize db:create
```
```
$ sequelize db:migrate
```

```
const models = require('../../models')
// up method

const thomas = await models.Author.create({ name: 'Thomas'})
const adi = await models.Author.create({ name: 'Adi'})
await queryInterface.bulkInsert(
  'Books',
  [
    { title: 'learn node with thomas', authorId: thomas.id}
    { title: 'learn sequelize with adi', authorId: adi.id }
  ], {}
)

```
```
$ sequelize db:seed:all
```
```
$ sequelize db:seed:undo:all
```
**Making another example on how to add authors to a book with only one collected const**

**To open a file in Node, open the node console and then require it inside**

*After that doing some experiments that was very hard to follow*