---
title: Python Tutorial(2) - Types,Statements,and Other Goodies
categories:
- Python 3
tags:
- Python basic
---

## Introduction
- Data Types
- Flow Control
- Loops
- Dictionaries
- Exceptions
- Other Data Types

## Types in Python - Wait, What?
``` bash
    // C# or Java
    int answer = 42;
    String name = "PythonBo";

    # Python
    answer = 42
    name = "PythonBo"    
``` 

### Type Hinting

``` python
    def  add_numbers(a:int,b:int) -> int:
        return a + b
``` 

## Integers and Floats
``` python
    answer = 42
    pi = 3.14159
    answer + pi = 45.14159 # Don't worry about conversion!
    int(pi) == 3
    float(answer) == 42.0
``` 

## Strings
``` python
    'Hellow World' == "Hellow World" == """Hellow World""" 
    "hello".capitalize() == "Hello"
    "hello".replace("e","a") == "hallo"
    "hello".isalpha() == True
    "123".isditit() == True # Useful whe converting to int
    "some,csv,values".split(",") == ["some","csv","values"]    
``` 
### String Format Function

``` python
    name = "PythonBo"
    machine = "HAL"
    "Nice to meet you {0}. I am {1}".format(name,machine)
    f"Nice to meet you {name}. I am {machine}"
```

## Boolean and None
``` python
    python_course = True
    java_course = False
    int(python_course) == 1
    int(java_course) == 0
    str(python_course) == "True"

    aliens_found = None

```
## if Statements

``` python

    number = 5
    if number ==5 :
        print("Number is 5")
    else:
        print("Number is NOT 5")

``` 

### Truthy and Falsy Values

``` python

    number = 5
    if number :
        print("Number is defined and truthy")

    text = "Python"
    if text:
        print("Text is defined and truthy")

``` 

### Boolean and None

``` python

python_course = True

if python_course: # Not python_course == True
    print("This will execute")

aliens_found = None
if aliens_found:
    print("This will NOT execute")
s
``` 
### Not if

``` python
    number = 5
    if number != 5:
        print("This will not execute")

    python_course = True
    if not python_course:
        print("This will also not execute")
``` 


### Multiple If Conditions
``` python
    number = 3
    python_course = True
    if number == 3 and python_course:
        print("This will execute")

    if number == 17 or python_course:
        print("This will also execute")
``` 

### Ternary if Statements
``` python
    a = 1
    b = 2
    "bigger" if a > b else "smaller"
``` 

## Lists
``` python
    student_names = []
    student_names = ["Mark","Katarina","Jessica"]
``` 

### Getting List Elements

``` python
    student_names = ["Mark","Katarina","Jessica"]
    student_names[0] == "Mark"
    student_names[2] == "Jessica"
    student_names[-1] == "Jessica"
    student_names[-2] == "Katarina"
    student_names[-3] == "Mark"    
``` 

### Changing List Elements
``` python
   student_names = ["Mark","Katarina","Jessica"]
   student_names[0] = "James"

   student_names == ["James","Katarina","Jessica"]
``` 

### List Functions

``` python
    student_names = ["Mark","Katarina","Jessica"]
    student_names[3] = "Homer" # No Can do!
    student_names.append("Homer") # Add to the end
    student_names = ["Mark","Katarina","Jessica","Homer"]
    "Mark" in student_names == True  # Mark is still there!
    len(student_names) == 4 #How many elements int the list
    del student_names[2] # Jessica is no longer in the list :(
    student_names = ["Mark","Katarina","Homer"]    

``` 

### List Slicing

student_names = ["Mark","Katarina","Homer"]
student_names[1:] == ["Katarina","Homer"]
student_names[1:-1] == ["Katarina"]

