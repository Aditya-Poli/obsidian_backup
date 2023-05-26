# [Largest Sum Contiguous Subarray (Kadane’s Algorithm)](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

- Read
- Discuss(740+)
- Courses
- Practice
- Video

Given an array **arr[]** of size **N**. The task is to find the sum of the contiguous subarray within a **arr[]** with the largest sum. 

![kadane-algorithm](https://media.geeksforgeeks.org/wp-content/cdn-uploads/kadane-Algorithm.png) 

The idea of **Kadane’s algorithm** is to maintain a variable **max_ending_here** that stores the maximum sum contiguous subarray ending at current index and a variable **max_so_far** stores the maximum sum of contiguous subarray found so far, Everytime there is a positive-sum value in **max_ending_here** compare it with **max_so_far** and update **max_so_far** if it is greater than **max_so_far**.

So the main **Intuition** behind **Kadane’s algorithm** is, 

– the subarray with negative sum is discarded (_by assigning max_ending_here = 0 in code_).

– we carry subarray till it gives positive sum.

[**Pseudocode**](https://www.geeksforgeeks.org/what-is-pseudocode-a-complete-tutorial/)**:**

> Initialize:  
>     max_so_far = INT_MIN  
>     max_ending_here = 0
> 
> Loop for each element of the array
> 
>   (a) max_ending_here = max_ending_here + a[i]  
>   (b) if(max_so_far < max_ending_here)  
>             max_so_far = max_ending_here  
>   (c) if(max_ending_here < 0)  
>             max_ending_here = 0  
> return max_so_far

**Illustration:**

>     Lets take the example: {-2, -3, 4, -1, -2, 1, 5, -3}  
>     max_so_far = INT_MIN  
>     max_ending_here = 0
> 
>     for i=0,  a[0] =  -2  
>     max_ending_here = max_ending_here + (-2)  
>     Set max_ending_here = 0 because max_ending_here < 0  
>     and set max_so_far = -2
> 
>     for i=1,  a[1] =  -3  
>     max_ending_here = max_ending_here + (-3)  
>     Since max_ending_here = -3 and max_so_far = -2, max_so_far will remain -2  
>     Set max_ending_here = 0 because max_ending_here < 0
> 
>     for i=2,  a[2] =  4  
>     max_ending_here = max_ending_here + (4)  
>     max_ending_here = 4  
>     max_so_far is updated to 4 because max_ending_here greater   
>     than max_so_far which was -2 till now
> 
>     for i=3,  a[3] =  -1  
>     max_ending_here = max_ending_here + (-1)  
>     max_ending_here = 3
> 
>     for i=4,  a[4] =  -2  
>     max_ending_here = max_ending_here + (-2)  
>     max_ending_here = 1
> 
>     for i=5,  a[5] =  1  
>     max_ending_here = max_ending_here + (1)  
>     max_ending_here = 2
> 
>     for i=6,  a[6] =  5  
>     max_ending_here = max_ending_here + (5)  
>     max_ending_here = 7  
>     max_so_far is updated to 7 because max_ending_here is   
>     greater than max_so_far
> 
>     for i=7,  a[7] =  -3  
>     max_ending_here = max_ending_here + (-3)  
>     max_ending_here = 4

Follow the below steps to Implement the idea:

- Initialize the variables **max_so_far** = INT_MIN and **max_ending_here** = 0
- Run a for loop from **0** to **N-1** and for each index **i**: 
    - Add the arr[i] to max_ending_here.
    - If  max_so_far is less than max_ending_here then update max_so_far  to max_ending_here**.**
    - If max_ending_here < 0 then update max_ending_here = 0
- Return max_so_far

Below is the Implementation of the above approach.


```java
// Java program to print largest contiguous array sum
import java.io.*;
import java.util.*;

class Kadane {
	// Driver Code
	public static void main(String[] args)
	{
		int[] a = { -2, -3, 4, -1, -2, 1, 5, -3 };
		System.out.println("Maximum contiguous sum is "
						+ maxSubArraySum(a));
	}

	// Function Call
	static int maxSubArraySum(int a[])
	{
		int size = a.length;
		int max_so_far = Integer.MIN_VALUE, max_ending_here
											= 0;

		for (int i = 0; i < size; i++) {
			max_ending_here = max_ending_here + a[i];
			if (max_so_far < max_ending_here)
				max_so_far = max_ending_here;
			if (max_ending_here < 0)
				max_ending_here = 0;
		}
		return max_so_far;
	}
}

```
**Output**

```output
Maximum contiguous sum is 7
```
**Time Complexity:** O(N)  
**Auxiliary Space:** O(1)

## Print the Largest Sum Contiguous Subarray 

> To print the subarray with the maximum sum the idea is to maintain **start** index of **maximum_sum_ending_here** at current index so that whenever **maximum_sum_so_far** is updated with **maximum_sum_ending_here** then start index and end index of subarray can be updated with **start** and **current index**.

Follow the below steps to implement the idea:

- Initialize the variables **s**, **start,** and **end** with **0** and **max_so_far** = INT_MIN and **max_ending_here** = 0
- Run a for loop from **0** to **N-1** and for each index **i**: 
    - Add the arr[i] to max_ending_here.
    - If max_so_far is less than max_ending_here then update max_so_far to max_ending_here and update **start** to **s** and **end** to **i** .
    - If max_ending_here < 0 then update max_ending_here = 0 and **s** with **i+1**.
- Print values from index **start** to **end**.

Below is the Implementation of above approach:

```java
// Java program to print largest
// contiguous array sum
import java.io.*;
import java.util.*;
class GFG {

	static void maxSubArraySum(int a[], int size)
	{
		int max_so_far = Integer.MIN_VALUE,
			max_ending_here = 0, start = 0, end = 0, s = 0;

		for (int i = 0; i < size; i++) {
			max_ending_here += a[i];

			if (max_so_far < max_ending_here) {
				max_so_far = max_ending_here;
				start = s;
				end = i;
			}

			if (max_ending_here < 0) {
				max_ending_here = 0;
				s = i + 1;
			}
		}
		System.out.println("Maximum contiguous sum is "
						+ max_so_far);
		System.out.println("Starting index " + start);
		System.out.println("Ending index " + end);
	}

	// Driver code
	public static void main(String[] args)
	{
		int a[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
		int n = a.length;
		maxSubArraySum(a, n);
	}
}

// This code is contributed by prerna saini

```

**Output**
```output
Maximum contiguous sum is 7
Starting index 2
Ending index 6
```
**Time Complexity:** O(n)  
**Auxiliary Space:** O(1)

**Kadane’s Algorithm** can be viewed both as greedy and DP. As we can see that we are keeping a running sum of integers and when it becomes less than 0, we reset it to 0 (Greedy Part). This is because continuing with a negative sum is way worse than restarting with a new range. Now it can also be viewed as a DP, at each stage we have 2 choices: Either take the current element and continue with the previous sum OR restart a new range. Both choices are being taken care of in the implementation.

## **Recursive implementation of Kadane’s algorithm to find the maximum contiguous sum of an integer array.**

> To determine the maximum subarray sum of an integer array, Kadane’s Algorithm uses a Divide and Conquer strategy. This algorithm’s fundamental concept is to break the given array into smaller subarrays, recursively solve the issue for each subarray, and then combine the solutions to find the overall solution.

Recursive algorithm to find the maximum contiguous sum of an integer array:

1. The input array **“arr”** and its length **“n”** are the two parameters for the function **“maxSubArraySum”**.
2. When there is only one element in the array, the base case of the recursion occurs. In this situation, the function merely returns that element.
3. Finding the midpoint of the array **“m”** in the recursive case splits the problem into two smaller subproblems. (i.e., the index of the middle element).
4. To find the largest subarray sum in those subarrays, the function recursively calls itself on the left half of the array and the right half of the array (starting from the midpoint). **“left_max”** and **“right_max”** contain these values.
5. The function loops through the right half of the array, keeping track of the maximum subarray sum ending at each index, to determine the maximum subarray sum that crosses the middle element of the array. This value is stored in **“right_sum”**.
6. The function then performs a loop through the array’s left half, recording the highest subarray sum beginning at each index. **“left_sum”** is where this value is kept.
7. The sum of the maximum subarray sum beginning at the left half and ending at the right half (i.e., **“left_sum + right_sum”**) crosses the middle element. **“cross_max”** is where this value is kept.
8. The **“left_max”**, **“right_max”**, and **“cross_max”** subarray sums are returned by the function as their respective maximum values.

Below is the Implementation of above algorithm:

```java
import java.util.Arrays;
public class Program {
	// Define a function to find the maximum subarray sum
	public static int maxSubArraySum(int[] arr)
	{
		// Base case: when there is only one element in the
		// array
		if (arr.length == 1) {
			return arr[0];
		}

		// Recursive case: divide the problem into smaller
		// sub-problems
		int m = arr.length / 2;

		// Find the maximum subarray sum in the left half
		int leftMax
			= maxSubArraySum(Arrays.copyOfRange(arr, 0, m));

		// Find the maximum subarray sum in the right half
		int rightMax = maxSubArraySum(
			Arrays.copyOfRange(arr, m, arr.length));

		// Find the maximum subarray sum that crosses the
		// middle element
		int leftSum = Integer.MIN_VALUE;
		int rightSum = Integer.MIN_VALUE;
		int sum = 0;

		// Traverse the array from the middle to the right
		for (int i = m; i < arr.length; i++) {
			sum += arr[i];
			rightSum = Math.max(rightSum, sum);
		}

		sum = 0;

		// Traverse the array from the middle to the left
		for (int i = m - 1; i >= 0; i--) {
			sum += arr[i];
			leftSum = Math.max(leftSum, sum);
		}

		int crossMax = leftSum + rightSum;

		// Return the maximum of the three subarray sums
		return Math.max(crossMax,
						Math.max(leftMax, rightMax));
	}

	// Example usage
	public static void main(String[] args)
	{
		int[] arr = { -2, -3, 4, -1, -2, 1, 5, -3 };
		int maxSum = maxSubArraySum(arr);
		System.out.println("Maximum contiguous sum is "
						+ maxSum);
	}
}

```

**Output**
```output
Maximum contiguous sum is 7
```

**Practice Problem:** 

> Given an array of integers (possibly some elements negative), write a C program to find out the *maximum product* possible by multiplying ‘n’ consecutive integers in the array where n ≤ ARRAY_SIZE. Also, print the starting point of the maximum product subarray.