[Link](https://practice.geeksforgeeks.org/problems/maximize-number-of-1s0905/1)[👍]

Given a binary array **arr** of size **N** and an integer **M**. Find the maximum number of **consecutive 1's** produced by flipping at most **M 0's**.  
 

**Example 1:**

**Input:**
N = 3
arr[] = {1, 0, 1}
M = 1
**Output:**
3
**Explanation:**
Maximum subarray is of size 3
which can be made subarray of all 1 after
flipping one zero to 1.

**Example 2:**

**Input:**
N = 11
arr[] = {1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1}
M = 2
**Output:**
8
**Explanation:**
Maximum subarray is of size 8
which can be made subarray of all 1 after
flipping two zeros to 1.

**Your Task:**  
Complete the function **findZeroes()** which takes array **arr** and two integers **n, m**, as input parameters and **returns** an integer denoting the answer.  
 

**Expected Time Complexity:** O(N)  
**Expected Auxiliary Space:** O(1)  
 

**Constraints:**  
1 <= N <= 10^7  
0 <= M <= N  
0 <= arri <= 1

# Solution

This is my naive solution.
I make things more complicated, i.e the time complexity for this problem is O(n^2).
But I made this even more complicated of O(n^2 m)
```java


// User function Template for Java

class Solve {
    // m is maximum of number zeroes allowed to flip
    int findZeroes(int arr[], int n, int m) {
        // code here
        int length = 0;
		
        for(int i = 0; i < n; i++){
            int k = i;
            for(int j = 0; j < m; j++) {
                while(k < n && arr[k++] != 0);
            }
            while(k < n && arr[k] != 0)k++;
            length = Math.max(length, k - i);
        }
		
		return length;
    }
}
```



# Solution (Online)
In this article, we have explored algorithms to Find the longest sequence of consecutive ones when atmost k zeros can be altered to 1. This involve techniques like Sliding Window approach.

|TABLE OF CONTENTS|
|---|
|1) Problem statement|
|2) Naive approach|
|3) Sliding Window approach|
|4) Conclusion|

## 1)Problem statement

  

Given a binary array. Find the longest sequence of consecutive ones when atmost k zeros can be altered to 1.

For example,  
Let the binary array be nums=[1,0,1,1,0,0,1,0].  
Let k be 2.  
Flipping zeros at indices (4,5) or (1,4) will give consecutive sequence of ones containing 5 ones which is the longest possible sequence of ones.

## 2)Naive approach

  

It is said that k zeros can be flipped, so instead of flipping the zeros let's search for a sequence containing atmost k zeros.  
In this approach considering each index of the array, we find the subarray starting with that index which contains ones and atmost k zeros. At any instance while traversing for the subarray if number of zeros are greater than k the process of finding the subarray for that index is stopped and will proceed for the next index.  
The longest of all such subarrays is tracked.

Let's look at dry run of the algorithm.

> nums=[1,0,1,1,0,0,1,0]  
> k=2

Let the length of the maximum subarray containing all 1s with atmost k zeros flipped is res.

> Initialize res=0

For index=0

> [**1,0,1,1,0**,0,1,0] currSubArrayLength=5  
> res=max(res,currSubArrayLength)=max(0,5)=5

For index=1

> [1,**0,1,1,0**,0,1,0] currSubArrayLength=4  
> res=max(res,currSubArrayLength)=max(5,4)=5

For index=2

> [1,0,**1,1,0,0,1**,0] currSubArrayLength=5  
> res=max(res,currSubArrayLength)=max(5,5)=5

For index=3

> [1,0,1,**1,0,0,1**,0] currSubArrayLength=4  
> res=max(res,currSubArrayLength)=max(5,4)=5

For index=4

> [1,0,1,1,**0,0,1**,0] currSubArrayLength=3  
> res=max(res,currSubArrayLength)=max(5,3)=5

For index=5

> [1,0,1,1,0,**0,1,0**] currSubArrayLength=3  
> res=max(res,currSubArrayLength)=max(5,3)=5

For index=6

> [1,0,1,1,0,0,**1,0**] currSubArrayLength=2  
> res=max(res,currSubArrayLength)=max(5,2)=5

For index=7

> [1,0,1,1,0,0,1,**0**] currSubArrayLength=1  
> res=max(res,currSubArrayLength)=max(5,1)=5

Hence the maximum consecutive ones when 2 zeros can be flipped in the array nums=[1,0,1,1,0,0,1,0] is 5.

### Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int nums[]={1,0,1,1,0,0,1,0};
    int n=sizeof(nums)/sizeof(nums[0]);
    int k=2;
    int res=0;
    int zeros,ones;
    for(int i=0;i<n;i++)
    {
        //intialize the counts to 0
        zeros=0,ones=0;
        //start from index i
        int j=i;
        //traverse through the array
        for(;j<n;j++)
        {
            //if 0 is encountered increment zeros count by one
            if(nums[j]==0)
                zeros++;
            //if 1 is encountered increment ones count by one
            else
                ones++;
            //if zeros count is greater than k then 
            //break the loop(stop considering elements from then)
            //because we can have atmost k zeros in the subarray
            if(zeros>k)
                break;
        }
        //j-1 is the index at which the subarray ends 
        //hence (j-1-i+1)=(j-i) gives the length of the subarray
        res=max(res,j-i);
    }
    //print length of the maximum subarray containing all 1s with atmost k zeros flipped
    cout<<res<<endl;
    return 0;
}
```

```output
5
```

  

The time complexity for the naive approach is O(n2)  
Traverse through the array - O(n)  
For each index find a subarray which contains all 1s with k 0s flipped - O(n)  
Hence, the complexity is O(n2).

The time complexity can be improved using the optimized approach.

Let's look at the sliding window approach.

## 3)Sliding Window approach

  

In this approach a window is maintained based on given constraints.

Here, the constraint is to have atmost k zeros in the subarray with rest of the elements as ones.

A window is said to be stable if it contains atmost k zeros otherwise it is unstable.

Hence, whenever the window becomes unstable we slide the window.

There will be two pointers left and right which are bounds of the window, each time the window becomes unstable the left pointer will moved to decrease the size of the window until the window becomes stable.

### ALGORITHM

1.Initialize two variables `l`,`r` to zero indicating the left and right bounds of the window  
2.Increment the size of the window with `r`  
  2.1.If a zero is encountered increment the `zeros` count  
  2.2.If a one is encountered increment the `ones` count  
  2.3.When the window becomes unstable i.e., `zeros` count becomes more than `k` decrease the size of the window using `l` until the window becomes stable  
    2.3.1.If a zero is encountered decrement the `zeros` count  
    2.3.2.If a one is encountered decrement the `ones` count  
    2.3.3.Increment `l`  
  2.4.Keep track of the maximum subarray

  

Let's look at dry run of the algorithm.

> nums=[1,0,1,1,0,0,1,0]  
> k=2

Let the length of the maximum subarray containing all 1s with atmost k zeors flipped be res.

> Initialize res=0

Let l,r be the left and right bounds of the window respectively.

> Initialize l=0,r=0

Let zeros,ones be the zeros and ones count in the window respectively.

> Initialize zeros=0,ones=0

Increment the window size using r

r=0

> nums[r]=1  
> ones=ones+1=0+1=1  
> res=max(res,r-l+1)=max(0,0-0+1)=1

r=1

> nums[r]=0  
> zeros=zeros+1=0+1=1  
> res=max(res,r-l+1)=max(1,1-0+1)=2

r=2

> nums[r]=1  
> ones=ones+1=1+1=2  
> res=max(res,r-l+1)=max(2,2-0+1)=3

r=3

> nums[r]=1  
> ones=ones+1=2+1=3  
> res=max(res,r-l+1)=max(2,2-0+1)=3

r=4

> nums[r]=0  
> zeros=zeros+1=1+1=2  
> res=max(res,r-l+1)=max(3,4-0+1)=5

r=5

> nums[r]=0  
> zeros=zeros+1=2+1=3  
> Here, the number of zeros are greater than k hence decrease the window using l and update the counts  
> l=0 nums[l]=1  
> ones=ones-1=3-1=2  
> l=1 nums[l]=0  
> zeros=zeros-1=3-1=2  
> l=2  
> The number of zeros in the current window are atmost k. Hence, stop reducing the window  
> res=max(res,r-l+1)=max(5,5-2+1)=5

r=6

> nums[r]=1  
> ones=ones+1=2+1=3  
> res=max(res,r-l+1)=max(5,6-2+1)=5

r=7

> nums[r]=0  
> zeros=zeros+1=1+1=3  
> Here, the number of zeros are greater than k hence decrease the window using l and update the counts  
> l=2 nums[l]=1  
> ones=ones-1=3-1=2  
> l=3 nums[l]=1  
> ones=ones-1=2-1=1  
> l=4 nums[l]=0  
> zeros=zeros-1=3-1=2  
> l=5  
> The number of zeros in the current window are atmost k. Hence, stop reducing the window  
> res=max(res,r-l+1)=max(5,7-5+1)=5

Hence the maximum consecutive ones when 2 zeros can be flipped in the array nums=[1,0,1,1,0,0,1,0] is 5.

### Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int nums[]={1,0,1,1,0,0,1,0};
    int n=sizeof(nums)/sizeof(nums[0]);
    int k=2;
    int res=0;
    int zeros,ones,l,r;
    //intialize the counts to 0
    zeros=0,ones=0;
    //intially there will be no elements in the window 
    //hence the l,r will be pointing to the first index
    l=0,r=0;
    while (r<n)
    {
        //if 0 is encountered increment zeros count by one
        if(nums[r]==0)
            zeros++;
        //if 1 is encountered increment ones count by one
        else
            ones++;
        //the below while loop gets executed whenever the window becomes
        //unstable i.e., zeros count becomes greater than k
        
        //whenever the zeros count becomes greater than k reduce the window until 
        //the given constraints are fulfilled i.e., zeros count becomes less than or equal to k

        //the execution of the loop halts when the window is stable
        while(l<r and zeros>k)
        {
            //if 0 is encountered decrement zeros count by one i.e., remove that 0 from the window
            if(nums[l]==0)
                zeros--;
            //if 1 is encountered decrement ones count by one i.e., remove that 1 from the window
            else
                ones--;
            //decrease the window size by incrementing left bound of the window
            l++;
        }
        //since we are dealing with indices (r-l+1) would give the length of the subarray
        //keep track of the maximum subarray
        res=max(res,r-l+1);

        //increment r irrespective whether the window will be stable or not 
        //because l takes care of the stability of thw window
        r++;
    }
    //print length of the maximum subarray containing all 1s with atmost k zeros flipped
    cout<<res<<endl;
    return 0;
}
```

```output
5
```

## 4)Conclusion

  

The Sliding Window approach takes O(n) time complexity as the array will be traversed twice using the two pointers.  
Traverse by left pointer l - O(n)  
Traverse by right pointer r - O(n)  
Summing up it's O(n+n)= O(2n)= O(n)  
Hence the time complexity is O(n) where n is the size of the given binary array.
# *Solution Submitted
This is the solution submitted*
In this solution I have removed ones variables because it is not needed to maintain.
We only need to maintain zeros variables.

```java
//{ Driver Code Starts
// Initial Template for Java

import java.io.*;
import java.util.*;

class GFG {
    // Driver code
    public static void main(String[] args) throws Exception {
        BufferedReader br =
            new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine().trim());
        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine().trim());
            String[] str = br.readLine().trim().split(" ");
            int[] arr = new int[n];
            for (int i = 0; i < n; i++) {
                arr[i] = Integer.parseInt(str[i]);
            }
            int m = Integer.parseInt(br.readLine().trim());

            int ans = new Solve().findZeroes(arr, n, m);

            System.out.println(ans);
        }
    }
}
// } Driver Code Ends


// User function Template for Java

class Solve {
    // m is maximum of number zeroes allowed to flip
    int findZeroes(int arr[], int n, int m) {
        //intially there will be no elements in the window 
	    //hence the l,r will be pointing to the first index
		int l = 0, r = 0;
		//intialize the counts to 0
		int zeros = 0;
		int length = 0;
		
		while(r < n) {
			//if 0 is encountered increment zeros count by one
			if(arr[r] == 0) {
				zeros++;
			}
			//if 1 is encountered increment ones count by one
			// I have removed the ones variable because we don't
			// need to keep track of it
			
			//the below while loop gets executed whenever the window becomes
	        //unstable i.e., zeros count becomes greater than k
	        
	        //whenever the zeros count becomes greater than k reduce the window until 
	        //the given constraints are fulfilled i.e., zeros count becomes less than or equal to k

	        //the execution of the loop halts when the window is stable
			
			while(l < r && zeros > m) {
				//if 0 is encountered decrement zeros count by one i.e., remove that 0 from the window
				if(arr[l] == 0) {
					zeros--;
				}
				//if 1 is encountered decrement ones count by one i.e., remove that 1 from the window
				//decrease the window size by incrementing left bound of the window
				l++;
			}
			//since we are dealing with indices (r-l+1) would give the length of the subarray
	        //keep track of the maximum subarray
			length = Math.max(length, r-l+1);
			//increment r irrespective whether the window will be stable or not 
	        //because l takes care of the stability of thw window
			r++;
		}
		
		return length; 
    }
}
```
