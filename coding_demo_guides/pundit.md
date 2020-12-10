**PROBABLY NEEDS TO BE UPDATED TO MORE GENERAL EXAMPLE**

- Authentication - who is the user?
- Authorization - what is the user allowed to do?

- Will implement a package to exchange this if else

- lets pretend that you have several roles and use cases and then you can end up in a cluster fuck
- in that case it is much easier to use a package
- single responsibility, it is not the controllers responsibility to deal with this authorization

- Show pundit, the actual gem 
- show the instructions
- include it in the applications controller
- run a generator 

```
gem 'pundit'
```
```
$ bundle
```
```
#applicationscontroller

include Pundit
```
```
$ rails g pundit install 
```
- will create an application policy, what is that?
- Pundit are all about policies 
- pundit plays very well with devise because it asks for current_user 
- the policy is a set of rules that allows us to choose what the user can do or not
- the name of the policy should include the name of the resource
- pure ruby class, back to basics, plain ruby
- define the attributes and initialize them
- define the method you want to authorize, and the corner cases where you want to hinder someone from do something that is not authorized 
- better to use || and ! instead of 'or not'

```
$ rails g pundit:policy WatchlistItem
```
- lets look at the policy
- it inherits from the application policy 
- Remove the scope

```
def create?
  binding.pry
end
```
- remove the if statements

```
def create 
  authorize(WatchlistItem.create)

  ...
end
```
- and we hit the policy
```
def create?
  true
end
```
- now the test is passing because we always return true, no matter what 
- but now the sad path is not passing because it actually creates the watchlistitem 
- if we change it to false then both will fail
```
def create?
  user.subscriber
end
```
- now the first will pass and the second will fail because we get the error from pundit
- we can rescue that error by passing in the applications controller if we want a generic error
```
#watchlistcontroller

rescue_from Pundit::NotAuthorizedError, with: :user_not_authorized 

..

private 

def user_not_authorized
  render json: { message: 'what ever message' }
end
```

- run everything now, and it is all passing 
- we have the exact same test. we are just refactoring the logic we have for this authorization
- the create method is a bit neater  but we actually have more code
- but we have separated the responsibilities and if we would have a lot of cases were we would deal with authorization then this would make more sense
