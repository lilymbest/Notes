# **Python Functions**

Functions are the building blocks of programming and all programming languages.
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

### **Key Differences of Python vs. JS Functions**
___
- Function expressions do not exist in python. Functions are defined with `def` and these functions are never assigned to variables in JS.
- Python has anonymous/inline functions called `lambda`