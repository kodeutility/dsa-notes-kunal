# Searching
- Finding a value
- Types of search
    1. Linear Search - Start search from 1st element till u find
    2. Binary Search

# Questions
## Find a element in an array
- We can do a linear search and return the index of the array where we found the element
- If no value found in the array we can return -1 as the index
- Time Complexity : 
    - Best : O(1) constant time
    - Worst : O(N) N is size of array
- Linear search takes N comparisons in worst case

```java
static int linearSearch(int[] arr, int target){
    if(arr.length==0){
        return -1;
    }

    for(int i=0; i<arr.length;i++){
        int element = arr[i];
        if(element==target){
            return i;
        }
    }
    return -1;
}
```
## Find a character in String
```java
public static void main(String[] args){
    String name = "Kunal";
    char target = 'u';
    System.out.println(search(name, target));
}

static boolean(String str, char target){
    if(str.length()==0){
        return false;
    }
    for(char c:str.toCharArray()){
        if(c==target){
            return true;
        }
    }
    return false;
}
```

## Even Digits
- Given an array **nums** of integers, return how many of them contain an even number of digits
```
Input: nums = [12,345,2,6,7896]
Output: 2
Explanation: 
12 contains 2 digits (even number of digits). 
345 contains 3 digits (odd number of digits). 
2 contains 1 digit (odd number of digits). 
6 contains 1 digit (odd number of digits). 
7896 contains 4 digits (even number of digits). 
Therefore only 12 and 7896 contain an even number of digits.

Input: nums = [555,901,482,1771]
Output: 1 
Explanation: 
Only 1771 contains an even number of digits.
```
### Brute Force
- iterate over an array
- count number of digits or convert to string and take length()
- if even increase global count
- return results

```java
static int findNumbers(int[] nums){
    int count=0;
    for(int num:nums){
        if(even(num)){
            count++;
        }
    }
    return count;
}

static boolean even(int num){
    int numberOfDigits = digits(num);
    return numberOfDigits%2==0;
}

static int digits(int num){
    int count=0;
    if(num==0){
        return 1;
    }
    if(num<0){
        num*=-1;
    }
    while(num>0){
        count++;
        num/=10;
    }
    return count;
}
```
### Optimization
- count number of digits in constant time
- (int)(Math.log10(number)) + 1
- Log to base 10 of the number +1 gives number of digits in constant time
```java
static int findNumbers(int[] nums){
    int count=0;
    for(int num:nums){
        if(even(num)){
            count++;
        }
    }
    return count;
}

static boolean even(int num){
    int numberOfDigits = digits(num);
    return numberOfDigits%2==0;
}


// Optimization
static int digits(int num){
    if(num<0){
        num*=-1;
    }
    return (int)(Math.log10(num)) +1;
}
```

## Richest Customer Wealth

- You are given an m x n integer grid accounts where accounts[i][j] is the amount of money the ith customer has in the jth bank. 
- Return the wealth that the richest customer has.
- A customer's wealth is the amount of money they have in all their bank accounts. 
- The richest customer is the customer that has the maximum wealth.
```
Input: accounts = [[1,2,3],[3,2,1]]
Output: 6
Explanation:
1st customer has wealth = 1 + 2 + 3 = 6
2nd customer has wealth = 3 + 2 + 1 = 6
Both customers are considered the richest with a wealth of 6 each, so return 6.

Input: accounts = [[1,5],[7,3],[3,5]]
Output: 10
Explanation: 
1st customer has wealth = 6
2nd customer has wealth = 10 
3rd customer has wealth = 8
The 2nd customer is the richest with a wealth of 10.

Input: accounts = [[2,8,7],[7,1,3],[1,9,5]]
Output: 17

Constraints:
m == accounts.length
n == accounts[i].length
1 <= m, n <= 50
1 <= accounts[i][j] <= 100
```
```java
public int maximumWealth(int[][] accounts){
    int max_wealth = 0;

    for(int i=0;i<accounts.length;i++){
        int row_sum = 0;
        for(int j=0;j<accounts[i].length;j++){
            row_sum += accounts[i][j];
        }
        if(row_sum>max_wealth){
            max_wealth=row_sum;
        }
    }
    return max_wealth;
}
```

# Binary Search
- Used for sorted arrays
- Observation (ascending order)
    - Pick a element
    - All elements to left of the element will be smaller
    - All elements to right of the element will be greater
- Algorithm
    - Find middle element of array
    - Check if target is middle element
        - Yes: Found
        - No: 
            - Continue same search in right side of the array if target is greater than middle element (start=mid+1)
            - Continue same search in left side of the array if target is lesser than middle element (end=mid-1)
    - If start > end: element does not exist
- We can see in every iteration the search space is getting divided by 2

- Time Complexity : 
    - Best : O(1) constant time
    - Worst : O(logN) N is size of array

- Number of elements in search space
    - N, N/2, N/4, N/8, N/16, ....., 1
    - N/2<sup>0</sup>, N/2<sup>1</sup>, N/2<sup>2</sup>, N/2<sup>3</sup>, N/2<sup>4</sup>, ....., N/2<sup>k</sup>
    - Consider we take 'k' steps to reach N to 1.
        - For 0th step: N/2<sup>0</sup>
        - For 1st step: N/2<sup>1</sup>
        - For 2nd step: N/2<sup>2</sup>
        - For 3rd step: N/2<sup>3</sup>
        - For kth step: N/2<sup>k</sup>
    - At kth level we know value of N/2<sup>k</sup> is 1
    - Hence, 
        - 1=N/2<sup>k</sup>
        - N=2<sup>k</sup>
        - Log base 2 on both sides
        - log(N) = log(2<sup>k</sup>)
        - log(N) = klog(2)
        - We know log2 to base 2 = 1
        - log(N) = k or k = log(n) to base 2
    - For k number of comparisons we take logN time

### Issue with finding middle element
- If we do (start+end)/2 , it may so happen that values of start and end are really big and sum of start and end can cross the limit of integer capacity
- Hence we can do [start + (end-start)/2]. Take the offset from start.

# Code for BinarySearch
```java
static int binarySearch(int[] arr, int target){
    int start = 0;
    int end = arr.length -1;

    while(start<=end){
        int mid= start + (end-start)/2;

        if(target==arr[mid]){
            return mid;
        }else if(target>arr[mid]){
            start = mid+1;
        }else if(target<arr[mid]){
            end = mid-1;
        }
    }

    return -1;
}
```

# Order-Agnostic Binary search
- First we have to find out if the array is in ascending or descending
- How?
    - Just compare 2 elements, if left number is smaller than right number then ascending else descending
    - But what if elements are like [3,3,3,3,3,5,6,7,8,9]
    - Instead of taking any 2 numbers best case would be to pick first and last number
        - If first number < last number : ascending
        - If first number > last number : descending
        - If first number == last number : same elements in entire arrays

# Code for Order-Agnostic BinarySearch
```java
static int binarySearch(int[] arr, int target){
    int start = 0;
    int end = arr.length -1;

    boolean isAsc = arr[start]<arr[end];

    while(start<=end){
        int mid= start + (end-start)/2;

        if(target==arr[mid])
            return mid;
        
        if(isAsc){
            if(target>arr[mid]){
                start = mid+1;
            }else{
                end = mid-1;
            }
        }else{
            if(target<arr[mid]){
                start = mid+1;
            }else{
                end = mid-1;
            }
        }
    }

    return -1;
}
```
# Binary Search Interview Questions - Google, Facebook, Amazon
- When to try Binary Search?
    - When given array is sorted, try binary search
    - Required to get one particular answer and are **working with continous sequence of numbers** to get the answer. E.g. Square root of a number
    - When we have assumed the range of numbers needed are sorted

# Ceiling of a Number
- Given a sorted array [2,3,5,9,14,16,18] and given a target = 15.
- Find Ceiling of given target
- Ceiling of a given target number is smallest number in array which is greater or equal to given number
- E.g:
    - target=14 , answer=14
    - target=15 , answer=16

### Observation
- So if given target is 15, we have to search in 16,18 of given array
- We eliminate numbers which are smaller than 15
- First small number from the reduced search space is the answer
- If target is 9 , eleminate all numbers less than 9, so we search smallest in reduced space 9,14,16,18
- First smallest in reduced space is 9, answer is 9
- Since array is sorted, and we eliminate search space we can try binary search
- In Binary search if we find the element we were returning the index, else if not found we would return -1
- In this modified search for ceiling, if we don't find given number then we return next index from where we stopped binary search

### Intiution
- In Binary search we take start and end pointer, we are saying the answer if lying between start and end inclusive
- Always **Start** ---- **target** --- **end**
- Breaking condition of binary search is suppose if start > end
```
Loop continous and arrive at a point where start=mid=end, at this point either we have reached the element or it is a number just less than the target.
```
- At this point if number is found we return it else we increment start=mid+1, which represents a number just greater than target 
- **end** ---- **target** --- **start**
```
If we have to find a number which is ceiling of given target, we either get answer at start=mid=end, where mid is answer and return it, else once loop ends due to start pointer becoming greater than end pointer, start pointer is poiting to answer a number just greater than given target
```

### Solution
- Return start pointer if element not found in binary search algorithm

# Code for Ceiling of given Number
```java
static int binarySearch(int[] arr, int target){
    // if target is greater than the greatest number in the array
    if(target >arr[arr.length-1]){
        return -1;
    }
    int start = 0;
    int end = arr.length -1;

    while(start<=end){
        int mid= start + (end-start)/2;

        if(target==arr[mid]){
            return mid;
        }else if(target>arr[mid]){
            start = mid+1;
        }else if(target<arr[mid]){
            end = mid-1;
        }
    }

    return start;
}
```
- Time Complexity : O(logN)
- Space Complexity : O(1)

# Floor of a Number
- Given a sorted array [2,3,5,9,14,16,18] and given a target = 15.
- Find biggest number smaller than or equal to target number, the floor of given target
- E.g:
    - target=14 , answer=14
    - target=15 , answer=14

### Observation
- Now we know when we are at last search space , start=mid=end which will either be the target and number just less than target
- So if not found, now start pointer will go ahead of end pointer
```
The element pointing by end pointer will be the biggest number smaller than target number
```
### Solution
- Return end pointer if element not found in binary search algorithm

# Code for Floor of given Number
```java
static int binarySearch(int[] arr, int target){
    // if target is smallest than the smallest number in the array
    // returning end will take care of this
    int start = 0;
    int end = arr.length -1;

    while(start<=end){
        int mid= start + (end-start)/2;

        if(target==arr[mid]){
            return mid;
        }else if(target>arr[mid]){
            start = mid+1;
        }else if(target<arr[mid]){
            end = mid-1;
        }
    }

    return end;
}
```
- Time Complexity : O(logN)
- Space Complexity : O(1)

# Find Smallest Letter Greater Than Target
- Given a characters array letters that is sorted in non-decreasing order and a character target, return the smallest character in the array that is larger than target.
- Note that the letters wrap around.
- For example, if target == 'z' and letters == ['a', 'b'], the answer is 'a'.
```
Input: letters = ["c","f","j"], target = "a"
Output: "c"

Input: letters = ["c","f","j"], target = "c"
Output: "f"

Input: letters = ["c","f","j"], target = "d"
Output: "f"

Constraints:
- 2 <= letters.length <= 104
- letters[i] is a lowercase English letter.
- letters is sorted in non-decreasing order.
- letters contains at least two different characters.
- target is a lowercase English letter.
```

- Since here it is strictly greater than given target, hence we don't need the target==mid condition
- Wrap around mean if there are no characters available in given sorted array which is greater than given target, then return 0th index

```java
class Solution {
    public char nextGreatestLetter(char[] arr, char target) {
        // if target is greater than the greatest number in the array
        if(target >=arr[arr.length-1]){
            return arr[0];
        }
        int start = 0;
        int end = arr.length -1;

        while(start<=end){
            int mid= start + (end-start)/2;

            if(target<arr[mid]){
                end = mid-1;
            }else{
                start = mid+1;
            }
        }

        return arr[start];
    }
}
```
# Find First and Last Position of Element in Sorted Array
- Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.
- If target is not found in the array, return [-1, -1].
- You must write an algorithm with O(log n) runtime complexity.
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]

Input: nums = [], target = 0
Output: [-1,-1]

Constraints:
0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums is a non-decreasing array.
-109 <= target <= 109
```
- [5,7,7,7,7,8,8,10] target=7
- First step of binary search we reach 7th for mid element, but  we need first and last occurance
- For first occurance even though mid is 7 there is possibility that there might be 7 on left side of mid, now again use binary search to find if 7 exists and repeat i.e. when target==mid we do end=mid-1
- For last occurance even though mid is 7 there is possibility that there might be 7 on right side of mid, now again use binary search to find if 7 exists and repeat i.e. when target==mid we do start=mid+1
```java
class Solution {
    public int[] searchRange(int[] arr, int target) {
        int start = 0;
        int end = arr.length -1;
        int lower=Integer.MAX_VALUE;
        int higher=Integer.MIN_VALUE;

        while(start<=end){
            int mid= start + (end-start)/2;

            if(target==arr[mid]){
                // store possible answer and continue search on left side of mid
                if(mid<lower){
                    lower=mid;
                }
                end = mid-1;
            }else if(target>arr[mid]){
                start = mid+1;
            }else if(target<arr[mid]){
                end = mid-1;
            }
        }
        // Reset start and end values
        start = 0;
        end = arr.length -1;
        
        while(start<=end){
            int mid= start + (end-start)/2;

            if(target==arr[mid]){
                // store possible answer and continue search on right side of mid
                if(mid>higher){
                    higher=mid;
                }
                start = mid+1;
            }else if(target>arr[mid]){
                start = mid+1;
            }else if(target<arr[mid]){
                end = mid-1;
            }
        }
        
        if(lower==Integer.MAX_VALUE){
            return new int[]{-1,-1};
        }

        return new int[]{lower,higher};
    }
}
```
# Find position of an element in a sorted array of infinite numbers
- Suppose you have a sorted array of infinite numbers, how would you search an element in the array?
- Source: Amazon Interview Experience. 
- Since array is sorted, the first thing clicks into mind is binary search, but the problem here is that we don’t know size of array.
- Infinite array means we cannot use the length attribute of array
- If the array is infinite, that means we don’t have proper bounds to apply binary search. So in order to find position of key, first we find bounds and then apply binary search algorithm.
- Since it is infinite array we move in chunks, we can take start index =0 and end index= 10, if number within this range i.e. arr[10] > target
- If not in range then start=end+1, end=start+10 and continue the process till we find a range where we know our target lies between the range and then apply binary search
- How can we optimize the search window?
    - we can do this by increasing the window size exponentially
- Reverse logic
    - In binary search we take full length of array and reduce by half and half till we just have 1 element for comparison
    - No we can search from window size of 1 and double it every iteration till be find our search window which should take logN time complexity to find our search window
    - Once we find our search window, then we apply binary search and find the target in logN time complexity

```java
public class InfiniteArray {
    public static void main(String[] args) {
        int[] arr = {3, 5, 7, 9, 10, 90,
                100, 130, 140, 160, 170};
        int target = 10;
        System.out.println(ans(arr, target));
    }
    static int ans(int[] arr, int target) {
        // first find the range
        // first start with a box of size 2
        int start = 0;
        int end = 1;

        // condition for the target to lie in the range
        while (target > arr[end]) {
            int temp = end + 1; // this is my new start
            // double the box value
            // end = previous end + sizeofbox*2
            end = end + (end - start + 1) * 2;
            start = temp;
        }
        return binarySearch(arr, target, start, end);

    }
    static int binarySearch(int[] arr, int target, int start, int end) {
        while(start <= end) {
            // find the middle element
//            int mid = (start + end) / 2; // might be possible that (start + end) exceeds the range of int in java
            int mid = start + (end - start) / 2;

            if (target < arr[mid]) {
                end = mid - 1;
            } else if (target > arr[mid]) {
                start = mid + 1;
            } else {
                // ans found
                return mid;
            }
        }
        return -1;
    }
}
```


# Finding size of array by indices
- arr=[0,1,2,3,4,5,6,7,8,9,10]
- If we wan to find the size of box from index 2 to 8
- Visualize it as [0-8] - [2nd index -1]
- i.e [[0,1] -  [2,3,4,5,6,7,8]]
- If end index is at 8, start index is at 2 , 
- Which is end - (start-1) = end-start+1

# Peak index in a mountain array (a.k.a bitonic array)
- Let's call an array **arr** a mountain if the following properties hold:
    - arr.length >= 3
    - There exists some i with 0 < i < arr.length - 1 such that:
        - arr[0] < arr[1] < ... arr[i-1] < arr[i]
        - arr[i] > arr[i+1] > ... > arr[arr.length - 1]
- Given an integer array arr that is guaranteed to be a mountain, return any i such that arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1].
```
Input: arr = [0,1,0]
Output: 1

Input: arr = [0,2,1,0]
Output: 1

Input: arr = [0,10,5,2]
Output: 1

Constraints:
3 <= arr.length <= 104
0 <= arr[i] <= 106
arr is guaranteed to be a mountain array.
```
- 

