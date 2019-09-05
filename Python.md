# Python

**Python** - A scripting language that was started in December 1989 and released in 1991 by Dutch programmer Guido van Rossum.

- Python is a high-level interpreted programming language designed for writing applications where programmers don't have to worry about memeory management. [Python Packet Index](https://pypi.org/)
___
## Python syntax 
___
Designed to be more readable by using more english key words then symbols. && = and in python. 

- Uses indentation to define blocks of code.
- Comments are defined with # and anything after it will not run. Multiline coments use tripple quotes(""") or a # on each line
- Naming a class and a variabe may have different case types (snake case camel case etc...).
- Boolean values are uppercase
___
## Data Types
---
- <class 'int'> = 25
- <class 'str'> = 'string'
- <class 'bool'> = True
- <class 'float'> = 3.14159
- <class 'complex'> = 3+4j
- <class 'NoneType'> = None
___
## Math Operations
___
- (+)
- (-)
- (*)
- (/)
- (%)
- (**)

Note: Increment Operators Do not exist in python (++), (--).

___
## Converting Between Data Types
___
- str(item)
- int(item, base)
- float(item)
- hex(int)
- oct(int)
- tuple(item)
- list(item)
- dict(item)

Ex. str(5) = '5'

---
## Python Built in Functions
---
- len() = length
Ex. len("texas") = 5
---
## Control Flow
---
Control Flow - the order in which code executes in a program.

---
## Truthy & Falsey
---
False
- False
- None
- Zero (In any numeric type)
- Empty sequences or collections 
    - '' (Empty String) 
    - [] (Empty list)
    - () (Empty Tuple)
    - {} (Empty Dictionary)
    - range(0) (Empty Range)
---
## Logical Operators
---
- or = || (If the first operand is truthy, return it, otherwise return the second operand)

- and = && (If the first operand is falsey, return it, otherwise return the second operand)
---
## Comparison Operators
---
- (<) - Less than
- (>) - Greater Than
- (<=) - Less than or equal to
- (>=) - Greater than or equal to
- (==) - Equal to
- (!=) - Not equal to 

# **Python Containers**

Frequently in an application you need to maintain collections of data within a container data type.

Built-in Python containers
- `Dictionaries`
- `Lists`
- `Tuples`
___
## Dictionaries
___
Dictionaries are to Pyton as Objects are to JavaScript.
It provides a container for key: value pairs (reffered to as items) and have a class type of dict.

### **Dictionary - Basic Syntax**
___
Like objects in JS, dictionaries are created with a set of curly braces.
```python
student = {
    'name': 'Fred',
    'course': 'SEI',
    'current_week': 7
}
```
- Strings used as keys must be quoted.

- If not quoted, Python expects the identifier to be a variable holding what you want to use as the key. This is similar to how computed properties work in JS.

### **Features**
___
- Dictionaries are `unordered`
- Dictionaries are `mutable`
- The values assigned to a key can be changed
- Additional items can be added
- Exisitng items can be deleted
- Any `immutable` type can be used as a key(numers, tuples).

### **Dictionary - Getting/Setting Values**
___
Square brackets are used to get and set an item's value:
```python
name = student['name']
print(name)
> 'Fred'
student['name'] = 'Tina'
print(name)
> 'Tina'
```
You cannot acces itmes in python dictionary using dot notation.

### **Dictionary - get Method**
___
Where JavaScript returns undefined when accessing a property that does not exist, a dictrionary will cause a `KeyError`
```python
 birthdate = student['birthdate']
 > KeyError: 'birthdate'
 print( student.get('birthdate') )
 > None
 # Provide a default value if key not in dictionary
 print( student.get('birthdate', '07-04-1776') )
 > 07-04-1776
```
### **Dictionary - in Operator**
___
- Another way to avoid the KeyError is to use the in operator to check if the dictionary includes a key:

```python
if 'course' in student:
    print(f"{student['name']} is enrolled in {student['course']}")
else:
    print(f"{student['name']}is not enrolled in a course")
```
### **Dictionary - Adding Items**
___
`Assigning a key that does not exist will create a new item in the dictionary:`
```python
student['age'] = 21
```

### **Dictionary - Deleting Items**
___
```python
del student['age']
#Then varify that the item was deleted
'age' in student
> False
```

### **Dictionary - Number of Items**
___
```python
print(student)
> {'name': 'Tina', 'course': 'SEI'}
len(student)
> 2
len ({})
> 0
```

### **Dictionary - Iterating Items**
___
`for` loops are used to iterate over the items in a dictionary. The following is considered to be a Python anti-pattern

`Anti-pattern` - A common response to a recurring problem that is usually ineffective and risks being highly counterproductive.

```python
#NOT Best Practice
for key in student:
    print(f'{key} = {student[key]}')
```

```python
#Best practice
for key, val in student.items():
    print(f'{key} = {val}')
```
The student.items() call above returns a wrapped set of tuples:
```python
student.items():
 > dict_items([('name', 'Tina'), ('course', 'SEI')])
```
The for statement "unpacks" the tuples by assigning its values to multiple variables like with key, val above.

### Dictionary Practice Exercise
___
- Define a dictionary names where_my_things_are where the keys are things you have and values are where they are.
- Write a for loop that iterates over the items and prints each one.

```python
where_my_things_are = {
    'computer': 'desk',
    'phone': 'pocket',
    'headphones': 'coffee table'
}

for key, val in where_my_things_are.items():
    print(f'{key} = {val}')
```

___
## Lists
___
### **Lists - Basic Syntax**
- Created with square brackets
```python
colors = ['red', 'green', 'blue']
```
- Numbers of items in a list is returned using the built in len() function:
```python
len(colors)
> 3
```

### **Features**
___
-  `Mutable`
    - Items in the list can be replaced
    - Items can be added and removed from a list
- Considered to be a `sequence` type in Python
-Can contain anything including other lists.

`Sequence` - A generic term used for an ordered collection. Other squence types include `strings` and `tuples`.

### **Lists - Accessing Elements**
___
Unlike in JavaScript negative integers can be used to index from the end of a list:
```python
colors[-1]
> blue
```
### **Lists - Assigning Elements**
___
Square brackets are used to target an element of a list for assignment:

```python
colors[-1] = 'brown'
print(colors)
> ['red', 'green', 'brown']
```

### **Lists - Adding Elements**
___
The Python append() method is equivalent to JavaScript's push() method.

```python
colors.append('purple')
```
Unlike the `push()` method `append()` can only add one item and does not return a value.

For adding multiple items use the `extend()` method.

```python
colors.extend(['orange', 'black'])
```
### **Lists - Inserting Elements**
___
Adding items to anywhere but the end of the list the `insert()` method is used. Similar to the `slice()` method in JavaScript.
```python
print(colors)
> ['red', 'green', 'brown', 'purple', 'orange', 'black']
colors.insert(1, 'yellow')
> ['red', 'yellow', 'green', 'brown', 'purple', 'orange', 'black']
```
### **Lists - Deleting Elements**
___
```python
print(colors)
> ['red', 'yellow', 'brown', 'purple', 'orange', 'black']
del colors [1]
print(colors)
> ['red', 'brown', 'purple', 'orange', 'black']
```
There is also a `remove()` method that removes the first item that matches what you pass in.
```python
print(colors)
> ['red', 'brown', 'purple', 'orange', 'black']
colors.remove('orange')
print(colors)
> ['red', 'brown', 'purple', 'black']
```
No value is returned by the `remove()` method.

### **Lists - Clearing**
___
The `clear()` method clears out the whole list

```python
print(colors)
> ['red', 'brown', 'purple', 'black']
colors.clear()
print(colors)
> []
```

### **Lists - Iteration**
___
Again the for loop is the best practice for iterating over the items in a list.

```python
colors = ['red', 'green', 'blue']
for colors in colors:
    print(color)
> red
> green
> blue
```
The built in `enumerte() `function provides the index and value to the `for` loop.

```python
for idx, color in enumerate(colors):
    print(idx, color)
> 0 red
> 1 green
> 2 blue
```
___
## List Comprehensions
___
One of the most powerful features in Python is list comprehension.

`List Comprehension` - Provides a consise way to create and work with lists.

For example if you wanted to square all the numbers in a list and put them into a new list, you may use a for loop like this:

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# I want 'n * n' for each 'n' in nums 
squares = []
for n in nums:
    squares.append(n * n)
print(squares)
> [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
#### `List comprehenstion can reduce this code to:`

```python
# I want 'n * n' for each 'n' in nums 
squares = [n * n for n in nums]
```
The comprehension is basically an advanced for loop within square brackets which, of course, returns a new list.

### **Lists Comprehensions - Basic Syntax**
___

[< expression > for < item > in < list >]

This reads as: I want < expression > for each < item > in < list >

### **Lists Comprehensions - Filtering**
___

List comprehension can be used for filtering as well. Start by using a for loop to map and filter simultaneously.

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

even_squares = []

for n in nums:
    square = n * n 
    if square % 2 == 0:
        even_squares.append(square)
print(even_squares)
> [4, 16, 36, 64, 100]
```

#### `With filtering we can reduce this code to one line.`
```python
even_squares = [n * n for n in nums if (n * n) % 2 == 0]
```
___
## Tuples
___
Tuples are very similar to lists. They can be defined in different ways.

Most Basic tuple:

```python
colors = ('red', 'green', 'blue')
print(colors)
> ('red', 'green', 'blue')
print( len(colors) )
> 3
```
The commas is the syntax to actually define the tuple instead of the parentheses. So you can infact run the code with out parentheses but it is NOT considered best practice:

```python
colors = 'red', 'green', 'blue'
print(type(colors))
> <class 'tuple'>
```

However, creating single-item tuples without parens requires a trailing comma:

```python
colors = 'purple',  # tuple, not a string
print(type(colors), len(colors))
> <class 'tuple'> 1
print(colors)
> ('purple',)
```
### **Differences Between Tuples and Lists**
___
- Tuples are immutable, and there for useful for protecting data that you don't want changed.

- Tuples in Python are iterated over faster than lists. They can also be used for keys in dictionaries.

- Generally Tuples are used to contain heterogeneous data types and lists for homogeneous data types.

- Are classified by how many elements they contain. Example: 2-tuple would be used to hold a key and its value.

### **Tuples - Accessing Elements**
___
Although tuples cannot be modified like lists, we can retrieve their elements in the exact same way:

```python
colors = ('red', 'green', 'blue')
green = colors[1]
print(green)
> green
```
Sequences also have an index() method that returns the index of the first match:

```python
colors = ('red', 'green', 'blue')
blue_idx = colors.index('blue')
print(blue_idx)
> 2
```
### **Tuples - Accessing Elements**
___
Iterated upon with for loops:

```python
colors = ('red', 'green', 'blue')
for idx, color in enumerate(colors):
    print(idx, color)
> 0 red
> 1 green
> 2 blue
```
### **Tuples - Unpacking**
___
A convenient feature called unpacking is for doing multiple variable assignment:

```python
colors = ('red', 'green', 'blue')
red, green, blue = colors
print(red, green, blue)
> red green blue
```
A tuple of variables on the left-side of the assignment operator and a tuple of values on the right is all it takes.

### **Slicing Sequences**
___

The slice operator([m:n]) is one of the coolest tricks in Python. Since sequence types are a collection of items (BTW, characters are the items in a string), we can target subsets, called slices, of those items using [m:n]:

```python
short_name = 'Alexandria'[0:4]
print(short_name)
> Alex
```
`Note:` Slice includes up to, but not including the index to the right of the colon.

If the first index is omitted, the slice copies the sequence starting at the beginning:

```python
colors = ('red', 'green', 'blue')
print( colors[:2] )
> ('red', 'green')
```
If the up to index is omitted, the slice copies the sequence all the way to the end:

```python
colors = ['red', 'green', 'blue']
print( colors[1:] )
> ['green', 'blue']
```
