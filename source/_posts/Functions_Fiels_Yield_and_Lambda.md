---
title: Python Tutorial(3) - Functions, Files, Yield, and Lambda
categories:
- Python 3
tags:
- Python basic
---

## Our App - PystudentManager
- Name: PystudentManager
- Student Details
- Easy to Expand
- From Console to a Web App

## Functions

``` bash
    print("Hello World")
    str(3) == "3"
    int("15") == 15
    username = input("Enter the user's name:")
```


``` python
    students = []

    def get_students_titlecase():
        students_titlecase = []
        for student in students:
            students_titlecase = student.title()
        return students_titlecase
    
    def print_students_titlecase():
        students_titlecase = get_students_titlecase()
        print(students_titlecase)
    
    def add_student(name):
        students.append(name)

    student_list = get_students_titlecase()

    add_student("Mark")
```

## Function Arguments

``` python
    students = []

    def get_students_titlecase():
        students_titlecase = []
        for student in students:
            students_titlecase = student.title()
        return students_titlecase
    
    def print_students_titlecase():
        students_titlecase = get_students_titlecase()
        print(students_titlecase)
    
    def add_student(name, student_id=332):
        student = {"name": name, "student_id": student_id }
        students.append(student)

    def var_args(name, *args):
        print(name)
        print(kwargs["description"],kwargs["feedback"])

    student_list = get_students_titlecase()
    add_student( name = "Mark" , student_id = 15)

    var_args("Mark",description="Loves Python",feedback=None,pluralsight_ssubscriber=True)
```

## Adding Students to Our App

``` python
    students = []

    def get_students_titlecase():
        students_titlecase = []
        for student in students:
            students_titlecase = student["name"].title()
        return students_titlecase
    
    def print_students_titlecase():
        students_titlecase = get_students_titlecase()
        print(students_titlecase)
    
    def add_student(name, student_id=332):
        student = {"name": name, "student_id": student_id }
        students.append(student)

    student_list = get_students_titlecase()
    
    student_name = input("Enter student name: ")
    student_id = input("Enter student ID:")

    add_student(student_name,student_id)
    print_students_titlecase()

```

## Nested Functions and Closures



## Opening,Reading, and Writing Files


## Yield


## Lambda Functions

