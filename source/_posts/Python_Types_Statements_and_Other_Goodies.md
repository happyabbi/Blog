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
``` python
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
``` python
student_names = ["Mark","Katarina","Homer"]
student_names[1:] == ["Katarina","Homer"]
student_names[1:-1] == ["Katarina"]
``` 

## Loops
### Printing List Elements
``` python
student_names = ["Mark","Katarina","Homer"]
print(student_names[0])
print(student_names[1])
print(student_names[2])
...
``` 
### For Loop
``` python
student_names = ["Mark","Katarina","Homer"]
for name in student_names:
    print("Student name is {0}".format(name))
``` 

### Other Code
``` python
for (var i = 0; i < someArray.length; i++ ){
    var element = someArray[i];
    console.log(element);
}
``` 

### Demo
``` python
for index in range(10)
    x += 10
    print("The value of X is {0}".format(x))

range(5,10) == [5,6,7,8,9]

range(5,10,2) == [5,7,9]

``` 

## Break and Continue
### Break
``` python
    student_names = ["James","Katarina","jessica","Mark","Bort","Frank Grimes","Max Power"]

    for name in student_names:
        if name == "Mark":
            print("Found him! " + name)
            break
        print("Currently testing "+name)
``` 
### Continue
``` python
    student_names = ["James","Katarina","jessica","Mark","Bort","Frank Grimes","Max Power"]

    for name in student_names:
        if name == "Bort":
            print("Found him! " + name)
            continue
        print("Currently testing "+name)
``` 

## While Loops
``` python
    x = 0
    while x < 10:
        print("Count is {0}".format(x))
        x += 1
``` 

### Infinite Loops
``` python
    num = 10
    while True:
        if num = 42:
            break
        print("Hello World")
``` 

## Dictionaries
``` python
    student = {
        "name" : "Mark",
        "student_id" : 15163,
        "feedback" : None
    }
``` 

### List of Dictionaries
``` python
    all_students = [
        {"name": "Mark", "student_id":15163},
        {"name": "Katarina","student_id":63112},
        {"name": "Jessica","student_id":30021}
    ]
``` 

### Dictionary Data
``` python
    student["name"] == "Mark"
    student["last_name"] == KeyError
    student.get("last_name","Unknown") == "Unknown"
    student.keys() = ["name","student_id","feedback"]
    student.values() = ["Mark",15163,None] 
    student["name"] = "James"
    del student["name"]
``` 

## Exceptions
``` python
    student = {
        "name" : "Mark",
        "student_id" : 15163,
        "feedback" : None
    }

    student["last_name"] = "Kowalski"

    try:
        last_name = student["last_name"]
        numbered_last_name = 3 + last_name
    except KeyError:
        print("Error finding last_name")
    except TypeError as error:
        print("I can't add these two together!")
        print(error)
    except Exception:
        print("Unknown error")

    print("This code executes!")
``` 

## Other Data Types
``` python
    complex
    long # Only in Python 2
    bytes and bytearray
    tuple = (3,5,1,"Mark")
    set and frozenset
    set([3,2,3,1,5]) == (1,2,3,5)
``` 










