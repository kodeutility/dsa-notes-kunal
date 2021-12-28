# Functions/ Methods in java

- Function inside a class is called method
- In JAVA all functions are inside a class hence JAVA has only methods
- Set of statements which will be used many times can be put inside a method and can be re-used

```
access_modifier return type name_of_method (parameters){
    // body of methods
    return statement;
}
```
- Any usage inside static variables/methods/class also have to be static
- We know main() method is static, so any method called inside main method directly also have to be of static type
- When function finishes execution after function call, it will have a value, usually it is of return type , if nothing is returned from the function , null is returned
- When return statement is reached function execution is over
- If we have specified a return type then we have to return same type value else we get compile time error

```java
public class Greeting{
    public static void main(String[] args){
        greeting();
    }

    static void greeting(){
        System.out.println("Hello");
    }
}
```
## Pass arguments for function

```java
public class Sum{
    public static void main(String[] args){
        int ans = sum(10,30);
        System.out.println(ans);
    }

    static int sum(int a, int b){
        return a+b;
    }
}
```

# Does this swap values?

```java
public class Swap{
    public static void main(String[] args){
        int a = 10;
        int b = 20;

        swap(a,b);
        System.out.println(a + " " + b); //10,20
    }

    // This does not swap the values
    static void swap(int a, int b){
        int temp=a;
        a=b;
        b=a;
    }
}
```

- In JAVA there is only pass by value/object , there is no pass by reference

```java
class Main {
  public static void main(String[] args) {
    int[] arr = {1,2,3,4,5};
    System.out.println(arr[0]); //1

    change(arr);
    System.out.println(arr[0]); //10

  }

  static void change(int[] b){
    b[0]=10;
  }
}
```

- Integer array arr is created and passed to the function
- Now inside change() method, variable **b** is alos now pointing to same integer array
- At this point both **arr** and **b** are pointing to same integer array
- any changes made by **b** will also get reflected by **arr**
- After making change change() method is destroyed and variable **b** is gone, but **arr** is still pointing to the integer array where change has occured.
- Hence printing the first value of integer array after function call reflects the changes in **arr**
- For Strings since they are immutable new String is created in Heap and it points to new object hence we don't see any change

```java
class Main {
  public static void main(String[] args) {
    String str1 = "Kiran";
    System.out.println(str1); //Kiran

    change(str1);
    System.out.println(str1); //Kiran

  }

  static void change(String str2){
    str2 = "Kunal";
  }
}
```

- **str1** points to string **Kiran** and it is passed to the change() method
- Now **str1** and **str2** both are poiting to same string object
- Now **str2** is assigned new string, since strings are immutable new string object is created and **str2** starts pointing to that, **str1** is still pointing to **Kiran** and **str2** is pointing to **Kunal**
- Once method call is over **str2** reference is destroyed and **Kunal** object do not have any reference
- **str1**  is still poiting to **Kiran**
- Hence before and after method call output of string is same
- For primitives (byte, short, int, long, float, double, char) values are passed, a copy is passed hence any changes made won't be affecting original values
- For objects reference value is passed, hence variable outside method call and variable inside method call both point to same object because both these variables has address value of the same object
- For primitives, variables store actual value like 10, 10.4, etc
- For objects, variables store address of objects in heap x234, x4442, etc. Hence when this value is passed local variable also starts poiting to same object as both have same object address

# Scoping
- Any variables created inside a particular block is available only inside that block
- We cannot access the variables created inside a method, outside the method

## Function scope
- Any variables defined inside a function including the parameters are only allowed to be accessed inside that function

## Block scope
- If variable is already initialized outside the block, we cannot initialize it again, but we are allowed to modify existing variables
- If we create new variables inside a block , we cannot access it outside the block, will remain in the block

```java
public static void main(String[] args){
    int a=10;
    int b=20;
    {   
        int a = 50; //invalid: can't initialize again
        a=78; //valid: allowed for changes
        int c = 70;
    }

    System.out.println(c); //invalid: no scope
}
```

## Loop scope
- If variable is already initialized outside for block, we cannot initialize it again, but we are allowed to modify existing variables
- If we create new variables inside a for block , we cannot access it outside the block, will remain in the block

```java
public static void main(String[] args){
    int a=10;
    
    for(int i=0;i<10;i++){
        int num=10;
        int a=90; //invalid: can't create new one
        a=40; //valid
    }
    int num=100; //valid

    System.out.println(i); //invalid: no scope
}
```

# Shadowing
- It is use of 2 variables with same name within the scope that overlaps
- The variable with higher level scope is hidden, lower level(inner level) variable will override the outer level variable, this is called shadowing

```java
public class Shadow{
    static int x=90; //will be shadowed by variable below
    public static void main(String[] args){
        System.out.println(x); //90;

        int x=40;
        System.out.println(x); //40;
        fun();
    }

    static void fun(){
        System.out.println(x); //90;
    }
}
```
- int x; is called declaration
- x=40; is called initialization
- Have to initialize it first and then use variables
- This does not work in methods, only with class variables

```java
public class Shadow{
    static int x=90; //will be shadowed by variable below
    public static void main(String[] args){
        System.out.println(x); //90;

        int x;
         System.out.println(x); //Error:Variable 'x' might not have been initialized
         // Scope will begin when the value is initialized
        x=40;
        System.out.println(x); //40;
        fun();
    }

    static void fun(){
        System.out.println(x); //90;
    }
}
```

# Var-args (variable length arguments)
- A method which takes variable number of arguments
- This is used when we do not know how many arguments we are giving
- We give 3 dots (int ...v), (String ...v), (char ...v),etc
- It will internally store it in an array
- We can have positional based argument and var args also, but positional have to be declared first and called in same way and later use var args while declaring and calling

```java
import java.util.Arrays;

public class VarArgs{
    public static void main(STring[] args){
        fun(2,3,4,5,6,8); // o/p: [2,3,4,5,6,8]
        fun(); // o/p: []

        multiple(2,3,"Kunal", "Rahul", "Kiran");
    }

    static void fun(int ...v){
        System.out.println(Arrays.toString(v));
        
    }

    static void multiple(int a, int b, String ...v){

    }
}
```

# Method overloading
- Multiple functions with same name and if parameters are different, either number of arguments or type of arguments
- At compile time it gets decided which overloaded methods to run
- If there is no function which match exactly (either 0 functions or ambiguity) then we get error, var args function is considered at last

```java
public class OverLoad{
    public static void main(String[] args){
        fun(43);
        fun("Kunal");
    }

    static void fun(int x){
        System.out.println(x);
    }

    static void fun(String x){
        System.out.println(x);
    }

}
```
# Questions
## Prime number

```java
import java.util.Scanner;

public class IsPrime{
    public static void main(String[] args){
        Scanner scn = new Scanner(System.in);
        int n = scn.nextInt();
        boolean ans = isPrime(n);
        System.out.println(ans);
    }

    static boolean isPrime(int n){
        if(n<=1){
            return false;
        }

        int c=2;
        while(c*c<=n){
            if(n%c==0){
                return false;
            }
            c++;
        }
        return true;
    }
}
```

## Armstrong numbers
- An Armstrong number is a positive m-digit number that is equal to the sum of the mth powers of their digits. 
- It is also known as pluperfect, or Plus Perfect, or Narcissistic number.
- Examples:
    - 1: 1<sup>1</sup> = 1
    - 2: 2<sup>1</sup> = 2
    - 3: 3<sup>1</sup> = 3
    - 153: 1<sup>3</sup> + 5<sup>3</sup> + 3<sup>3</sup> = 1 + 125+ 27 = 153
    - 125: 1<sup>3</sup> + 2<sup>3</sup> + 5<sup>3</sup> = 1 + 8 + 125 = 134 (Not an Armstrong Number)
    - 1634: 1<sup>4</sup> + 6<sup>4</sup> + 3<sup>4</sup> + 4<sup>4</sup> = 1 + 1296 + 81 + 256 = 1643

```java
// Only 3 digit armstrong numbers
static boolean isArmstrong(int n){
    int original = n;
    int sum=0;
    while(n>0){
        int rem = n%10;
        n/=10;
        sum+=rem*rem*rem;
    }
    return sum==original;
}
```