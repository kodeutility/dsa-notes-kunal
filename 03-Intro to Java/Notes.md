# Introduction to JAVA
- Machine only understand 0's and 1's
- We cannot write application in 0's and 1's
- Hence we use programming language to write our commands /application in human readable format
- JAVA is one of these programming language
- We write our source code in **.java** file
- For C++ we have source code in **.cpp** file and we compile it, which turns our human readable source code into machine code which is 0's and 1's. Compilation of cpp file will happen for entire file

# How JAVA code executes
- .java file(human readable) ---compile(entire file)--->.class file(byte code) ---interpreter(line by line)--->Machine code(0's and 1's)
- In JAVA entire human readable source code is converted into byte code by java compiler, note this is not machine code.
- Byte code is like a language of JAVA, it will not directly run on a system
- To run byte code we need JVM(Java Virtual Machine) program.
- JVM acts as interpreter and interprets byte code line by line and generate machine code.
- This architecture of creating intermediate byte code and interpreting using platform specific JVM to execute make JAVA platform independent language
- WORA : Write once Run anywhere

# More about platform independence
- It means byte code can run on all operating systems
- We need to convert source code to machine code so computer can understand
- Compiler helps in doing this is by turning it into executable code
- This executable code is a set of instructions for the computer
- After compiling C/C++ code we get .exe file which is platform dependent
- In JAVA we get bytecode, JVM converts this into machine code
- JAVA is platform independent but JVM is platform dependent

![](img-01.png)

- JDK (Java Development Kit): JRE + Development tools
- JRE (Java Runtime Environment): JVM + Library classes
- JVM (Java Virtual Machine): This executes byte code line by line
- JIT (Just in Time) compiler

# JDK (Java Development Kit)
- Provides environment to develop and run java program
- Set of files which include
    - development tools - to provide an environment to develop your program
    - JRE : to execute your program
    - javac : java compiler
    - jar : archiver
    - javadoc : docs generator
    - interpreter/loader

# JRE (Java Runtime Environment)
- It is an installation package that provides environment to only run the program
- It consists of:
    1. Deployment technologies
    2. User interface toolkits
    3. Integration libraries
    4. Base libraries
    5. JVM
- After we get the .class file, next things happen at runtime
    1. class loader loads all classes needed to execute the program
    2. JVM sends code to Byte code verifier to check the format of code

![](img-02.png)

# Class Loader (How JVM works)
- **Loading** :
    - reads .class file and generate binary data
    - an object of this class is created in heap
- **Linking** : 
    1. JVM verifies the .class file
    2. allocates memory for class variables and default values
    3. replace symbolic references from the type with direct references
- **Initialization** : 
    - all static variables are assigned with their values defined in the code and static block
    - Static variables do not depend on the objects of the classes
- JVM contains the Stack and Heap memory allocations
- Stack is where we have function calls and reference variables
- Heap is where we have objects

# JVM Execution
- Interpreter
    - Line by line execution
- JIT
    - when one method is called many times, it will interpret again and again
    - for these repeated methods JIT compiler provides direct machine code so re-interpretation is not required which makes exection faster

# Flow
- Java Source Code (.java file) -> JDK (javac) -> ByteCode (.class file) -> JVM (converts to executable code)-> JRE (provides environment to execute machine code)






