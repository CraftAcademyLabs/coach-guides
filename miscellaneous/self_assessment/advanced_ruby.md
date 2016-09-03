### Advanced Ruby
#### What is a Proc?
A `Proc`, short for procedure, acts similar to a block, but can be saved as variables and reused. Think of them as blocks you can call over and over again on multiple arrays.

Be prepared to explain an instance when you would use a proc over a block.

### What is a lambda?
Lambdas are very similar to procs in terms of functionality. However, they have a few key differences. Lambdas check the number of arguments passed and will return an error if you try to pass the wrong number (a `Proc` sets extra variables to nil).

The other difference is that lambdas can handle a return function, whereas procs will return an error.

### What are the three levels of method access control for classes and what do they signify? What do they imply about the method?

The short answer is: Public, protected, and private.

**Public methods** can be called by all objects and subclasses of the class in which they are defined in.

**Protected methods** are only accessible to objects within the same class.

**Private methods** are only accessible within the same instance.

Be able to explain why this does or doesn’t matter, and when you would want to set a method as private.
