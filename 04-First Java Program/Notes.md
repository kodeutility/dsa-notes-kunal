# Java Program
- In JAVA evey file we write must have a class, which means every file itself is a class
- Filename and class name should be same if the class is public
- There can be only one public class in single java file but a single java file can contain many classes
- Convention(not a rule)
    - Words with capital letter is a class name
    - for variables, function names we use camelCase
    - Source code files go in **src** folder
    - .class file go in **out** folder
- **public** is a access modifier which means in below code, class can be accessed from anywhere (other classes, other files, other packages)
- From where our program starts is main() function, without main() our program won't run

Main.java

```java
public class Main{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```
- Convert our source code **Main.java** to Bytecode
> $ javac Main.java
- We use **javac** java compiler to compile our **.java** file to **.class** file which is byte code.
> $ java Main
- Now we use **java** command to run the **.class** file we created to execute java application

# Code explanation
- **public** : Means the class can be accessed from anywhere
- **class** : Named group of properties and functions
- **Main** : File name has to be same name as public class in the .java file
- **main** : Starting point of java program
- **static** : to run without creating object of its class
- **String[] args** : command line arguments. It's String array in this case.
- **System** : class which provide standard input, output, error facility
- **out** : it is a PrintStream object. Dafult value is command line

```java
public static final PrintStream out=null;
```
- **println** : PrintStream class has println() method. Also add new line after printing the contents
- **print** : Prints to standard output but do not add new line at the end

```java
public void println(String x){
    if(getClass() == PrintStream.class){
        writeln(String.valueOf(x));
    }else{
        synchronized (this){
            print(x);
            newLine();
        }
    }
}
```

- First JVM will look for **public static void main(String[] args)** to start execution of java program
- It is like entry point of java program
- If any mistake in this method signature then JVM throws error saying can't find main() method
- main() method is public so JVM can find it execute it
- JVM need not create a object of the class to run main() method
- Nothing is returned to JVM hence return type of main() method is void
- String[] args : whatever we give in command line , it will be stored as String array

Main.java

```java
public class Main{
    public static void main(String[] args){
        System.out.println(args[0]);
    }
}
```
> $ javac Main.java

> $ java Main "Kunal"

- By default java compiler will store the .class file in the same folder of .java file
- We can give **-d** flag to specify the location of .class file
> $ javac -d .. Main.java
- This is store .class file in previous folder

# Location of javac
- How do our computer know where is javac and java?
    - All commands we write in command prompt like python3, git, javac, java are actually executable files located on our computer

```
$ where javac
/usr/bin/javac
```
- Instead of writing full path to execute a file we just write name of the executable and this is recognized from the PATH and ENVIRONMENT varaibles

> $ echo $PATH

- PATH variable is just a list of all paths where the computer has to search if a particular executable is located. If the executable is not found in any of the mentioned list of paths we get error like 'javac' is not recognized.

# Package
- In simple terms it just means the folder in which our java file is present
- This is there is restrict access, using a access modifier we can allow what is accessible just to the files present in a particular folder
- It just provides layer of security
- Each dot represents a sub folder 
- E.g. com.kunal, com.rahul
- kunal and rahul are two folders present inside com folder

# Output
 - Java folks have provided few basic functions which we can use
 - Like take input and show output
 - Input and output related files are in **java.lang** package
 - This **java.lang** package is inherited by default, so all functionality in our java.lang package can be accessed directly

 # Input
 - For taking input we have **Scanner** class
 - **Scanner** class is available in **java.util** package
 - Scanner is just a simple text scanner which can parse primitive types and strings using regular expressions
 - We have to specify where we are taking input while creating a **Scanner** class

 ```java
 import java.util.Scanner;

 public class Main{
     public static void main(String[] args){
        Scanner scn = new Scanner(System.in);
        System.out.println(scn.nextInt());
     }
 }
 ```
 - Using **new** keyword we are creating object
 - **Scanner()** is called constructor, where we can pass values
 - **System.in** means standard input stream i.e Keyboard input

 ```java
 public static final InputStream in = null;
 ```
 - So this means when we ask for input we are saying it to read it from keyboard as we initialized with System.in
 - Every class in JAVA extends **Object** class
 - scn.next(); just takes forst word till it reach space
 - scn.nextLine(); reads entire line which also has spaces

 # Primitive DataType
 - Any data type which we cannot break further is called primitive data type
 - E.g byte, short, int, long, float, double, boolean, char

|Datatype|Size|Range|Default values|
|---|---|---|---|
|byte|1 byte|-128 to 127|0|
|short|2 bytes|-32,768 to 32,767|0|
|int|4 bytes|-2,147,483,648 to 2,147,483,647|0|
|long|8 bytes|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|0L|
|float|4 bytes|Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits|0.0f|
|double|8 bytes|Stores fractional numbers. Sufficient for storing 15 decimal digits|0.0d|
|char|2 bytes||'\u0000'|
|boolean|1 bit|true, false|false|

- By default, all integer type numbers are of type int, hence if we have to specify byte, short, long we have to postfix with 'b', 's', 'l'
- By default, all decimal type numbers are of type double, hence for float we have to prefix with 'f' 
- All primitive datatypes also have class
- Comments will be ignored by compiler

```java
// for single line comment

/* For
* multi-line
* comment
*/
```

```java
int a = 10;
int b = 1_000_000;
```
- **int** is the primitive datatype
- **a** is the identifier. Names given to variables/functions/classes/packages,etc
- **10** is the literal value
- We can use underscore for better readability for number, compiler later ignores it

# TypeCasting
- Lower datatype will automatically be converted to higher datatype, also known as implicit type casting
- If we want to conver higher datatype to lower datatype then we have to explicitly type cast it (Narrow conversion)
- byte->short->int->long->float->double
- char->int
- Character is also of type integer so it gets casted to int
- Conditions for implicit casting
    - Two types must be compatible
    - Destination type should be greater than the source type
- Below code explains how to do explicit type casting

```java
int num = (int) (67.56f);
```
- It finds highest level of datatype and convert all below datatypes 

# Automatic type promotion in expressions

```java
int a=257;
byte b = (byte) (a);
System.out.print(b); //1
```
- Even after casting here we cannot store 257 in byte variable, in this case result is remainder of max value and given value
- 257%256 = 1

```java
byte a = 40;
byte b = 50;
byte c = 100;
int d = a * b / c;
```
- Here because a * b exceeds capacity of byte varaible , a and b are promoted to integer to perform calculation of expression

```java
byte b = 50;
b = b * 2; //error
```
- This throws error because b * 2 , 2 is integer by default and b is also promoted to int to perform calculation and result is now in int but b is of type byte hence we have to explicitly type cast else we get error

# Character
 - JAVA uses UNICODE values so we can print/ use many languages in java

```java
System.out.println("नमस्ते");
```
# Summary

```java
byte b = 42;
char c = 'a';
short s = 1024;
int i = 50000;
float f = 6.67f;
double d = 0.123;
double result = (f*b) + (i/c) - (d-s);
System.out.println((f*b) + " " + (i/c) + " " + (d-s)); //238.14 515 -1023.8766
System.out.println(result); //1777.016614684376
```
- f*b : float * byte -> converted to float
- i/c : int / char -> converted to integer
- d-s : double-short -> converted to double
- (f*b) + (i/c) : float + integer -> converted to float
- ((f*b) + (i/c)) - (d-s) : float - double -> converted to double

# Conditions

```java
int salary = 15000;
if(salary>10000){
    salary += 2000;
}else if(salary>5000){
    salary += 1500;
}else{
    salary += 1000;
}
```

# Loops
##Syntax

```java
// for loop
for(initialization;condition;increment/decrement){
    //body
}

// while loop
while(condition){
    //body
}

// do-while loop
do{
    //body
}while(condition);
```
## Examples

```java
// for loop
for(int i=0; i<10; i++){
    System.out.print(i);
}

// while loop
int j=0;
while(j<10){
    System.out.println(j);
    j++;
}

 do-while loop
int k=0;
do{
    System.out.println(k);
    k++;
}while(k<10);
```
# Examples
## Find the largest of the 3 numbers

```java
int a = scn.nextInt();
int b = scn.nextInt();
int c = scn.nextInt();

int max = a;
if(b>max){
    max=b;
}else if(c>max){
    max=c;
}

System.out.println(max);

//OR

int maxValue = Math.max(c,Math.max(a,b));
System.out.println(maxValue);
```

## Alphabet case check
- Check first character of the given word.
- trim() :  remove extra spaces before and after a word
- charAt(index) : extracts character from String at given index

```java
Scanner scn = new Scanner(System.in);
char ch = scn.next().trim().charAt(0);

if(ch >= 'a' && ch<='z'){
    System.out.println("lower case");
}else if(ch >= 'A' && ch<='Z'){
    System.out.println("upper case");
}

```

## Fibonacci Sequence
- Find nth fibonacci number

```java
Scanner scn = new Scanner(System.in);
int n = scn.nextInt();
int a = 0;
int b = 1;

int count = 2;

while(count<=n){
    int temp = b;
    b = b + a;
    a = temp;
    count++;
}

System.out.println(b)
```

## Count occurances
- Check number of occurances for given number
- Whenever we are going to check for individual number we get obtain it by taking remainder after dividing number by 10
- lastDigit = n%10
- reducedNumber = n/10

```java
int n=345354;

int count=0;
while(n>0){
    int rem = n%10;
    if(rem==5){
        count++;
    }
    n=n/10;
}

System.out.println(count);
```

## Reverse a number

```java
int num=23423434;
int ans=0;
while(num>0){
    int rem=num%10;
    num/=10;
    ans = ans *10 +rem;
}

System.out.println(ans);
```
## Calculator
- Take input from user till user does not press X or x

```java
import java.util.Scanner;

public class Calculator{
    public static void main(String[] args){
        Scanner scn = new Scanner(System.in);
        int ans = 0;

        while(true){
            char op = scn.next().trim().charAt(0);
            if(op=='+' || op=='-' || op=='*' || op=='/' || op=='%'){
                int num1=scn.nextInt();
                int num2=scn.nextInt();

                if(op=='+'){
                    ans=num1+num2;
                }else if(op=='-'){
                    ans=num1-num2;
                }else if(op=='*'){
                    ans=num1*num2;
                }else if(op=='/'){
                    if(num2!=0){
                        ans=num1/num2;
                    }
                }else if(op=='%'){
                    ans=num1%num2;
                }

            }else if(op=='x' || op=='X'){
                break;
            }else{
                System.out.println("Invalid operation");
            }
            System.out.println(ans);
        }
    }
}
```

# Switch
- If we check for string value do not use == instead use str1.equals(str2)

```java
String a="Kunal";
String b="Kunal";
System.out.println(a==b); //true
```
- Here only one "Kunal" object is created and both 'a' and 'b' are pointing to same object 
- == check if both references are pointing to same object, hence we get true when we do a==b
- To check the contents of string use .equals()

```java
//Switch syntax
switch(expression){
    //cases
    case one: //do something
            break;
    case two: //do something
            break;
    default: //do something
            break;
}
```
- In switch cases we can jump to various cases based on the expression
- cases have to be the same type as expression, must be constant or literal
- duplicate case values are not allowed
- break is use to terminate the case
- if break is not used it will continue to next case
- default will execute when none of the above case does
- default can be written at any position, use break after it, else if default case is at beginning and no break statement is used, fall through will happen
- in if-else every condition is checked, in switch case , it directly jumps to the case, it does not check every case, that is the advantage

```java
Scanner scn = new Scanne(System.in);
String fruit = scn.next();

switch(fruit){
    case "mango":
        System.out.println("King");
        break;
    case "apple":
        System.out.println("red fruit");
        break;
    case "orange":
        System.out.println("also a color");
        break;
    case "grapes":
        System.out.println("bunch of fruit");
        break;
    default:
        System.out.println("not a fruit");
        break;
}

### Newer syntax
- break need not be specified, it is there automatically
- Use {} if more than one statement

```java
switch(fruit){
    case "mango" -> {
        System.out.println("King");
    }
    case "apple" -> System.out.println("red fruit");
    case "orange" -> System.out.println("also a color");
    case "grapes" -> System.out.println("bunch of fruit");
    default -> System.out.println("not a fruit");
}
```

### Find weekday or weekend (old way)

```java
switch(day){
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        System.out.println("Weekday");
        break;
    case 6:
    case 7:
        System.out.println("Weekend");
        break;
    default:
        System.out.println("Invalid");
        break;
}
```
### Find weekday or weekend (new way)

```java
switch(day){
    case 1,2,3,4,5 -> System.out.println("Weekday");
    case 6,7 -> System.out.println("Weekend");
    default -> System.out.println("Invalid");
}
```

## Nested switch case (old way)

```java
Scanner scn = new Scanner(System.in);
int empID = scn.nextInt();
String department = scn.next();

switch(empID){
    case 1:
        System.out.println("Kunal");
        break;
    case 2:
        System.out.println("Rahul");
        break;
    case 3:
        switch(department){
            case "IT":
                System.out.println("IT dept");
                break;
            case "Management":
                System.out.println("Management dept");
                break;
            default:
                System.out.println("No dept");
                break;
        }
    default:
        System.out.println("Invalid empID");
        break;
}
```

## Nested switch case (new way)
- There should be break statement for every case then only we can use new syntax

```java
Scanner scn = new Scanner(System.in);
int empID = scn.nextInt();
String department = scn.next();

switch(empID){
    case 1 -> System.out.println("Kunal");
    case 2 -> System.out.println("Rahul");
    case 3 ->{
        switch(department){
            case "IT" -> System.out.println("IT dept");
            case "Management" -> System.out.println("Management dept");
            default -> System.out.println("No dept");
        }
    }
    default -> System.out.println("Invalid empID");
}
```