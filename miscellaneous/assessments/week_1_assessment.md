##Question 1 - Variables
Create a variable and set it equal to 'variable'.  
What are some different data types? Write a few examples.

##Question 2 - Hashes and Arrays
Open irb. We're going to make some cars.
Create two hashes, one for each `car`, with the following attributes: `wheels`, `max_speed`, `color`  
Create an array that contains both cars.  
How do we use the array to access the second car? How do we find the second car's `color`?

## Question 2 - Classes and Methods
Create a new file called 'car.rb' with:
 - a class Car
 - a method that "paints" a car a new color.
 - a method that checks if the current car is the first car in an array. (`is_first_car?`)
Open irb. Load your 'car.rb' file. Then create two arrays like in the previous exercise and use the `is_first_car?` method.

## Question 3 - Rspec
How do you initialize `rspec` in a folder? Do it in our cars folder.  
We would ordinarily have written our tests first, then written code to make them pass. Why?  
Create two unit tests for our `Car` class - one for each of our methods.
Create an `instance_double` `Driver`. A driver should have a car. Write a third test for this and make it pass.
