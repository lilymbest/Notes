# **Python Functions**

Functions are the building blocks of programming and all programming languages.
- Code organization
- Code reusability
- Readability (when appropriately named)
___
### **Defining Functions In Python**
___
Basic function definition in python:

```python
def fahr_to_kelvin(temp):
    return ((temp - 32) * (5/9)) + 273.15
```

The first line starts with `def` which defines a function.

### **Minimal Function**
___
"Stubbing up" an empty function in python:

```python
def frist_function():
    pass
```
- `pass` is simply a "do nothing" statement.
- Empty functions in JS return undefined but Python returns `None`
- Cannot assign functions to variables.

### **Key Differences of Python vs. JS Functions**
___
- Function expressions do not exist in python. Functions are defined with `def` and these functions are never assigned to variables in JS.
- Python has anonymous/inline functions called `lambda`.
- Cannot invoke a python function before the code that defines it.

Lambda 
- Similar to arrow functions in JS 
- Implicity return a single expressions result 
- They can also be assigned to a variable. 
- **CANNOT** have any code block - only a single expression.

Example:

JS
```javascript
const nums = [1, 3, 2, 6, 5];
let odds = nums.filter(num => num % 2);
```
Python
```python
nums = [1, 3, 2, 6, 5]
odds = list( filter(lambda num: num % 2, nums) )
```

Lambda functions are useful in Django when using Python functions like map().

```python
# Not allowed until after the code below
add(5, 10)

def add(a, b):
  return a + b
```

### **Calling Functions**
___
Calling functions is the same as JavaScript and `callbacks` exists in Python as well.

```python
def add(a, b):
  return a + b
  
def sub(a, b):
  return a - b

def compute(a, b, op):
  return op(a, b)

print( compute(1, 2, add) )
```

### **Parameters and Arguments**
___
`Parameter` - Place holder for passing an input to a function.
Example:
```python
# a & b are parameters
def add(a, b):
  return a + b
```
Like JS the values/expressions passed into a function when calling it are `arguments`. 
```python
num = 5

# num & 10 are arguments
add(num, 10)
```
Python however requires the correct number of arguments to be provided.
Example:
```python
def add(a, b):
  return a + b
  
add()
  
# Generates the following error:
# TypeError: add() missing 2 required positional arguments: 'a' and 'b'
```
## **Accepting and varying number of arguments**
___

#### Python's * Parameter Specifier (*args)
___
Using the `*` specifier in a parameter list allows us to pass in a varying number of arguments.

Example:
```python
def f(*args):
    print( type(args) )
    for arg in args:
        print(arg)

f(1, 2, 'SEI')
''' Output:
<class 'tuple'>
-> 1
-> 2
-> SEI
```
While `*args` can be named anything it is best practice to use args.

Always use the *args parameter after any required positional parameters. For example:
```python
def dev_skills(dev_name, *args):
    dev = {'name': dev_name, 'skills': []}
    for skill in args:
        dev['skills'].append(skill)
    return dev

print(dev_skills('Alex', 'HTML', 'CSS', 'JavaScript', 'Python'))

-> {'name': 'Alex', 'skills': ['HTML', 'CSS', 'JavaScript', 'Python']}
```
#### Python's ** Parameter Specifier (**kwargs)
___
To access a varying number of named arguments **kwargs is used at the end of the parameter list:
```python
def dev_skills(dev_name, **kwargs):
  dev = {'name': dev_name, 'skills': {}}
  # unpacking the tuples returned by the items function
  for skill, rating in kwargs.items():
    dev['skills'][skill] = rating
  return dev

print(dev_skills('Jackie', HTML=5, CSS=3, JavaScript=4, Python=2))
```
#### Combining Positional, *args & **kwargs
___
You can define all three types of parameters in a function, but you have to do it in this order:

```python
def arg_demo(pos1, pos2, *args, **kwargs):
  print(f'Positional params: {pos1}, {pos2}')
  print('*args:')
  for arg in args:
    print(' ', arg)
  print('**kwargs:')
  for keyword, value in kwargs.items():
    print(f'  {keyword}: {value}')

arg_demo('A', 'B', 1, 2, 3, color='purple', shape='circle')

'''Output:
Positional params: A, B
*args:
  1
  2
  3
**kwargs:
  color: purple
  shape: circle
'''
```