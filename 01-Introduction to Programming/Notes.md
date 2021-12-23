# Introduction to Programming
- Computers understand only 0 and 1
- Programming language is just a way to communicate with the computer
- Program is just bunch of instructions given to computer
- If computer just understands only 0's and 1's then it would be difficult to write big instructions , hence we have these programming languages which are human readable format
- Internally computer will translate the instructions to 0's and 1's 

# Types of languages
- Procedural : 
    - Specifies a series of well structured steps and procedures to compose a program
    - Contains a systematic order of statements, functions, loops and commands to complete a task
    - Order of statements are important to get the task done successfully
- Functional : 
    - Writing programs only in pure functions i.e. never modify variables but only create new ones as output
    - Used in situations where we have to perform lots of different operations on the same set of data like ML
    - Also follow First Class functions. 
- Object oriented :  
    - Revolves around objects
    - Code + Data = Object
    - Was developed to make things easy to create, debug, resuse and maintain software.
    - Classes are used to create custom data type
    - Class is just named grouped of properties and functions
    - Instance of a class is called an object


- Functions are just block of code which we can reuse again and again
- e.g.
```
a=10;
b=20;
c=b;
```
- Here we see we are assigning one variable to another variable , if this behavior is allowed for functions then it is called first class functions
- Many languages like Python, Java, C, C++, C#, JavaScript follow many types of paradigms mentioned
- One language is not restricted to just one type of paradigm
- Compilation: converting source code to machine code

# Another category of languages
- Static : 
    - Perform type checking at compile time
    - Errors will show at compile time
    - Declare data type before you use it
    - More control
- Dynamic : 
    - Perform type checking at runtime
    - Error might not show till program is run
    - No need to declare datatype of variables
    - Saves time in writing code but might give error at runtime

# Memory
- We have 2 types of memory
    1. Stack memory
    2. Heap memory

```
a=10;
```
- Here 'a' is known as reference variable
- '10' is known as object

1. Stack memory :
    - Variables/references are stored in stack.
    - Reference variable will be pointing to that object
2. Heap memory : 
    - Actual objects are stored in heap
    - All objects are in heap

- More than one reference can point to same object
- If any one of the refernce change the object value, it will be reflected for all the varaibles/references

# Garabage collection
- Sometimes there can be a scenario where the object loses all its references
- When garabage collection happens all the objects which do not have any references will be removed from memory
