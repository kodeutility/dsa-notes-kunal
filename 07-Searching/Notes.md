<head>
  <link href="/fontawesome/css/all.css" rel="stylesheet"> <!--load all styles -->
</head>

<i class="fas fa-user"></i> <!-- uses solid style -->
<i class="far fa-user"></i> <!-- uses regular style -->
<i class="fal fa-user"></i> <!-- uses light style -->

# Searching <i class="fas fa-search"></i>
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
### Observation
- Basically we are suppose to find the index of maximum number in given array
- Brute force way is linear search till we find max element O(N)
- Possibilities
    - if arr[mid]>arr[mid+1] && arr[mid]>arr[mid-1] then we  have found maximum element, return mid
    - if arr[mid] > arr[mid+1] then we are in decreasing part of array then our answer is mid or elements before mid, mid might be potential answer i.e. update search space end=mid
    - if arr[mid] < arr[mid+1] then we are in increasing part of the array then our answer is mid+1 or elements after mid+1, mid+1 might be potential answer i.e. update search space start=mid+1
```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int start = 0;
        int end = arr.length -1;
        int possible_answer=Integer.MIN_VALUE;
        int possible_index = -1;

        while(start<=end){
            int mid= start + (end-start)/2;
            if(arr[mid]>arr[mid+1] && arr[mid]>arr[mid-1]){
                return mid;
            }
            else if(arr[mid]>arr[mid+1]){
                if(arr[mid]>possible_answer){
                    possible_answer=arr[mid];
                    possible_index=mid;
                }
                end=mid;
            }else if(arr[mid]<arr[mid+1]){
                if(arr[mid+1]>possible_answer){
                    possible_answer=arr[mid+1];
                    possible_index=mid+1;
                }
                start=mid+1;
            }
        }

        return possible_index;
    }
}
```
## OR
- start and end are trying to find the maximum number
- Both start and end are always trying to find the maximum number, hence at any given point of time start and end pointer have best answers
- Since we have loop till start<end , when we have start==end loops starts and both start and end are pointing to maximum value
```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int start = 0;
        int end = arr.length -1;

        while(start<end){
            int mid= start + (end-start)/2;
            if(arr[mid]>arr[mid+1]){
                end=mid;
            }else{
                start=mid+1;
            }
        }
        return start; // OR return end;
    }
}
```

# Find in Mountain Array
- You may recall that an array arr is a mountain array if and only if:
    - arr.length >= 3
    - There exists some i with 0 < i < arr.length - 1 such that:
        - arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
        - arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
- Given a mountain array mountainArr, return the minimum index such that mountainArr.get(index) == target. If such an index does not exist, return -1.
- You cannot access the mountain array directly. You may only access the array using a MountainArray interface:
    - **MountainArray.get(k)** returns the element of the array at index k (0-indexed).
    - **MountainArray.length()** returns the length of the array.

```
Input: array = [1,2,3,4,5,3,1], target = 3
Output: 2
Explanation: 3 exists in the array, at index=2 and index=5. Return the minimum index, which is 2.

Input: array = [0,1,2,4,2,1], target = 3
Output: -1
Explanation: 3 does not exist in the array, so we return -1.

Constraints:
3 <= mountain_arr.length() <= 104
0 <= target <= 109
0 <= mountain_arr.get(index) <= 109
```
- First we find the peak element
- Then do orderAgnostic Binary Search on first half of Mountain array , if not found then do orderAgnostic Binary search on second half of array
```java
//Code
```

# Search in Rotated Sorted Array
- There is an integer array nums sorted in ascending order (with distinct values).
- Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). 
- For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
- Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
- You must write an algorithm with O(log n) runtime complexity.

### Approach 1
- Find pivot in the array, which is largest number in the array
- Once pivot is found then we have 2 arrays which are both sorted
- Apply binary search till (0 to pivot) , if not found then return binary search of (pivot+1 to end of array)
- How to find pivot?
    - In [3,4,5,6,7,0,1,2]
    - We can see 3,4,5,6,7 is ascending and 0,1,2 is also ascending
    - 7,0 is descending only two elements can be descending as this is a pivot
    - if 7 is mid, then we know breaking condition will be if arr[mid] > arr[mid+1] then mid is the pivot

### Cases for finding answer (Below cases can occur only for 1 pair of elements)
- Case 1: if arr[mid] > arr[mid+1] then mid is the pivot
- Case 2: if arr[mid] < arr[mid-1] then mid-1 is the pivot

# Rotation count
- Find the number of rotationsin given array
- We can just find the pivot index and add 1 to it
- E.g. [5,6,7,8,9,0,1,2,3,4] count: 4+1 = 5 rotations
- E.g. [0,1,2,3,4,5,6,7,8,9] count: -1+1 = 0 rotations

```java
public class RotationCount {
    public static void main(String[] args) {
        int[] arr = {4,5,6,7,0,1,2};
        System.out.println(countRotations(arr));
    }

    private static int countRotations(int[] arr) {
        int pivot = findPivot(arr);
        return pivot + 1;
    }

    // use this for non duplicates
    static int findPivot(int[] arr) {
        int start = 0;
        int end = arr.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            // 4 cases over here
            if (mid < end && arr[mid] > arr[mid + 1]) {
                return mid;
            }
            if (mid > start && arr[mid] < arr[mid - 1]) {
                return mid-1;
            }
            if (arr[mid] <= arr[start]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return -1;
    }

    // use this when arr contains duplicates
    static int findPivotWithDuplicates(int[] arr) {
        int start = 0;
        int end = arr.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            // 4 cases over here
            if (mid < end && arr[mid] > arr[mid + 1]) {
                return mid;
            }
            if (mid > start && arr[mid] < arr[mid - 1]) {
                return mid-1;
            }

            // if elements at middle, start, end are equal then just skip the duplicates
            if (arr[mid] == arr[start] && arr[mid] == arr[end]) {
                // skip the duplicates
                // NOTE: what if these elements at start and end were the pivot??
                // check if start is pivot
                if (arr[start] > arr[start + 1]) {
                    return start;
                }
                start++;

                // check whether end is pivot
                if (arr[end] < arr[end - 1]) {
                    return end - 1;
                }
                end--;
            }
            // left side is sorted, so pivot should be in right
            else if(arr[start] < arr[mid] || (arr[start] == arr[mid] && arr[mid] > arr[end])) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return -1;
    }
}
```

# Split Array largest sum
- Given an array nums which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays.
- Write an algorithm to minimize the largest sum among these m subarrays.

```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.

Input: nums = [1,2,3,4,5], m = 2
Output: 9
Example 3:

Input: nums = [1,4,4], m = 3
Output: 4

Constraints:
1 <= nums.length <= 1000
0 <= nums[i] <= 106
1 <= m <= min(50, nums.length)
```
### Brute Force
- Try every sub array combination
- For every subarray take max sum
- Find minimum of all maximum sum of subarrays

### Observations
- We have to split into subarrays, in each way of spliting maximum sum is picked and out of all ways if more than 1 then minimum is picked
- What is the minimum number of partitions can make on the sub array?
    - Minimum partition is 1, so it is just whole array
    - Here we take sum of all entire array since m=1 and that is the answer
    - E.g. [7,2,5,10,8] -> 7+2+5+10+8=32
- What is the maximum number of partitions can make on the sub array?
    - Upto 50 , it will be the length of array, so just individual elements
    - Theres is only one way, individual numbers is the sum of it's subarray so answer is the maximum element
    - E.g. [7,2,5,10,8] -> 10
- minimum answer = max value in array
- maximum answer = sum of all values in array
- So our answer can only be in the range [10 to 32]
```
When we have a range of answer and we have to find potential answer we can use Binary Search
```
- Here in this example , our answer lies in range from 10 to 32 and we know all numbers between 10 to 32 is sorted so we can try binary search
- Trial 1:
    - 10+32/2 = 21, now this is one potential answer
    - 21 means largest individual sum we can have
    - So let's divide our array in subarrays which sums upto 21 or less [7,2,5] and [8,10]
    - And while creating each subarray we take count of pieces we made
    - Check if have made pieces that is less than or equal to given **m**
- If we are finishing out pieces, try to reduce 21 and check again by reducing search space
- Basically(pieces made <= m) then search in left side of middle , so new search space is start & end=mid
- Trial 2:
    - Now start is 10 and end is 21
    - mid 10+21/2 = 15
    - So let's divide our array in subarrays which sums upto 15 or less [7,2,5], [8], [10] which made 3 pieces
    - (pieces made > m) then search in right side of middle
    - Update search space , start=mid+1,end
    - now we have to search in values 16 to 21
- Trial 3:
    - Now start is 16 and end is 21
    - New mid is 18
    - So let's divide our array in subarrays which sums upto 18 or less [7,2,5], [8,10] which made 2 pieces
    - Check if have made pieces that is less than or equal to given **m**
    - (pieces made <= m) then search in left side of middle , so new search space is start & end=mid
- Trial 4:
    - Now start is 16 and end is 18
    - Mid is 17
    - So let's divide our array in subarrays which sums upto 17 or less [7,2,5], [8], [10] which made 3 pieces
    - (pieces made > m) then search in right side of middle
    - Update search space , start=mid+1,end
    - now we have **start=mid=end** i.e. 18 which is final answer
- Concept is
    - If we have a certain sum, if we are making more pieces than given **m** we have to increase value of potential answer
    - If we have a certain sum, if we are making less pieces or equal than given **m** we have to descrease value of potential answer 

```java
class SplitArray {
    public int splitArray(int[] nums, int m) {
        // Range of possible answers
        int start = 0; // maximum element in array
        int end = 0; // Sum of array

        for (int i = 0; i < nums.length; i++) {
            start = Math.max(start, nums[i]); // in the end of the loop this will contain the max item of the array
            end += nums[i];
        }

        // binary search
        while (start < end) {
            // try for the middle as potential ans
            int mid = start + (end - start) / 2;

            // calculate how many pieces you can divide this in with this max sum
            int sum = 0;
            int pieces = 1;
            for(int num : nums) {
                if (sum + num > mid) {
                    // you cannot add this in this subarray, make new one
                    // say you add this num in new subarray, then sum = num
                    sum = num;
                    pieces++;
                } else {
                    sum += num;
                }
            }

            if (pieces > m) {
                start = mid + 1;
            } else {
                end = mid;
            }

        }
        return end; // here start == end
    }
}
```

# Search in 2D array
- Linear search is 2D array take O(m*n) time complexity
```java
for(int i=0;i<arr.length;i++){
    for(int j=0;j<i.length;j++){
        if(arr[i][j]==target){
            return new int[]{i,j};
        }
    }
}
```
# Matrix is sorted in row wise and column wise
- Take any row and it will be sorted
- Take any column and it will be sorted
