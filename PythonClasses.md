## Classes in Python

### Review of OOP
___
Python is an Object Oriented Programming(OOP) language.

**OOP** - Object Oriented Progamming is characterized by programming with `objects` that represent real-world objects of the application.

Example: A book would have a book object with all its properties and methods.

![book](https://i.imgur.com/3AQdh0F.png)

Objects bundle related properties (attributes) and methods (behavior) together. This is the encapsulation priciple in OOP.

In an OOP language, classes are used to create objects. We instantiate a class to obtain an instance (object) of that class.

Everything in Python is an object.

Python uses a dir() function that can be used to list an objects attributes and methods.

```python
nums = [1, 2, 3]
print( dir(nums) )
```
___
## **Basic Python Class**
___
```python
class Dog():
    def __init__(self, name, age = 0):
        self.name = name
        self.age = age
    def bark(self):
        print(f'{self.name} says woof!')
```

Python automatically calls the `__init__` magic method when a new dog is created. shot for initialize the method is used to initalize the properties of a new object.

```python
age = 0
```
Above is a default parameter and will be assigned the result of the expression to the right of the = if the function is called with out an argument for that parameter.

```python
self.name = name
self.age = age
```
The above are attributes of the dog object

```python
def bark(self):
    print(f'{self.name}says woof!')
```
Bark is an instance method.

Instance Method - A method associated with objects, each instance method is called with a hidden argument that refers to the current object.

The `self` in the above function is equivilant to `this` in JavaScript, C++, etc...

### **Creating Objects by Instancing a Class**
___

By defining the dog class we know the structure that each of the other dogs will have.

```python
spot = Dog('Spot', 8)

print(spot)
-> similar to <__main__.Dog object at 0x7f27bad2c208>

# print the name and age attributes of the spot object
print(spot.name, spot.age)  
-> Spot 8

# invoke the spot object's bark instance method
spot.bark() 
-> Spot says woof!

```
Using the default parameter for a new dog's age:
```python
dog = Dog('Lassie')
print(dog.name, dog.age)
-> Lassie 0
```
### **Overriding Methods**
___
```python
spot = Dog('Spot', 8)

print(spot)
-> similar to <__main__.Dog object at 0x7f27bad2c208>
```
This gives an unfriendly output. You can fix this my overriding the `__str__` method that the print function calls automatically to obtain the strinf output.
```python
class Dog():
  def __init__(self, name, age = 0):
    self.name = name
    self.age = age

  def bark(self):
    print(f'{self.name} says woof!')
    
  def __str__(self):
    return f'Dog named {self.name} is {self.age} years old'

spot = Dog('Spot', 8)

print(spot)
-> Dog named Spot is 8 years old
```
