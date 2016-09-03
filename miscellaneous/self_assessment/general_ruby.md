### General Ruby Knowledge
#### What is a class?
You should easily be able to explain not only what a class is, but how and when you would create a new one as well as what functionality it would provide in the larger context of your program.

#### What is the difference between a class and a module?
The straightforward answer: *"A module cannot be subclassed or instantiated, and modules can implement mixins"*.

Be prepared to discuss what this actually means in real life, and when you would use a module vs. a class and why.

### What is an object?
Textbook answer here is that an object is an instance of a class and has state, behavior, and identity. In a plain text example, you can say that a truck and a car are both objects of the class Vehicle, or that apple and pear are both objects of the class Fruit.

You should be able to explain in detail how object structure and behavior relate to their common class, and why this is so important in Ruby (see question 1).

### How would you declare and use a constructor in Ruby?
Constructors are declared via the initialize method and get called when you call on a new object to be created.

Using the code snippet below, calling Order.new acts as a constructor for an object of the class Order.

```ruby
class Order
  def initialize(customer, dish)
    @customer = customer
    @dish = dish
  end
end
```

### How does a symbol differ from a string?
Short answer: symbols are immutable and reusable, retaining the same object_id.

Be prepared to discuss the benefits of using symbols vs. strings, the effect on memory usage, and in which situations you would use one over the other.

### How and when would you declare a Global Variable?
Global variables are declared with the ‘$’ symbol and can be declared and used anywhere within your program. You should use them sparingly to never.

### How would you create getter and setter methods in Ruby?
Setter and getter methods in Ruby are generated with the `attr_accessor` method. attr_accessor is used to generate instance variables for data that's not stored in your database column.

You can also take the long route and create them manually.

### Describe the difference between class and instance variables?
Class variables are created with the prefix `@@` and are shared by all objects in a class.

Instance variables are created with the prefix `@` and belong to a single object within a class.

Beyond the simple textbook definition, be able to describe an example of a class and how you would use class and instance variables within it, and how they relate to issues of class inheritance.

### Explain some of the looping structures available in Ruby?
For loop, While loop, Until loop.

Be able to explain situations in which you would use one over another.
