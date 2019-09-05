# Python
---
**Python** - A scripting language that was started in December 1989 and released in 1991 by Dutch programmer Guido van Rossum.

- Python is a high-level interpreted programming language designed for writing applications where programmers don't have to worry about memeory management. [Python Packet Index](https://pypi.org/)
---
## Python syntax 
---
Designed to be more readable by using more english key words then symbols. && = and in python. 

- Uses indentation to define blocks of code.
- Comments are defined with # and anything after it will not run. Multiline coments use tripple quotes(""") or a # on each line
- Naming a class and a variabe may have different case types (snake case camel case etc...).
- Boolean values are uppercase
---
## Data Types
---
- <class 'int'> = 25
- <class 'str'> = 'string'
- <class 'bool'> = True
- <class 'float'> = 3.14159
- <class 'complex'> = 3+4j
- <class 'NoneType'> = None
---
## Math Operations
---
- (+)
- (-)
- (*)
- (/)
- (%)
- (**)

Note: Increment Operators Do not exist in python (++), (--).

--- 
## Converting Between Data Types
---
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

### **Basic Syntax**
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

### **Getting/Setting Values**
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

### **get Method**
___
Where JavaScript returns undefined when accessing a property that does not exist, a dictrionary will cause a `KeyError`
```python
 birthdate = student['birthdate']
 > KeyError: 'birthdate'
 print( student.get('birthdate') )
 > None
 # Provide a default value if key not in dictionary
 print( student.get('birthdate', '07-04-1777') )
 > 07-04-1777
```
### **in Operator**
___
- Another way to avoid the KeyError is to use the in operator to check if the dictionary includes a key:

```python
if 'course' in student:
    print(f"{student['name']} is enrolled in {student['course']}")
else:
    print(f"{student['name']}is not enrolled in a course")
```
### **Adding Items**
___
`Assigning a key that does not exist will create a new item in the dictionary:`
```python
student['age'] = 21
```

### **Deleting Items**
___
```python
del student['age']
#Then varify that the item was deleted
'age' in student
> False
```

### **Number of Items**
___
```python
print(student)
> {'name': 'Tina', 'course': 'SEI'}
len(student)
> 2
len ({})
> 0
```

### **Iterating Items**
___
`for` loops are used to iterate over the items in a dictionary. The following is considered to be a Python anti-pattern

`Anti-pattern` - A common response to a recurring problem that is usually ineffective and risks being highly counterproductive.

```python
for ket in student:
    print(f'{key} = {student[key]}')
```
- Best practice iteration is a `for` loop.

```python
for key, val in student.items():
    print(f'{key} = {val}')
```
The student.items() call above returns a wrapped set of tuples:
```python
student.items():
 > dict_items([('name', 'Tina'), ('course', 'SEI')])
```
The for statement "unpacks" the tuples by assigning its values to multiple variables like with key, val above.

---
## Lists
---
### **Basic Syntax**
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

`Sequence` - A generic term used for an ordered collection. Other squence types include `strings` and `tuples`.

### **Accessing Elements**
___
Unlike in JavaScript negative integers can be used to index from the end of a list:
```python
colors[-1]
> blue
```

Square brackets are used to target an element of a list for assignment:

```python
colors[-1] = 'brown'
print(colors)
> ['red', 'green', 'brown']
```

### **Adding Elements**
___
