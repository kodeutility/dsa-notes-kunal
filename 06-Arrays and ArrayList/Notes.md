# Arrays
- Arrays datastructure is useful when we have to store lot of same type of values
- Array is collection of same datatype, collection of integers, collection of primitives, collection of objects

```java
// syntax 1D array
datatype[] variable_name = new datatype[size];

//examples
int[] roll_nos = new int[10];
int[] roll_nos_2 = {1,2,3,4,5};
``` 
---

```java
//invalid syntax

int[] arr; 
arr = {1,2,3,4,5}; //Array constant can only be used in initializers
//OR
int[] arr = new int[5];
arr = {1,2,3,4,5};
//OR
int[] arr = new int[];
//OR
int[] arr = new int[5]{1,2,3,4,5}; //array creation with both dimension expression and initialization is illegal
//OR square brackets
[]int arr;

```
---
```java
//Valid syntax
//square brakets can be moved around
int[] arr;
int []arr;
int  []   arr;
int arr  [];

int[] arr = new int[]{1,2,3,4,5};
//OR
int[] arr = {1,2,3,4,5};
//OR
int[] arr = new int[5];
arr[0]=1;
arr[1]=2;
arr[2]=3;
arr[3]=4;
arr[4]=5;
//OR
int[] arr; 
arr = new int[5];
arr[0]=1;
arr[1]=2;
arr[2]=3;
arr[3]=4;
arr[4]=5;
//OR
int[] arr; 
arr = new int[]{1,2,3,4,5};
```

- This means roll_nos is a reference variable pointing to a array of integer values object
- **int[] roll_nos** is declaration, the reference variable get defined in the stack
    - **int[]** : datatype
    - **roll_nos** : reference variable
- **new int[10]** is initialization where the array object of size 10 is actually created in heap memory and the reference variable starts poiting to it
- **new** keyword in JAVA is used to create objects
- Either we have to mention the size of array or have to declare the array directly
- **int[] arr** : Happens at compile time
- **new int[5]** : Happens at runtime, also called Dynamic memory allocation because memory gets allocated at runtime
- In C/C++ array is represented as contiguous block of memory, if array size is 10, then ten continous block of memory in RAM is allocated
- In JAVA there are no pointers, so it totally depends on the JVM whether it is going to be continous or not
    - Array objects are in heap
    - In Java Language Specification it is mentioned that memory allocation for Heap objects are **not continous**
    - Heap is the runtime data area from which the memory for which all the classes and instances for arrays is allocated
    - Since memory for arrays objects are created during runtime, memory is created in heap, but in heap there is no guarantee memory assigned in heap is continous and memory allocation depends on JVM, we can conclude that the memory assigned to Arrays in JAVA may/may not be continous, even though array data structure says it is continous block of data
- Arrays are 0 based indexed
    - First element is at 0th index
    - Second element is at 1st index
    - Third element is at 2nd index,etc
- Default value of integer array is 0
- Objects will have **null** as it's default value
- **null** is not a keyword, but it is like special literal, and can't be used to create a type of null
- **null** can only be assigned to object type and not primitive datatypes, it is like special literal for default value of non-primitive datatypes

```java
null a=null; //invalid
int a = null; //invalid
```
- For primitive datatypes values are stored in stack memory
- For non-primitive datatypes values(objects) are stored in heap memory and since objects are created at runtime the default value for all reference variables will be null which means the reference variable is not pointing to any object

# Internal memory level working of arrays
- Consider String arrays **String[] str = new String[5];**
- **str** reference variable will be stored in stack memory, array object will be created at runtime in heap memory
- The String array will have 5 elements [ _ , _ , _ , _ , _ ]
- Array itself is a object and each element of array is also any object, each of these String object will be stored at different part of heap memory
- Since we have not initialized String array (str[0], str[1], str[2], str[3], str[4] are reference variables) all reference variables will have **null** as it's value
- Hence String array when declared will have nulls for it's array elements [ null , null , null , null , null ]. These are just collection of reference variables, if no value then it is null
- **.length** attribute will give length of the array

```java
for(int i=0; i<arr.length; i++){
    arr[i] = scn.nextInt();
}

for(int i=0; i<arr.length; i++){
    System.out.println(arr[i]);
}

// enhanced for each loop
// We directly get the element which we can use
// It is iterated from first to last elements of array
for(int num : arr){
    System.out.println(num);
}

//Arrays class also has Arrays.toString() to print entire array
System.out.println(Arrays.toString(arr));
```

- If we try to access elements which is out of given range of indices, we get **ArrayIndexOutOfBounds** Exception

# Passing In Functions
- In JAVA it is pass by value, the address of the object is passed to function, hence the new local variable of function will also now have the same object address and point to same object

```java
public static void main(String[] args){
    int[] nums = {3,4,5,12};
    System.out.println(Arrays.toString(nums)); // [3,4,5,12]
    change(nums);
    System.out.println(Arrays.toString(nums)); // [99,4,5,12]
}

static void change(int[] arr){
    arr[0] = 99;
}
```

# 2D Arrays
- Rows and columns
- Rows must be specifed, columns are optional

```java
int[][] arr = new int[3][]; //valid
int[]  [] arr = new int[3][]; //valid
int[]  []arr = new int[3][]; //valid
int[] arr[] = new int[3][]; //valid
int[][] arr = {
    {1,2,3},
    {4,5,6},
    {7,8,9}
}; //valid

int[][] arr = new int[][3]; //invalid, rows is mandatory
```

# Internal working of 2D arrays
- In C/C++ 2D arrays are also contiguous allocation of memory
- 2D arrays is like arrays of arrays
- The column can vary and need not be same 
- We can access using row value and column value to access and modify
- arr[0] will just give 1st row, arr[0][0] will give first element of 1st row
- arr.length will give length of arrays

```java
int[][] arr = {
    {1,2,3},
    {4,5},
    {6,7,8,9}
}; //valid

// Take input
for(int row=0;row<arr.length;row++){
    for(int col=0;col<arr[row].length;col++){
        arr[row][col]=scn.nextInt();
    }
}

// Output
for(int row=0;row<arr.length;row++){
    for(int col=0;col<arr[row].length;col++){
        System.out.print(arr[row][col] + " ");
    }
    System.out.println
}
// OR
for(int row=0;row<arr.length;row++){
    System.out.println(Arrays.toString(arr[row]));
}

// For each loop
// Every single element is itself an array
for(int[] a: arr){
    for(int b:a){
        System.out.print(b);
    }
}
```
# ArrayList
- ArrayList is used when we do not know the size of the array we are going to create
- Similar to Vectors in C++
- Mentioning data type while creating object is optional(on left and right side)
- It is slower than traditional arrays
- We can also pass **initialCapacity** in the constructor while creating ArrayList
- We can only specify class type, we cannot specify primitive datatypes instead mention wrapper classes like Integer than int

```java
import java.util.ArrayList;

public class ArrayListExample{
    public static void main(String[] args){
        ArrayList<Integer> arr = new ArrayList<>();
        // OR
        ArrayList<Integer> arr = new ArrayList<Integer>();
        // OR
        ArrayList<Integer> arr = new ArrayList<Integer>(10);
        // OR
        ArrayList<> arr = new ArrayList<>();// valid but Bad practice
        // OR
        ArrayList<int> arr = new ArrayList<int>(); //invalid have to give wrapper class for primitives

        arr.add(1);
        arr.add(2);
        arr.add(3);
        arr.add(4);

        // Output: internally it calls .toString() method
        System.out.println(arr); // [1,2,3,4]
    }
}
```

# ArrayList Methods


# Internal working of ArrayList
- Size is fixed internally
- When ArrayList fill to certain amount, new ArrayList is created with maybe double the size, old elements are copied to new ArrayList and new element to added in new ArrayList
- Old ArrayList is deleted

# ArrayList of ArrayList
- Multi Dimensional ArrayList

```java
ArrayList<ArrayList<Integer>> arr = new ArrayList<>();

// Initialization must be done before accessing else we get error
for(int i=0;i<3;i++){
    arr.add(new ArrayList<>());
}

for(int i=0;i<3;i++){
    for(int j=0;j<3;j++){
        arr.get(i).add(scn.nextInt());
    }
}
```

# Example
## Swap values in Array

```java
import java.util.Arrays;

public class SwapArray{
    public static void main(String[] args){
        int[] arr = {1,2,3,4,5};
        swap(arr, 1,3);
        System.out.println(Arrays.toString(arr));
    }
    static void swap(int[] arr, int index1, int index2){
        int temp = arr[index1];
        arr[index1]=arr[index2];
        arr[index2]=temp;
    }
}
```

## Maximum Value of Array
```java
public class MaxValueInArray{
    public static void main(String[] args){
        int[] arr = {1,2,3,4,5};
        int max_value = max(arr);
        System.out.println(max_value);
    }
    static int max(int[] arr){
        if(arr.length<1)
            return -1;
        int max_value = arr[0];
        for(int x:arr){
            if(x>max_value){
                max_value=x;
            }
        }
        return max_value;
    }
}
```

## Reverse Array
```java
import java.util.Arrays;

public class Reverse{
    public static void main(String[] args){
        int[] arr = {1,2,3,4,5};
        reverse(arr);
        System.out.println(Arrays.toString(arr));
    }
    static void reverse(int[] arr){
        int start=0;
        int end=arr.length-1;

        while(start<end){
            int temp=arr[start];
            arr[start]=arr[end];
            arr[end]=temp;
            start++;
            end--;
        }
    }
}
```