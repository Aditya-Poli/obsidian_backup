## [30.  Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words)[👍]
You are given a string `s` and an array of strings `words`. All the strings of `words` are of **the same length**.

A **concatenated substring** in `s` is a substring that contains all the strings of any permutation of `words` concatenated.

-   For example, if `words = ["ab","cd","ef"]`, then `"abcdef"`, `"abefcd"`, `"cdabef"`, `"cdefab"`, `"efabcd"`, and `"efcdab"` are all concatenated strings. `"acdbef"` is not a concatenated substring because it is not the concatenation of any permutation of `words`.

Return _the starting indices of all the concatenated substrings in_ `s`. You can return the answer in **any order**.

**Example 1:**

**Input:** s = "barfoothefoobarman", words = ["foo","bar"]
**Output:** [0,9]
**Explanation:** Since words.length == 2 and words[i].length == 3, the concatenated substring has to be of length 6.
The substring starting at 0 is "barfoo". It is the concatenation of ["bar","foo"] which is a permutation of words.
The substring starting at 9 is "foobar". It is the concatenation of ["foo","bar"] which is a permutation of words.
The output order does not matter. Returning [9,0] is fine too.

**Example 2:**

**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
**Output:** []
**Explanation:** Since words.length == 4 and words[i].length == 4, the concatenated substring has to be of length 16.
There is no substring of length 16 is s that is equal to the concatenation of any permutation of words.
We return an empty array.

**Example 3:**

**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
**Output:** [6,9,12]
**Explanation:** Since words.length == 3 and words[i].length == 3, the concatenated substring has to be of length 9.
The substring starting at 6 is "foobarthe". It is the concatenation of ["foo","bar","the"] which is a permutation of words.
The substring starting at 9 is "barthefoo". It is the concatenation of ["bar","the","foo"] which is a permutation of words.
The substring starting at 12 is "thefoobar". It is the concatenation of ["the","foo","bar"] which is a permutation of words.

**Constraints:**

-   `1 <= s.length <= 104`
-   `1 <= words.length <= 5000`
-   `1 <= words[i].length <= 30`
-   `s` and `words[i]` consist of lowercase English letters.

Accepted

`338.9K`

Submissions

`1.1M`

Acceptance Rate

`31.2%`


**[Solution](**)**

- if the length of the String `s` is zero or the given `words` are empty then return the empty new ArrayList.
```java
if (s.isEmpty() || words.length == 0)
      return new ArrayList<>();
```

- First make a Map containing all the words in the words as keys.
- make a substring of the length of the word.
- Iterate and reduce the frequency of the appeared element.
- If the all elements are not appeared from the zeroth index.
- Restart the procedure from the index 1.
- Like this we need to proceed further.
- If from the no word start then move to another idx.
- we need to return the starting idx and the ending idx.

**[Solution 1](**)**

```java
class Solution {

    public List<Integer> findSubstring(String s, String[] words) {  

        /* List for the output idxs */

        List<Integer> idx = new ArrayList<Integer>();

        /* if the s is empty or the words are empty */

        if (s.isEmpty() || words.length == 0)

        /* return the empty List */

            return idx;

        /* length of the substring */

        int len = words[0].length();

        /* Map containing the frequencies of the words */

        Map<String, Integer> map = new HashMap<String, Integer>();
  
        /* store the frequencies of the words in the Map */

        for(String word: words) map.put(word, map.getOrDefault(word, 0) + 1);
  
        /* Iterate through the string and check for the substrings or words */

        /* i <= s.length() - len * words.length because we need have all of the

           words in the string i.e. we need to check all words in the*/

        for(int i = 0; i <= s.length() - len * words.length; i++){

            /* copy the map because we need to check at  every idx */

            Map<String, Integer> copyMap = new HashMap<String, Integer>(map); 

            /* check for all the words at the current idx */

            for(int j = 0; j < words.length; j++){

                /* extract the substring from the current idx of s */

                String str = s.substring(i + j*len, i+ j*len + len);  

                /* check if str is in copyMap */

                if(copyMap.containsKey(str)){

                    /* check for the frequency of the str in copyMap */

                    int count = copyMap.get(str);

                    /* If it is 1 remove the element because we visited req no of times */

                    if(count == 1) copyMap.remove(str);

                    /* else decrement its frequency */

                    else copyMap.put(str, count - 1);  

                    /* check if it is empty i.e. if we have visited all the words */

                    if(copyMap.isEmpty()) {

                        /* from the current idx we have vsited all words */

                        idx.add(i);

                        break;

                    }

                }  

                /* if the str is not part of the copyMap then break */

                else { break; }
            }

        }
 
        return idx;

    }

}
```



**[Solution 2](**)**

```java
class Solution {
  public List<Integer> findSubstring(String s, String[] words) {
    if (s.isEmpty() || words.length == 0)
      return new ArrayList<>();

    final int k = words.length;
    final int n = words[0].length();
    List<Integer> ans = new ArrayList<>();
    Map<String, Integer> count = new HashMap<>();

    for (final String word : words)
      count.merge(word, 1, Integer::sum);

    for (int i = 0; i <= s.length() - k * n; ++i) {
      Map<String, Integer> seen = new HashMap<>();
      int j = 0;
      for (; j < k; ++j) {
        final String word = s.substring(i + j * n, i + j * n + n);
        seen.merge(word, 1, Integer::sum);
        if (seen.get(word) > count.getOrDefault(word, 0))
          break;
      }
      if (j == k)
        ans.add(i);
    }

    return ans;
  }
}

```


## [32.  Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

Given a string containing just the characters `'('` and `')'`, return _the length of the longest valid (well-formed) parentheses_ 

_substring_

.

**Example 1:**

**Input:** s = "(()"
**Output:** 2
**Explanation:** The longest valid parentheses substring is "()".

**Example 2:**

**Input:** s = ")()())"
**Output:** 4
**Explanation:** The longest valid parentheses substring is "()()".

**Example 3:**

**Input:** s = ""
**Output:** 0

**Constraints:**

-   `0 <= s.length <= 3 * 104`
-   `s[i]` is `'('`, or `')'`.

Accepted

`603.6K`

Submissions

`1.8M`

Acceptance Rate

`32.8%`

**[Solution](**)**

```java
class Solution {

    public int longestValidParentheses(String s) {

        /* if the s is null or the len(s) is less than 2 */

        if(s == null || s.length() < 2) return 0;

        /* Init a stack */

        Stack<Integer> stack = new Stack<Integer>();

        /* loop through the string s */

        for(int i = 0; i < s.length(); i++){

          /* if opening element then push idx into the stack */

          if(s.charAt(i) == '('){

            stack.push(i);

          /* closing bracket case */

          } else {

            /* if stack is not and empty and the top is ( then pop */

            if(!stack.empty() && s.charAt(stack.peek()) == '('){

              stack.pop();

            /* else push idx it into the stack */

            } else {

              stack.push(i);

            }

          }

        }

        /* variables for maxLength and the end idx */

        int maxLen = 0;

        int endTerminal = s.length();

        /* if stack is empty i.e. entire string is satisfied */

        /* then return the length of the s */

        while(!stack.empty()){

          /* idx of the unbalanced paranthesisi */

          int startTerminal = stack.pop();

          /* check for the mac length of balanced valid paranthesis */

          maxLen = Math.max(maxLen, endTerminal - startTerminal - 1);

          /* decrease the length to the startTerminal value */

          endTerminal = startTerminal;

        }

  

        return Math.max(endTerminal, maxLen);

    }

}
```



## [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)


Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]
**Output:** 10
**Explanation:** The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]
**Output:** 4

**Constraints:**

-   `1 <= heights.length <= 105`
-   `0 <= heights[i] <= 104`

Accepted

`647.5K`

Submissions

`1.5M`

Acceptance Rate

`42.5%`


**[Solution](**)**
- Iterate through the heights.
- For each idx find out the nearest small element in the left and right directions.
- Because for up to nearest small element only the height is >= current idx height.
- find the difference between right and left idx and subtract one from it.
- difference is equal to the width of the rectangle and for the area multiply it with current height.
- keep track of the maximum area and return it.

**[Solution 1](**)**

**This approach works but 91/98 only passes `Time Limit Exceeded`**

```java
class Solution {

    public int largestRectangleArea(int[] heights) {

        int maxArea = 0;

        int[] nearestSmallLeft = nsl(heights);

        int[] nearestSmallRight = nsr(heights);

  

        for(int i = 0; i < heights.length; i++){

            maxArea = Math.max(maxArea, (nearestSmallRight[i] - nearestSmallLeft[i] - 1)*heights[i]);

        }

        return maxArea;

    }

  

    private static int[] nsl(int[] array){

      int[] out = new int[array.length];

  

      for(int i = 0; i < array.length; i++) {

        int j = i;

        while(j >= 0 && array[j] >= array[i]) j--;

        out[i] = j;

      }

      return out;

    }

  

    private static int[] nsr(int[] array){

      int[] out = new int[array.length];

      for(int i = 0; i < array.length; i++) {

        int j = i;

        while(j < array.length && array[j] >= array[i]) j++;

        out[i] = j;

      }

      return out;

    }

}
```

**[Solution 1 - Compressed](**)**

```java
int maxArea = 0;

      for(int i = 0; i < heights.length; i++) {

        int nearestSmallLeft = i;

          int nearestSmallRight = i;

        while(nearestSmallLeft >= 0 && heights[nearestSmallLeft ] >= heights[i]) nearestSmallLeft --;

        while(nearestSmallRight < heights.length && heights[nearestSmallRight] >= heights[i]) nearestSmallRight++;

        maxArea = Math.max(maxArea, (nearestSmallRight - nearestSmallLeft - 1)*heights[i]);

      }

        return maxArea;
```


**[Solution 2](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-using-stack/)**

**Largest Rectangular Area in a Histogram using Stack**

-   Difficulty Level : [Hard](https://www.geeksforgeeks.org/hard/)
-   Last Updated : 02 Nov, 2022

-   Read
-   Discuss(230+)
-   Courses
-   Practice
-   Video

Find the largest rectangular area possible in a given histogram where the largest rectangle can be made of a number of contiguous bars whose heights are given in an array. For simplicity, assume that all bars have the same width and the width is 1 unit. 

**Example:** 

> **Input:** histogram = {6, 2, 5, 4, 5, 1, 6}  
>  
> 
> ![histogram](https://media.geeksforgeeks.org/wp-content/cdn-uploads/histogram1.png)
> 
> **Output:** 12
> 
> **Input:** histogram = {3, 5, 1, 7, 5, 9}  
> **Output:** 15

Recommended Problem

Maximum Rectangular Area in a Histogram

[Stack](https://practice.geeksforgeeks.org/explore?page=1&category[]=Stack&sortBy=submissions)
[Data Structures](https://practice.geeksforgeeks.org/explore?page=1&category[]=Data%20Structures&sortBy=submissions)
[Microsoft](https://practice.geeksforgeeks.org/explore?page=1&company[]=Microsoft&sortBy=submissions)
[Google](https://practice.geeksforgeeks.org/explore?page=1&company[]=Google&sortBy=submissions)

[Solve Problem](https://practice.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1?utm_source=gfg&utm_medium=article&utm_campaign=bottom_sticky_on_article "Permalink to Maximum Rectangular Area in a Histogram")

Submission count: 1.3L

To solve the problem follow the below idea:

> For every bar ‘x’, we calculate the area with ‘x’ as the smallest bar in the rectangle. If we calculate the such area for every bar ‘x’ and find the maximum of all areas, our task is done. 
> 
> **How to calculate the area with ‘x’ as the smallest bar?** 
> 
> We need to know the index of the first smaller (smaller than ‘x’) bar on the left of ‘x’ and the index of the first smaller bar on the right of ‘x’. Let us call these indexes as ‘left index’ and ‘right index’ respectively. We traverse all bars from left to right and maintain a stack of bars. Every bar is pushed to stack once. A bar is popped from the stack when a bar of smaller height is seen. When a bar is popped, we calculate the area with the popped bar as the smallest bar. 
> 
> **How do we get the left and right indexes of the popped bar?**
> 
> The current index tells us the right index and the index of the previous item in the stack is the left index

Follow the given steps to solve the problem:

1.  Create an empty stack.
2.  Start from the first bar, and do the following for every bar hist[i] where ‘**i**‘ varies from 0 to n-1
    1.  If the stack is empty or hist[i] is higher than the bar at top of the stack, then push ‘**i**‘ to stack. 
    2.  If this bar is smaller than the top of the stack, then keep removing the top of the stack while the top of the stack is greater. 
    3.  Let the removed bar be hist[tp]. Calculate the area of the rectangle with hist[tp] as the smallest bar. 
    4.  For hist[tp], the ‘left index’ is previous (previous to tp) item in stack and ‘right index’ is ‘**i**‘ (current index).
3.  If the stack is not empty, then one by one remove all bars from the stack and do step (2.2 and 2.3) for every removed bar

Below is the implementation of the above approach.

-   java

```java
// Java program to find maximum rectangular area in linear
// time

import java.util.Stack;

public class RectArea {
	// The main function to find the maximum rectangular
	// area under given histogram with n bars
	static int getMaxArea(int hist[], int n)
	{
		// Create an empty stack. The stack holds indexes of
		// hist[] array The bars stored in stack are always
		// in increasing order of their heights.
		Stack<Integer> s = new Stack<>();

		int max_area = 0; // Initialize max area
		int tp; // To store top of stack
		int area_with_top; // To store area with top bar as
						// the smallest bar

		// Run through all bars of given histogram
		int i = 0;
		while (i < n) {
			// If this bar is higher than the bar on top
			// stack, push it to stack
			if (s.empty() || hist[s.peek()] <= hist[i])
				s.push(i++);

			// If this bar is lower than top of stack, then
			// calculate area of rectangle with stack top as
			// the smallest (or minimum height) bar. 'i' is
			// 'right index' for the top and element before
			// top in stack is 'left index'
			else {
				tp = s.peek(); // store the top index
				s.pop(); // pop the top

				// Calculate the area with hist[tp] stack as
				// smallest bar
				area_with_top
					= hist[tp]
					* (s.empty() ? i : i - s.peek() - 1);

				// update max area, if needed
				if (max_area < area_with_top)
					max_area = area_with_top;
			}
		}

		// Now pop the remaining bars from stack and
		// calculate area with every popped bar as the
		// smallest bar
		while (s.empty() == false) {
			tp = s.peek();
			s.pop();
			area_with_top
				= hist[tp]
				* (s.empty() ? i : i - s.peek() - 1);

			if (max_area < area_with_top)
				max_area = area_with_top;
		}

		return max_area;
	}

	// Driver code
	public static void main(String[] args)
	{
		int hist[] = { 6, 2, 5, 4, 5, 1, 6 };

		// Function call
		System.out.println("Maximum area is "
						+ getMaxArea(hist, hist.length));
	}
}
// This code is Contributed by Sumit Ghosh

```
     
         
**Output**

Maximum area is 12

**Time Complexity:** O(N), Since every bar is pushed and popped only once  
**Auxiliary Space:** O(N)

**Largest Rectangular Area in a Histogram by finding the next and the previous smaller element:**

To solve the problem follow the below idea:

> Find the previous and the next smaller element for every element of the histogram, as this would help to calculate the length of the subarray in which this current element is the minimum element. So we can create a rectangle of size **(current element * length of the subarray)** using this element. Take the maximum of all such rectangles.

Follow the given steps to solve the problem:

-   First, we will take two arrays **left_smaller[]** and **right_smaller[]** and initialize them with -1 and n respectively
-   For every element, we will store the index of the previous smaller and next smaller element in left_smaller[] and right_smaller[] arrays respectively
-   Now for every element, we will calculate the area by taking this **ith** element as the smallest in the range left_smaller[i] and right_smaller[i] and multiplying it with the difference of left_smaller[i] and right_smaller[i]
-   We can find the maximum of all the areas calculated in step 3 to get the desired maximum area

Below is the implementation of the above approach.

- java

`
```java
// Java code for the above approach

import java.io.*;
import java.lang.*;
import java.util.*;

public class RectArea {

	// Function to find largest rectangular area possible in
	// a given histogram.
	public static int getMaxArea(int arr[], int n)
	{
		// your code here
		// we create an empty stack here.
		Stack<Integer> s = new Stack<>();
		// we push -1 to the stack because for some elements
		// there will be no previous smaller element in the
		// array and we can store -1 as the index for
		// previous smaller.
		s.push(-1);
		int max_area = arr[0];
		// We declare left_smaller and right_smaller array
		// of size n and initialize them with -1 and n as
		// their default value. left_smaller[i] will store
		// the index of previous smaller element for ith
		// element of the array. right_smaller[i] will store
		// the index of next smaller element for ith element
		// of the array.
		int left_smaller[] = new int[n];
		int right_smaller[] = new int[n];
		for (int i = 0; i < n; i++) {
			left_smaller[i] = -1;
			right_smaller[i] = n;
		}

		int i = 0;
		while (i < n) {
			while (!s.empty() && s.peek() != -1
				&& arr[i] < arr[s.peek()]) {
				// if the current element is smaller than
				// element with index stored on the top of
				// stack then, we pop the top element and
				// store the current element index as the
				// right_smaller for the popped element.
				right_smaller[s.peek()] = (int)i;
				s.pop();
			}
			if (i > 0 && arr[i] == arr[(i - 1)]) {
				// we use this condition to avoid the
				// unnecessary loop to find the
				// left_smaller. since the previous element
				// is same as current element, the
				// left_smaller will always be the same for
				// both.
				left_smaller[i]
					= left_smaller[(int)(i - 1)];
			}
			else {
				// Element with the index stored on the top
				// of the stack is always smaller than the
				// current element. Therefore the
				// left_smaller[i] will always be s.top().
				left_smaller[i] = s.peek();
			}
			s.push(i);
			i++;
		}

		for (i = 0; i < n; i++) {
			// here we find area with every element as the
			// smallest element in their range and compare
			// it with the previous area. in this way we get
			// our max Area form this.
			max_area = Math.max(
				max_area, arr[i]
							* (right_smaller[i]
								- left_smaller[i] - 1));
		}

		return max_area;
	}

	// Driver code
	public static void main(String[] args)
	{
		int hist[] = { 6, 2, 5, 4, 5, 1, 6 };

		// Function call
		System.out.println("Maximum area is "
						+ getMaxArea(hist, hist.length));
	}
}
// This code is Contributed by Arunit Kumar.

```

**Output**

maxArea = 12

**Time Complexity:** O(N)  
**Auxiliary Space:** O(N)

**Related Articles:** [Divide and Conquer based O(N log N) solution](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/)

Thanks to [Ashish Anand](https://www.facebook.com/aasshishh?fref=ts) for suggesting initial solution. Please write comments if you find anything incorrect, or you want to share more information about the topic discussed above.

### Solution 3
```swift
What the Question is saying, 
Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, 
return the area of the largest rectangle in the histogram.
```

Understand this problem with an example;  
**Input:** `heights = [2,1,5,6,2,3]`  
![image](https://assets.leetcode.com/users/images/a844c036-9d8d-4155-a5fa-8f565822109d_1643426746.9005287.png)

Let's understand how we calculate this, let's took on index 4 height is 2. If we go to the left and see where the height is less then 2 and i.e. at index 1. So, that becomes the left Boundary. Similarly if we go to right and see where the height is less then 2 & i.e. at index 6 [which is end of the array].

Now we have left & right boundary the area could be find out by height * width. And width will get by (right - left - 1) in case of 4 that will be 6 - 1 - 1 = 4. And we know the height already i.e. 2.

The Area we get is 2 * 4 i.e. 8

![image](https://assets.leetcode.com/users/images/c49249ab-e50d-487a-8761-e130f41ee36c_1643428100.9047763.png)

The main idea here would be how to find **left boundary & right boundary** for every index. The **brute way** is using an **ARRAY**  
`For left boundary array:`

- Start with index 1, (left[0] = -1)
- For each index -> go to left & find the nearest index where height [index] < height[curr]
- Start with index 1,
- Eg : Index 1 : left[1] = -1

`For right boundary array:`

- Start with index n - 2 right[n - 1] = n
- For each index -> go to right & find the nearest index where height[index] < height[curr]
- Start with index n - 2
- Eg : Index 2 : right[2] = 4

I hope you got the point and let's code this brute force Approach then we move to optimal Approach:  
**Java**

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        if(n == 0) return 0; // Base Condition
        int maxArea = 0;
        int left[] = new int[n]; //fill left boundary
        int right[] = new int[n]; // fill right boundary
        
        left[0] = -1;
        right[n - 1] = n;
        
        for(int i = 1; i < n; i++){
            int prev = i - 1; // previous for comparing the heights
            while(prev >= 0 && heights[prev] >= heights[i]){
                prev = left[prev]; // we have done this to minimise the jumps we make to the left
            }
            left[i] = prev;
        }
        // Similarly we do for right
        for(int i = n - 2; i >= 0; i--){
            int prev = i + 1; 
            while(prev < n && heights[prev] >= heights[i]){
                prev = right[prev]; 
            }
            right[i] = prev;
        }
        // once we have these two arrays fill we need width & area
        for(int i = 0; i < n; i++){
            int width = right[i] - left[i] - 1;
            maxArea = Math.max(maxArea, heights[i] * width);
        }
        return maxArea;
        
    }
}
```

**C++**

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();
        if(n == 0) return 0; // Base Condition
        int maxArea = 0;
        vector<int> left(n); //fill left boundary
        vector<int> right(n); // fill right boundary
        
        left[0] = -1;
        right[n - 1] = n;
        
        for(int i = 1; i < n; i++){
            int prev = i - 1; // previous for comparing the heights
            while(prev >= 0 && heights[prev] >= heights[i]){
                prev = left[prev]; // we have done this to minimise the jumps we make to the left
            }
            left[i] = prev;
        }
        // Similarly we do for right
        for(int i = n - 2; i >= 0; i--){
            int prev = i + 1; 
            while(prev < n && heights[prev] >= heights[i]){
                prev = right[prev]; 
            }
            right[i] = prev;
        }
        // once we have these two arrays fill we need width & area
        for(int i = 0; i < n; i++){
            int width = right[i] - left[i] - 1;
            maxArea = max(maxArea, heights[i] * width);
        }
        return maxArea;
    }
};
```

ANALYSIS :

- **Time Complexity :-** BigO(N^2)
    
- **Space Complexity :-** BigO(N)
    

Now, let's see our Optimize Approach i.e. **Using Stack**  
So, what we do is we take a stack & keep on adding the indexes in the stack till we get a increasing sequence. Once the sequence becomes decreasing we need to pop the element and find the area `[That's the basic idea behind the stack]`

So, let's take the stack and we are at index 1. The height of current is less than that of top of stack which is the 0th index. As the height is decreasing. So, what we do here is find the area for elements in stack  
![image](https://assets.leetcode.com/users/images/7688de81-3901-4177-92b9-416735c81ab2_1643429827.2194455.png)

Now, to find the area we pop the element from stack & then for that element the area becomes **height[top] * curr i.e. 1**  
If the stack becomes empty i.e. if this is the only element present for that we find the width and multiply with the height of top element `[width would be curr - stack.peek - 1]` where curr is right & stack.peek() is left

For this case we **pop "0"** and stack becomes **empty**, so the area becomes **height[0] * curr = 2 * 1 = 2.** So, till now maxArea we have found is 2

![image](https://assets.leetcode.com/users/images/b4251cd2-8015-48eb-9ed4-b5bf6ffb9919_1643431407.4375658.png)

We will do this procedure for all the element's and we will get the **maxArea i.e. 10**

_I hope you got the idea,_ **So, let's code it up:**  
**Java**

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int maxArea = 0;
        Stack<Integer> st = new Stack<>();
        
        for(int i = 0; i <= n; i++){
            int currHeight = i == n ? 0 : heights[i];
            // check if currHeight becomes greater then height[top] element of stack. we do a push because it's an increasing sequence
            // otherwise we do pop and find area, so for that we write a while loop
            while(!st.isEmpty() && currHeight < heights[st.peek()]){
                int top = st.pop(); // current element on which we are working
                // now we need width & area
                int width = st.isEmpty() ? i : i - st.peek() - 1; // width differ, if stack is empty or not empty after we pop the element
                int area = heights[top] * width; // current height * width
                maxArea = Math.max(area, maxArea);
            }
            // if it doesn't enter in while loop, it means it's an increasing sequence & we need to push index
            st.push(i);
        }
        return maxArea;
    }
}
```

**C++**

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();
        int maxArea = 0;
        stack<int> st;
        
        for(int i = 0; i <= n; i++){
            int currHeight = i == n ? 0 : heights[i];
            // check if currHeight becomes greater then height[top] element of stack. we do a push because it's an increasing sequence
            // otherwise we do pop and find area, so for that we write a while loop
            while(!st.empty() && currHeight < heights[st.top()]){
                int top = st.top(); st.pop(); // current element on which we are working
                // now we need width & area
                int width = st.empty() ? i : i - st.top() - 1; // width differ if we stack is empty or not empty after we pop the element
                int area = heights[top] * width; // current height * width
                maxArea = max(area, maxArea);
            }
            // if it doesn't enter in while loop, it means it's an increasing sequence & we need to push index
            st.push(i);
        }
        return maxArea;
    }
};
```

ANALYSIS :

- **Time Complexity :-** BigO(N)
    
- **Space Complexity :-** BigO(N)
  

## [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)[👍]

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]
**Output:** 2.00000
**Explanation:** merged array = [1,2,3] and median is 2.

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]
**Output:** 2.50000
**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

**Constraints:**

-   `nums1.length == m`
-   `nums2.length == n`
-   `0 <= m <= 1000`
-   `0 <= n <= 1000`
-   `1 <= m + n <= 2000`
-   `-10^6 <= nums1[i], nums2[i] <= 10^6`

### Solution 1
Time complexity: O(m+n)O(m+n)O(m+n)

#### Idea

-   We create a new array with length that of the **sum of the array lengths**
-   We initialize **i & j = 0**. [i for nums1 & j for nums2]
-   Since the given arrays are already sorted it is easy to compare their elements. We comapre by observing nums1[i] < nums2[j]
-   if the element in nums1nums1nums1 at ithi^{th}ith is less than that of element at jthj^{th}jth index of nums2nums2nums2, we add nums1[i]nums1[i]nums1[i] to new array and increment i; so as to compare the next element of the array to nums2[j].
-   If the opposite case arises, we add nums2[j]nums2[j]nums2[j] to the new array as you can guess. And increment j by 1 for the same reasons we did it with i.
-   Depending on the length of new array, we calculate _median_.
-   If the length of array is even, median by rule is the average of the _2 middle elements_ of the array
-   If it is off, it is the _middlemost_ element

I will try to make a video on this to explain this with illustration soon, I'm currently on a time crunch ⏳ so it might take a while 😬

But here is the code, have a look the idea might just click once you see it (for me often the code helps me a lot)

#### Code

JAVA

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n1 = nums1.length;
        int n2 = nums2.length;
        int n = n1 + n2;
        int[] new_arr = new int[n];

        int i=0, j=0, k=0;

        while (i<=n1 && j<=n2) {
            if (i == n1) {
                while(j<n2) new_arr[k++] = nums2[j++];
                break;
            } else if (j == n2) {
                while (i<n1) new_arr[k++] = nums1[i++];
                break;
            }

            if (nums1[i] < nums2[j]) {
                new_arr[k++] = nums1[i++];
            } else {
                new_arr[k++] = nums2[j++];
            }
        }

        if (n%2==0) return (float)(new_arr[n/2-1] + new_arr[n/2])/2;
        else return new_arr[n/2];
    }
}
```

### Solution 2
![](https://codewithgeeks.com/wp-content/uploads/2022/07/Median-Of-Two-Sorted-Arrays.svg)



### Median Of Two Sorted Arrays LeetCode Solution 2022

-   [![](https://codewithgeeks.com/wp-content/litespeed/avatar/2ff167582d05bd77c691dabdd36e6e68.jpg?ver=1684247327forcedefault=1)](https://codewithgeeks.com/author/rishit16/)
-   Posted by[Rishit Pandey](https://codewithgeeks.com/author/rishit16/)
-   Updated 3 months ago
-   6 min

**Median Of Two Sorted Arrays LeetCode Solution:** Hi there, fellow geeks! In this article, we will tackle a classic problem of [binary search](https://en.wikipedia.org/wiki/Binary_search_algorithm) in which we are required to find the median of the array that results from merging two array into a sorted manner.

The problem statement says that we are given two arrays, A of size m and array B of size n, which are sorted in ascending order. The task is to merge the arrays and find the median of the merged array. Though it is not necessary to actually merge the arrays. Let us look at some methods to find the answer without consuming extra space.

#### Explanation:

The problem statement says that we will be given arrays of unequal size as argument of the function that we need to complete. The arrays are sorted in ascending order. Our job is to find the median that is the median of the array that results if we somehow merge both the arrays. This median also depends on the number of elements in the merged array.

We will try to seek multiple solutions to this question without actually merging the arrays because that is a very brute and time consuming approach. The time complexity of such an algorithm will be at least O(m+n) where m is the length of the first array and n is the length of the second array. We will try to reduce the time complexity.

#### Approach 1: (Using Linear Traversal)

We know that the arrays are sorted and the median will come from the middlemost element of the merged-sorted array. Thus it is easy to observe that we can traverse both the arrays using two pointers and store the elements that have been traversed into another array which will empty initially. This counting will stop when we have reached the central element of the merged array. Then, depending upon whether the final array contains even elements or odd elements, the median can be calculated easily. Let us put this method into an algorithm.

**Algorithm:**

1.  Store the sum of lengths of both the arrays into n.
2.  Declare an empty array merged of size n.
3.  Initialize i = 0, j = 0, k = 0. These variables will serve as the index pointers.
4.  Initialize a count variable to 0 and a current variable.
5.  Repeat steps 6 to 8 while count is less than n.
6.  If ith element of array1 is less than or equal to jth element of array2, store it in current and increment i.
7.  Else if jth element of array2 is smaller than ith element of array1, store it in current and increment j.
8.  Push back the value of current into the merged array and increment k.
9.  If n is even, median is the average of the two middlemost element.
10.  Else if n is odd, median is directly the central element.
11.  Return the median value.

##### Implementation in C++:

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size() + nums2.size();
        int merged[n];
        int mid = n/2;
        double median;
        int i = 0, j = 0, k = 0;
        int count = 0, curr;
        while(count<n){
            if(i<nums1.size() and j<nums2.size()){
                if(nums1[i]<=nums2[j]){
                    curr = nums1[i++];
                }
                else{
                    curr = nums2[j++];
                }
            }
            else if(i<nums1.size()){
                curr = nums1[i++];
            }
            else{
                curr = nums2[j++];
            }
            merged[k++] = curr;
            count++;
        }
        if(n%2==0){
            median = merged[mid] + merged[mid-1];
            median /= 2;
        }
        else{
            median = merged[mid];
        }
        return median;
    }
};
									 
```

##### Analysis of the Algorithm:

This approach to the solution of Median Of Two Sorted Arrays is a brute force method. Time complexity for this code is O(m+n) where ‘m’ is the length if the first array and ‘n’ is the length of the second array. The space complexity for this code is O(m+n) because we require an additional array of size (m+n).

### Approach 2: (Using binary search)

Previous one was the easiest and most obvious approach. But this question lies in the difficult region and is meant to be solved using the binary search method. When talking about sorted arrays, the first algorithm that comes to mind is Binary Search. We know that the size of the merged array will be (m+n) where m is the size of the first array and n is the size of the second array. This approach may look like merge sort.

In the merged array if we make a partition along the central element or elements, the array will be divided into two halves. All the elements of the first half will definitely be smaller than all the elements of the second half. Using this property we will try to construct the the first and second halves. For this operation, we will select certain random elements from both the arrays.

As mentioned previously, all the elements on the right half subarray must be smaller than all the elements on the left half subarray. It can be observed that this condition is satisfied if that the last element of the right half is smaller than the first element of the left half.

To find an optimal **median of two** [sorted arrays solution](https://codewithgeeks.com/merge-2-sorted-linked-lists-leetcode/), we will select elements from both the arrays such that half the elements constitute the right half and the rest form the left half of the merged array. But obviously we cannot select random elements to form the required subarray. So we will need to check the condition given in the previous paragraph to find the correct sequence of elements.

Suppose,

arr1[] = {1, 3, 4, 7, 10, 12}

arr2[] = {2, 3, 6, 15}

The merged array for these two arrays will be,

arr[] = {1, 2, 3, 3, 4, 6, 7, 10, 12, 15}

Suppose, we select 4 elements from arr1 and 1 element from arr2 for the formation of the right half and 2 elements from arr1 and 3 elements from arr2 for the left half. Then the subarray must look like this for a random combination.

![](data:image/png;base64,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mbqhAABjJ+fPjGXz68ik0jtL5vfdd9+y44471orvrGrou1FXzhGpsk7VcnaD/spXvlJ22WWXMa7OGkxGNqbPubE/m5T1R8YL4+N1AN4KLOccIClBz45BKe1OuXn6HURK12ebbbZ6ok9z6gwC0u8gpfFZhpWGqBtvvHF9zojSm+n3v/99+e1vf1tDgDw3F9ezzz575xnt7r///loanj5sOaFmqWUGIGMi30t6M4zLhgjZOWnTTTetS1yh29J4/4QTThiuT8mYSD+s1Vdfvay77rqdR7ojS77TIybBTn6Ws0ykWcqSAfh0001Xl0rn+JLmzAngJgavvvpqXSKeJbb5N8kSoE022WRAw78sF8qy/PRDy3tKQLnsssvWZTgDHfDx1mU5JwMtY9aMAbNx1thIeJaJoCxdbOstmT5jaWmQ813OfelHGjkGZ/yc8W/Od1kCOZDH5fQ4SyuT9CUdW1lmmUn4EVsF3HPPPeXMM8/s/d7H1nzzzVevGfpugAbAyAnRAACGACEaAMCEZTknAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALQQogEAAABACyEaAAAAALSYpGeYzu9hvPv73/9ennzyyfL888+XF198sbzyyiv18SmmmKJMN9105f3vf3+ZaaaZynve8576OMDE6D//+U/5y1/+Uh5++OHy1FNP1eNdHpt00knLVFNNVWaeeeYy++yzlw984APlXe96V+dPwfh199OlHHh+KaffWMrcM5Sy11qlbLlM54vQRTn+Zez3xBNP1GPiX//61/KPf/yjfu2d73xnHf/NMsssZY455ijvfe976+ODTcasjz/+eHn22WfL008/Xb+Hxrvf/e4y44wzlve9731lttlmq78OFi+99FK55ZZbyj333FP/HfI+V1hhhfLBD36w84x2+d5vvfXWcvPNN3ce6b/82y6zzDL1cwEYioRojHf//e9/6wXkfffdV0/iN9xwQ3nggQfqxWUzAMlFZS4o55lnnrL00kuXj33sY2W++eZzcQlMVP75z3/W49tNN91ULzjuvPPO8tBDD9VA7d///ncN0XKBOOecc5YFFligLLHEEmX11Vd3ccEEIURjoCW0yeTpddddV66//vpy//331/FfQqhMrEbGeh/60IfKXHPNVceAH//4x8siiywyaMaACZDuuuuucvXVV9fj+qOPPlpv+R4aU089dT2OZyJ4ueWWK+utt16Zf/75O18dGP/617/q+efSSy8tZ555ZrnxxhvreWippZYq3/3ud+vn3F/5/vfff/9y+umndx7pv7nnnrvsvffe5XOf+1znEYChRYjGeJXBU8Kz3/zmN+X888+vIVpO6qOTQC0h2g477FBWWWUVQRowUchkweWXX17OOOOMcs011wx3gTUqueDafPPNy+c///kBv+Bi6BGiMZAy3su471e/+lX53e9+VwO0NgmjEkJttdVWZa211hrwMWAmQC688MJ6XP/jH//YG/yNzoc//OGy5557lp133rnzSPflfHTFFVeUs846q/7a93z00Y9+tAZia6+9dueRdn/4wx/KbrvtVm6//fbOI/2Xyuvdd9+97LHHHp1HAIaWSb89TOf3MM4y+DjxxBPLIYccUmfDUpX2jne8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P/HEEz177LHHSN9bf28zzzxzz6GHHtp5xTe99tprPWeddVa9TunP59Dcms9jv/3267n//vs7rwYwNFnO2WVZsjnrrLPWmZqURWemqylzj1SdzTDDDHX2JkuCdtxxxzpDdNNNN9WlP5nNy6xRfh1RSq1vvPHGuqQzy0TznGEXef8z8zQ6mVVKtdwzzzxTZ5syc/XJT36y89XRy/eRBrGZGcv3Ni5SGp+/N7OAAINNZvqvu+66fu3iNjqpRk4fnRzXYVxZzslAyfg2485U42aMmyWEOb6lgitjwmZcmHFvWphkbJqWIanE3WqrrcoGG2xQK50GSpYd5v1njJ7x7+STT15br2RsmzF1ZNl9dtTPaoms8shu8wP1vrM7aM5B49I3ebrppisrrbTScBsiZAVJKgizIUAq1fL7VKNlaWvfzyKfUf58Pq++/44bbrihHTmBIc9yzgGSwcQTTzxRQ69bbrmld0voDDhygl5wwQVr/4IEag8//HDtT5AS8zQuTX+xPGdEKa2+/PLLy3nnnVdPdKN77qikf0L6PKQPWwYUubDbaKONOl9tl7DvV7/61TjvKLrEEkuULbfccoyWRQF0y8svv1x7+WTSYVzkAiV9dFZYYYXOIzD2LOdkMMjEcCZ+s5wwY9j8PmPUSIiW415CtLT7yKRp7g8WCc6yaUzG3BkL5/cZU8fUU09d+ww3773by077ynLOa665plxwwQWdR8Zcws6EgX13J+0r57n8G2a5Zq5Z+n4WmfRPiJbAbDD+OwJMSEI0AIAhQIgGADBh2foQAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAAACghRANAAAAAFoI0QAAhoB3v6OU909dytsnLWWqKUqZfsrOFwAAGC8m6Rmm83sAACZS//x3Kdc/XMqFd5Qy63SlrL9oKTO+p/NFAADGmRANAGCIyKjuv28M+3XY71ORBgDA+CNEAwAAAIAWeqIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAAC0EKIBAAAAQAshGgAAAACMVin/D3ik6LEPINogAAAAAElFTkSuQmCC)

To check whether all the elements of right half is less than all the elements of the left half, we must check and compare the extreme elements. Now, if we half selected the correct elements for the subarray, then 7 <= 3 and 2 <= 10. This condition is not true because 7 is not less than equal to 3. Thus, all elements of right half are not smaller than all elements of left half. This only means that the subarray that we selected are invalid. So, let us select some other combination. For example,

![](data:image/png;base64,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5KCUA2R89KMfLd/73vfqAQGGi6ZEPoPJzBRmpjMSKmXWrhnsJjDacccdyw477FCvD5Xzzz+/7LTTTrV3SQZWCeOy7GDxxRev1/O8MzObGchzzjmnvifTdyUygP/c5z5Xl2roSwEjm2WPDFcJUvbee+9aLZOq6Yz73vCGN5Tf/va39eupmDr44IPHuzppYmQs+vDDD9dK6fGVVh6pYstxN9L/c88996ztPAZDgpz03spxPasq0lakCb36j1WWWGKJ8q1vfauOuQcqk3/f//73a9VXqpoSVmYZ39prr12X8aWXVf6OPIe0W8jYIsssm7FFgqXURQzW69HIz5x/z7PPPru2Wclzi/6vSXzyk58sJ510UvfauGU5acZ7+V1O/9S0jchr8r73va++Hvk3SfiX5ZCXXnppDdwaWQr5qU99qr4H9FuFFkj4BfHggw92dt11107PgSCBaGfyySfvzDrrrJ3VVluts9Zaa3Xe/va319tz6TkQd+69997ud8LQ6xkYdc4999zOSiut1OkZmNff056BeqdnINfpGcR1lltuud7f3znmmKPTMzjsfufQueCCCzo9g9HO8ssv3znwwAM7DzzwQPcro/vXv/7Vueyyy+p7sfkZcllzzTU7d955Z/dewEh1yyOdzoaHdzpTbt3pLLpHp3PKdd0vwBB67rnnOt/73vc6PSf99ZiT4+mee+7Z2WijjXqPQ2ussUbnnnvu6X7H8Pb3v/+985Of/KQz88wz1+c+1VRT1Z/lySef7N7jtffss892jj322M4SSyzR+xrm9V166aU766yzTmexxRbrvT33Oeuss7rfOW75+U466aTOnHPOWb8/4/jFF1+8c8IJJ9Sv9ffSSy91rrrqqjqmn3LKKev3vOlNb+psvvnmnWeeeaZ7r8Fx2223dTbbbLPe37X828w111yd9dZbr56DNK9JLp/85Ce73zUwl156aR1n5fXcbbfdOtdcc03nhRde6H71v/7whz90DjvssM673vWu0f6+jB+vvvrq7r2AkWzynjc1VCkLTiVKSoJTApweDl/84hdrs81tttmmzpbAcJXm8Jm9TLl8KhUze7nJJpuUb3zjG3VWd7CXNAxEdm7MDGaeXxruvtruk5n57BkY1zL/zEI2suSjKeEHgEklqwFSCZNK6lQm5diT5YG5jFTp55T+n1nKFllWmJ5aGfMOlvzdqURKD6pUEuXYngbu++yzT9l1113Lu9/97u49x1/GA/n5mh69Gbevu+66ZYMNNhjjBjkZK2Xn9lQ2NRtYpcIqFVJpeTKYstnPL37xi7rccK655iprrbVWrdA/8MAD6zhpYqSSPhsz7LbbbuX//b//V6vsx1TFldcr46zNNttstNcrVWF5fsDIJ/yiV8rYMxBISNCEXjvvvHM9MKZsGoa7LP9LP4sMchJ67bvvvmXDDTesDXmHo/Ts+vznP183jxjXeywDsQwIU6LfSKl+/358ADCx0ocyTeXTSiDtL7IjYI6tI7XXa8K8NIHPsrbIzzRq1Kh6/B1M+XsTJOb1TMiS0CtL6vI8xhTIjI/s5pjllI0s7cuSyTEFX418LcsrV1555e4tpYZnzbLWwZLnkR5cmXhvQq/tt9++9pSbWFmqm8dKsDWu1zjjxQSifXezT1+0JjAFRjbh1wTIh2CzO0qaaqc/VnYQySVr0LN+PrNlGTg0PbLGJmvys/XuiSeeWE444YS6LXGztr3p93PqqafWx8/fleu5va/MSqRqK/dJr6P07oo8diq60lOgefysp0/D7P7PLTu8bLXVVrW/gNCLkSbNSrNVd3pgZSA5nEMvABiuMgZN5U/GsxlHpjIqmxxlXDhSZUx+5ZVX1jFxZMfk/Dx9Q47BkOqi9N9KX62MtydF6BWZCEv41fSrSkP3TLClCn5cMvGdMK7ZPfqPf/xj7YmW853Bkuf69a9/vXz729+eZKHXhErAO5R/P/DaEX6NhwROWVKV3UIOOOCAWlny5S9/uXz2s58tn/nMZ+olywNz2x577FG3F84OOf2Dqv6yXCvb+SZ42nLLLeuuL5lhSMCWMCtluqkOyePn78osUf8ZmZTj7rXXXvU+u+yyS7nsssvq4+b57r///vU5NY+f5VUJwvo/ryzBSoPLBAhCL0aazBout9xyZeONN27tDog5IWma0kZ+5ummm657DQAmXkKUNB3P2DJN7ldZZZU6oTS2CqLhLFXSaXSfMXkjDfoTPA32z5TNalLdlOWIk7KKLrs6ZnfChJWRyb8EXwP5+VI1n8ryvu1NsoHQE0880b322kt11qc//ekawg21ySabrF6A9hF+DVDWoCdQSrCUqqhswZtdEXOgScjUyP0yq5SKsIROqUJJpdXYZk9yUM73ZdYm1Vg54KQ0OyFYZkDSGyCzMJG/K1Vi/dee56S4eR45Oc5uLxdffHH9/mwVnEqv5vHzteyikn5BwMiQz4XshNT0+EofsCwRMDsJwKSS/l5ZGvjrX/+6Xp9vvvnKeuutV/8/UmWyN5PGze6QqRTPrsrDIWiZVPqHVakmS0XXQCWI69t39PW81C/nR03ftEhbmPzOACOf8GuAMhi49tpr6yUh0gwzzFCWXHLJ8pGPfKRWmqRZ5aabblobNKbnUGZaEjRl+ePhhx8+2hr8cckSxp/97Gfl+OOPr6FXKjuybj8H6lRnjWsWJ88vPRoOPfTQOoDJSXKaPeYgn0aafRtmA8Nfgu3MWGdJc97fkVna9OeztBOASSGTsZlgTePxBB9taHIfmajOMbSpikrIk+qrSbHccLjIxHfOHxqp5hqfjaryWvRt/P/iiy/WarLXm5dffrk8++yz5fHHH+/e8kq13mAvjwVeG8KvAUr5a0KkHBgyCMjywywzPPjgg2sV2LHHHlsrrA455JC6Zj0l4k1Idcstt9RljQNdO5+ZqVSO5aCTD9vscpLHzFLKNIHM9bHtBpMT5ez2kktCuixj/NKXvlT7C2QJZZrZf/CDH2zVQR/aJs15c/KRz4/0+ssy6uxmGfkcyhKUNddcs14HgInV9I/NsaYNTe4joVB2VswlMpZPf6m0SWiTVH71DWwycT4+k2NTTDFFrXBqZAK/6T/8epIqwSyRbare8j7I6ziSKx+B/xJ+DVBmUJZZZpmyww471B1I0lA7VV5ZctT03EnYldmknJQmYEq1VmRJY/onNE3oxyXhVSq+0oA+j5OQbfPNN6/9uNK7K9dXW2217r3/V/6+fHinb1dmthKaffWrX639BRKcpWdYfg4VIzA8ZNCasLrZOCOX9BZM9Wbe77mkijOfNWnQm/A9/QXb2tsMgMGVoCOhVyZrUyE1yyyz1InSkdzkPtKKJLtWZgVHZClgdvPrW+VEqc3u+/b7TWj4elv2mKqvtJVplvxGgt+lllqqnpMBI5/wa4ASfmW74PT8GtcuiJlVSmXW0ksv3b3llfXjTa+egcigI8sp06B+QkKqPIcsy9x22201sIdhLrO1RxxxRO/GGblkk4uE7DkRydfTdDifK9kafeuttx6tNwcATIy+Te4zZkxl1Mc//vEBNUwfrhLo3Xzzzb1V06niGTVqVG10z+gyxuhb4ZfXrgkMXy+y3DETjc2mYvl9SSubddZZZ0S/D4D/En69RhKWZY14I30Uml4945IDUA7MqfbKVswTIsslN9lkk9oTCBjeMtuYy9jkZCQDsWyGkWXRWQ75elySAMCklSqfVB83FS/ZTCUn/FkeOJI99thj9edqKpgyps4Etv5N/ytjjNdzU/eMp9LX+YwzzujtDZcqwdVXX73umgm0g/BrGJp99tlrqfmCCy7YvWX8pU9Dljmq+ILhL7Otec9n44y+l4022qjeniXUWc6cjTPSX3DXXXetVWHZ0XWgvQQBoL9MzmZSJVVfCYnSDza9bXPSP5Klb2Z+rlTyNBZYYIE6uayKh74y+XjvvfeWk08+ue6GH2kzkfdACgn8vkB7CL8mUE44s3tMTkZThZGG1H379WS3xhx0J0QqxsZne+IxSaN7Pb1gZMj7PT28Emz1vRx55JHlO9/5Tt3wIk2Hm4ar6en3q1/9qhxwwAHjtZMsAPSVHrPpiZWQKNXFiy22WJ14Gek9sRLkpZInPb8ioV7agWRymP/Vf5nj66kSLBWCJ554Yj2fi/zs6fOVXfxTBQm0h/BrPKUZ/Q033FCOO+64sv/++9eT0jShTwPqvv16clvzIQowIRJiZ6CeJdD5vPnc5z7XG4BlJ6b0pUjQnpMXABgfacdx/fXXlzPPPLO3yX2qXZZddtnuPUamVLPddddd5ZJLLuneUuoGVWussYadzl9Fzm+eeuqp7rVXKp8mdiJ+JEifr1NPPbUWLiT8SwA8//zz13FX23YEBYRf4yVbQGct+De+8Y3yta99re7GlpmyVIDloAHwWskgNM3uU4LfzMZmKWS2b8/sNgCMj1S8nHPOOfU4kpP+bKqSXrEJATLmHdMlYUHffpMJ0P70pz/1fn04NEnPDsqZHLr11lvr9VTypH/ZSN+5cmyyW2Pf5Xn5N5qYc5M3vOENZeqpp+5ea6f8Lp922mnlxz/+ca0UzHsg/eA+/elP1x32LXeE9hF+DVCzzOjb3/52Of/88+sBJY3pswvIRz7ykbozY/9ePRokApNSArBVVllltH6ADz74YK1GBYDxkSWBV155Zf1zTvwTXKXp/SGHHPKql5NOOqncd9999Xvi4YcfLieccELv17ND8VBXI+fnSk/MpnF5eulm5/ORvpRzbDIplsq9Rv9KrnHJZFpCw0aCr74bd7VNE3zld/aOO+6ov//zzDNPbUHxmc98RoUgtJTwawBSPn3jjTfWmYG777673pYDaLaA3n333cvBBx9cjjrqqNF69eS2hGIAk9LMM8882k5VCeYff/zx7jUAGJiEHU8++WT9c5bSZyJl3333Hesl490777yzfk8kaDr88MN7v55elQkThkp2rszPcd1119XrTUVbNo9psyxT7NvrN5Vfzz//fPfauKXyqTnHibRdSGjYRk1BQxN8xZxzzlmDr1yyCRHQTsKvAXjxxRfLzTffPNoOIAm2vvnNb9aKr/QRyG0Ag22qqaZSmg/AeMvxY1IvbZtssslq4DRUfv/739eqr2b55UwzzVR7mDX9MttqxhlnHC2sSqiZZZ8JNcclS1efeOKJeoksE80kfybb2iYbluX347DDDusNvlIxl/O5rbfeWvAFLSf8GoDMEDzyyCP14BBzzDFH3QZ63nnnrdcBBkuWMqRcv5EB7+uhKS0Ak9ZCCy1UK10+9alPDfiyzjrrjFZ9PNtss5X11luv9+vrr79+bRg+FFLtlJ3Wm6qvSJuAtld9RSbhU73UTIal6isVek1l39hkeeQtt9zSu0w0Y4ollliidRNrCb4uv/zyWp3YFDQIvuD1Rfg1AAm9Uv3VSK+vnHCOTWacUkIMMCZZbpLBVwacfZsHj00GbhnY33777d1bXhmkLrDAAt1rADAwCYb23HPPuoP5QC/pfbvMMst0H6GUxRZbrBxwwAG9X99pp52GrLdWKpcSbjz66KP1evo2ZcfkLHtsuwRVqW7rOx5IFdwVV1wx1uqvnONkdctvfvOb7i2lzD333OX9739/91o7NMHX97///drXLprga7vttqureID2E34NwDTTTDNa08dUXeSAMqaDSfqD5eB7wQUXlKuvvrp7K8Do0jD4e9/7Xtlrr71qg+CHHnporCFYBm5XXXVV3ZK+aSacJSuZuW/zDlYAMC4vvfRSrXRK2NNIoLHGGmu8bpqXp+IuVW7Z+TGyIc6pp55aX5cxnbMk+MoE3E9/+tPeJYBvfetby/ve975WhUGCL6Ah/BqAHDSzjr4p/222hs4OOVkSGTnoptLr+uuvL0cccURdS963ceRIkOAuS6qefvrp/7mkfLrvgTMHzGxt3f9+w2GLa16/UrKfYKj/72Vu61u9+Wq/6/23cH8tpSnv/fffX4Ov3XbbrRx44IF1AJrt2ROENc8pO2ldc801dYetgw46aLTZ2Sw9WX311S3BBuB1LWPwBF9NM/70rVp44YWH5eRQxhnPPPPM/1z6j0Ey7k6VeP/75dxjTGFWKsETfjU7QuexMn449NBD66R8xhz5/ixzzATceeedVwOhX/7yl/X+ec3SHy071g92YJifJ+ca/X/WXPqfW4zp9cs4LyFXf3ncBHx5DZrgKz9nduRPC5uMGxP8jety1113DWgJKTC8Tdbp0f0zY3HZZZeVr3/9673VXFlbv+SSS9aDTHqA5YM4FV85cU11Rj6A8+GalzdfW3rppWuFR2ag+ssJbg4+KRuPsd331Zx//vm11Dwf0JG160cffXT980Dl4HHppZfWg0R/2c0nJ91NxUlmlz70oQ/9zzbIuT3Pu83bSTN8/e53v6s7+CSM7ivvx7w3+75/8z7ru3Qj0vg3pf6D0R8k79V99tmnBl6NNJdNn40sXWjeWxn05b5Z7ti8/yLvsa222qrOWvbd4QkYeW59tJR9zi7l9JtKWXi2Ur6+VikbL939IgwjOR7tvffe5Wc/+1m9njFfdjgfyuX3mdDK+HXXXXetx/rIpNAuu+xSPvvZz9brw0XOCfIcE0b1l2N8JtabsXyO8yuvvPL/VCZlrLDKKquUxRdfvHvLf+WcIrvOZyfDJqzJ5H3G5xnzZLyQ1yv3y4R983elknzUqFHly1/+cg2/BrvfVyb6EsalwKC/PMczzjije62URRZZpPaZ62uKKaaot6+11lp1xU4jQeExxxxTvvGNb/T2NJt22mlr1fz4bIKQx8/rl3FX38cHRpiEX4zb888/3+k5mHR6DgydKaecMoHhq17e/OY3d3o+IDvrrrtuZ6655qq39Zxod3o+1LuPNrqnnnqq03OA7v3+sd331eT+PR/6vY+x9dZbd78ycD0HwU7PIKb3MSbk8v73v7/zm9/8pvuIMHh6BpSdngH4GH8vB3rJe/sLX/hC9xFfW88++2ynZ0BWPytmnHHGMT6fMV3y+dIz4O3ssccenQceeKD7aMBIdssjnc6Gh3c6U/Ycuhfdo9M55bruF2CYuf322zsbbbRR7zEp48Z77rmn+9WhkePpfvvt13njG99Yn9NUU03VWX/99Tv3339/9x7Dx2OPPdbZcccde1+/CbnMOeecnYMOOqj7iP8rY4Ndd9218853vnOM39//Ms0003SWX375zpFHHtl54YUXuo8yuHIeM88884zx+Q30svrqq//PuOjhhx/ubL/99mO8//hexvT4wMhi2eMAzTDDDHWHm1R/rbvuurVctm/T+8yQZGnkUkstVTbZZJM6w7Dtttv27sKW9fepBBuTbAudGZdmjf7Y7vtq8v3NLE3fP4+PzASNqYx6fGRmpPk5YDDldzcVXxPz+5fvzftnMKSvxgYbbFCrvzIzveaaa9ZZ3Hxm9H3/Zsv4LD/IzO9KK61UNttss7LHHnvU2VnLHQEYTH3HqDk+5ZiZsd9QysqLVH6nsifPKbserrrqquNV2TNYJtVYe2xjlYwNvvjFL5avfOUrtTIv5yzZybDv+CiV7vPMM09d5rjpppvW9gvZrXOo+qPldelftT8+mt/FnFP1ldcqv68Te26Sx89rlgswcln2OJ7ywfz444+XG264oe6Okj9HSmhzEMmOMlm2lLLi9O1JP59bb721ltduuOGGYzxZzZKsSy65pJx11lm1l9bY7vtqsnY/a/bTZywnzlm2lRPr8ZHy6LPPPnuiGvWnZDrl0lkKCoMtv7vZbSrvowmR9/Fqq61W1l577e4tgyPLIB555JHaq+Tee++tZf/pSRYZsGXQmiULKenP0pIEZ0B7WPbISJGleeeee25thZHjU1qAZNyX49RQSWP3X/ziF/UYmueUXl/rr7/+sAy/Mua/+OKLayP6CZXJ9iz7S/uGscnYIjtf5jwkl4zzm6V/mcDP+UYu2bFzKP/9Iucxp5xySm2zMiEScqUAIUFe3wAvr0Ha0WSZbvOzT4g8/gorrFC23HLL7i3ASCT8AgAYQsIvAIDXlmWPAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAK0l/AIAAACgtYRfAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAK0l/AIAAACgtYRfAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAK0l/AIAAACgtYRfAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWpN1enT/DL1eeOGF8uCDD5YnnniiPP300+XPf/5zvX3qqacub3/728vss89e5plnnjLTTDPV22E4+de//lV/b/M7/Pjjj5fnnnuuvPTSS2WKKaYo008/fZljjjnKvPPOW2adddb6Oz0c5Dn/4Q9/KI8++mh93/3xj38sL774Yv1a876ba6656vOeccYZ6+3DzV/+8pf6/J988sn6Mzz77LPdr5Qy3XTT1dd7lllm8dkB/dz6aCn7nF3K6TeVsvBspXx9rVI2Xrr7RRhC//73v8tjjz1Wbr/99vL888+Xqaaaqsw///zlve99b/ceA5Nj8W9/+9vy17/+tXvLwOS4/c53vrMstdRSZcopp+zeCgDjT/hFr//85z/lmWeeKbfccku5/vrry+9+97vy+9//vp7M/ulPf6r3mWaaaeoJ+HzzzVeWXHLJ8oEPfKAsscQS9cQWhlrCovvuu68OsPP7e8cdd5QHHnig/l4nXMrA+S1veUsduC+yyCJl6aWXLh/+8IfL3HPP3X2EwZfnlffYtddeW6677rpy77331vddwqPmJKF53y2wwAJl2WWXLauuumpZbLHFhk1wl9ArJ0ZXXHFFufnmm8tDDz1Uf4annnqqe49SA7u8znPOOWdZYYUVyrrrrlsWWmih7lfh9U34xXCUsOumm24qv/rVr8rpp59ej1VvetObytZbb10OPfTQ7r3G7R//+Ef52c9+Vnbeeec6yTM+ctzeYIMNyiGHHFJmnnnm7q0AMP6EX1Q5Ab/tttvKqaeeWn7961/XP+e2sckJ+TLLLFO22WabstZaawnAGFKplLrooovKL37xi3L11VePFry8mgRKm266afnUpz41JEFMTggS1J100knlN7/5Tbn//vu7X3l1CZESHm255ZZljTXWGPIALCHdueee2/u6D2RWP+H51772tXoCBQi/GF4y/nv44YfLBRdcUEOrHKf++c9/dr9a6jHzuOOO614bt0xAJbzad999u7eMnzXXXLOGbTl2AMCEmuKbPbp/5nUsy5QykPnBD35QBzypAstJdSo1FlxwwVpy/ra3va0uHfv73/9evyd/zixg7p/lTKmmSXk6DIUrr7yy7LnnnuXSSy+tAUx+F9/61rfWaqn8buZ39I1vfGMNnLKMI7K8N5ViuZ7f88FeTpgqrwzoTzzxxDob/oY3vKEuKX7Pe95TKytHjRpV34OZo8jP9PLLL9fnn+WcOZnIzzaUVWsJvhLc5aQmJ0c5YZp22mnr815llVXKSiutVJZffvm6PKb5N8iSmfzb5LZU3gGlPP3nUi6/t5S7nyxl5ulKWXGBUkbN3v0iDJKM/TKRlCreo446qhx99NHl7rvvrrf3tfjii5f111+/e23c/va3v9XK5jxupP1Agqy0IHjHO94x1kuOiZlo/dCHPlTe/OY31+8HgAmh8ovq1ltvLd/61rfKaaedVgODLKlqLhl45KQ8QUHud+GFF9YT3YRfkZL0tddeu+y///71ZByGwjHHHFOrEPO7mrA24dG73/3uWtGV3+nMWqfnyDXXXFN/h9PDpJEeVDvuuGP57Gc/W8OZwXL++eeXnXbaqZ5cpApt5ZVXroFQlmSmx1eeS5ad3HjjjeXss8+uwV7Tfy9BXSqn9thjjyGpusxS6J///Oflu9/9bq1Ya/qypBotS0mzHDo/QwLHvPYJ9/L633PPPfV783Mut9xy3UeD1zeVXwy1TKzk8znHmowF0zogmgmLfL0xsZVfmfz43Oc+V2abreeXfRwyxszxMcdzAJgYKr+ocmKaPl+Z3dtkk01qCLDxxhvXk9N3vetdNRxYeOGF6wlrZupS7fXII4/U7001SjLUnPimYgWGQtOrLn3otthii7LVVlvVICYBbn5/mwa9uZ4KpQQ2mY2OVFUlQMpywsEMktIX64Ybbqgz4Hm+ORnI7HaqudIQPv3JMvOdWfY0uk+lZarFIicimT3PezJN5AdTXr9U2uVkJoF4JPj+0pe+VLbddtvyvve9r8wwwwy9zYnz/2ajgfws6VuW3l/AK1R+MdTuvPPOcuCBB5Zjjz22jvESeuUzO5My+X/fZfkTW/mV7//85z9f3v/+99djx9guGYPq9QXApDB59/+8zmVgsc4665TddtutVsBkudKYloCl5LwJFzIYaqSKJs3FYagsuuiiZZdddim777572XzzzWtYlKqj/hKE5ev5PW5k2WOW8GXAP5gSGKd3V6q3En5ldntMEh4luEuT+Cw/bqQaM7taDrZUcKU6IBVpkQqvjTbaqFYDJKwDYGTJpiXp+5rWFjkWpZdrxoMJxDIpCgAjnfCLKiev2U0nA5xxzbAlAMuJeLadbmRW77nnnuteg8GXaqMvf/nL9XdzTKFXX5lJXnHFFUdrFp8Bf8KkwZRqtE9/+tM1bB7Xc87XswQ5fbMaqdRslh8PprvuuqtcfPHFtQIsy2Hy2n/84x8f9J5pAEwa2cUxVcepPm5Cr+23374eLwGgDYRfEyDb+qdHz2WXXVZ3wUlT0IMOOqheDj/88HpblgSlOmIgJ6ZZvpQeWocddlhtfp3dFpum8mk8mpPMH//4x/XxjzzyyLorXG7vK1UrmbHLfdKA+oEHHqi357Fzopqd2JrHP+WUU2qV1sScNKeHUt/KLxhJEiSlQmmwlwu2QT7/sjym+YzJa5im9tkwAICRKT21dt111/Ltb39b6AVAKwm/xkMCpzSobpp2Zme5bNefGbKvfOUr9ZI/Z+lVWql95zvfKWeeeeb/BFX95WTynHPOKV/96lfrJUFXmoMmYPvhD39YvvGNb5Sdd9659/H/7//+r/Y26it9gPL35T577713Dd9SxZIgbZ999qnPs3n8PL8EZGk6PaHS4yu9vmCkGom/wwnFm4b3kcq1wa62St+xNEJO1VekX1nCr3FVrgEwfGVzmLS00LsVgLYSfg3Qiy++WCuw0k8ouyKeeOKJtfLroYceqs2yG6m0St+gVGf94Ac/qPc9/fTTa8D1anICnu/LyWR6D+Xk9uabb65VWt///vfL1Vdf3RtUZXlhqi6apteNfH/zPHKfPK8LLrig7LfffuXkk08uDz74YO/j5+T1tttuG+0kenzlexPQNXISPhQ7zsGEaLZz79svK+HNtNNO2702/OQzIO/95jlnV8v0L0v4NJhSZZpgvpHdurIZBgAAwHAl/BqghFc33XRTbfCcECnL/lLt8IlPfKLujLjDDjuUL3zhC7Xp85JLLlnDoARN2QktyyIvv/zy7iON25NPPlmXJv70pz+tJ7zZNS0742RXtzTx7tunaEzy/LKrTpY5XnPNNfUkOc1Ls8PaEkssMVrD7An17LPP1hCtkZ3p0rwbRoKEt3mfNdVLkZ0VB7Lt+lBIFWeqTs8444ze55zga5VVVhn0XbASGiZcj3wWpQ+ZnbgAAIDhbIpvZn0e45TlRgm+UkGVbZ/T3Dk7xiX8ynbP2SkxTUKzbXP6JKRSLBVgCcASYKVJfL5vTEuDUql17bXXlquuuqpeT9CW780Jbxpipwn9Jz/5ybLaaqvVEGyRRRapAVvfsClbUF944YXlD3/4Q61qeeqpp8rvf//7GpzlBHmzzTarz3m55Zarpe0pa89lmmmm6T7CwOVnS2Vb+og1vcnSK2LjjTeu4RwMd/fcc0/tzddUMKXiK7s/rr322jUsHg4ScuX9nP58Z511Vt1+vlnuPOecc9adFfP5M5gVl/lsyedU+gtGQu/mcy+fc3ldM0mQZdepjM3nWq7nc7OpXs1nTprkA//19J9LufzeUu5+spSZe97SKy5QyqjZu1+EIXbLLbfUyZdGxqIZ+w5UxrmZlL3iiivq9RxzcyzI2DWTxM0l13Pcy/g3x4mMnQFgUpmsk8Y3jFMCnyw/zMlyQqwFFljgVXvcJPC66KKLyh577FEb2ccaa6xRd84ZNWpUvd5XljFleeMBBxzQveUVaSC93Xbb1RPccVVWpCpkp512qifKjQRf2ao6j5GKr0nVkydLJtNH7Oc//3m9nkFMgsC99tpLBQjDXt7LWQqcXnoJiSPvj/TwW3fddev1wZZgKJ8V2Zyi8c9//rM+vwRK6bGVP+c9nc+QhHQJxVPROZhSMZfl3Lvttlu9np0nE8Jl58xUmWZZZkL3VIU2YVd2EMtusgnr89xXXXXV+hma4Ax4xa2PlrLP2aWcflMpC89WytfXKmXjpbtfhCF2/PHH152JG/ncP+6447rXxi1tMpp+uTHllFPWcCvHub5SgZ0J5EzwZII2Eys5bvTd5RgAJpRljwOU2adUOHzpS18qiy666FiDpBzUE1ylOquRWay+/YXGJcuvNt1003qZkEAp1StZJpklmVnuOKmCr1SlpfKj7zLOVKetvvrqgi9GhPTLO/fcc3uDr4S3eY+kKnKoZAlmTiSajTNyySYV2b31vPPOq881zzMnARtuuGGtBB3s4Cv6N9zP50EqTpsNPlIZkAqBJviKpg9iKsGyW236IGZJ9/h8HgIwciXo6ltVnUni/sFXPPfcc3Ui6Je//GU9Vnz5y1+um0BlYijfAwATQ/j1GklYliqNRpYLvfTSS91rY5eT3CxxzAnuhO7klibY+f6c1E8q+RlSgZIlT01wkMArz3UogwMYqGbH1gQxkQH5YostVpctD2V4O5CdJxOqJ0jKUsIs2cwSkmbZ8VDJUpZszpFq0MzMZ+lollin/2HfPohZIjPVVFP19kFMBUA2Ahnq5w/Aay9LHHOsXXPNNeuYMcfcHCuaS44TH/nIR2qlVyZ2crzL8SLVxFkZkQ2g+m/0BADjS8+v10j/Pl5pCp3lPinn7q//fdPIOssIc/+B6tvzK3ISmpPP6aefvl6fFFK98aMf/aietCYIS7Pr/D3bbrvtGH8uGE4SHGU5cjaCaBq2zz333OUzn/lM7V0ylL2+En4lHGo2pmguqTKdY4456tLBLBt55JFHyu23315nxvMz5IQiy0MmVWXnuPT/rEp4mOWMWYaZk5f0/csy7fXWW68uuW76gaUXYHajfeyxx+oJTSrD8u+RUGy4bjIAg0nPL4azie35lTArx6r0oM1KgQ022KAunfzYxz5WLx/96Efr17JiIcflpudl/p9WBY8//ngdc773ve8dtOMdAO0j/JpAWe7zwAMP1CqGnIimH1gaeebEMJf0v8kl/W9ifMKvVG1lIDA+gVL/8CsnnDkRnVSyRClLlU444YR64tpUzHzuc58rK620Uh3YwHCVAXTep+lX1TTczY6t2QRi6623HvIlu6n2zPspvQH7XnIy8L73va9uKJEq0ARIqV5LcJQm8gnDEpilB+Fg6P9ZlerWnAClf1qCrjyXNOBvPg/y/zzvLANPZVhm7vOcI0teEnypGgXhF8PbxIZfkQmm9PTKjuM55vXVHCsSfOWYl2Na2gE0G0fl2JfVEzlODsWSfwDawbLH8ZTeXTl5PuKII2rT95z0pTfPjjvuOFq/njS7z46IbZCfOX2Hsttcc+Kaao/0I0v5ulk4hrNUKaZfyFFHHVUD4sgMcpqub7HFFsN6IJ0gKbu7ZpY8nymf//zny8ILL1y/lhOC7KR42mmnDVn/rJzA5CRlXK9hTmxyQpPPi0Yq2RKGDXQ5OADtl+NFKsAyudoc7yLjz0xiAcCEEn6NhyeeeKJWP2VXuL333ruccsoptbory48yK9VGCb4uuOCCGhyk90KkdD3LMrPMaUJ7ksFg6Bt8nXPOObUCLMFXKiO32mqr0TalGO6yY2KWFKais1nOnAqw9NxKNdZwl8+KLH9snnvCuzQ37tscHwASgCX46lsZnJUNWeUAABNK+DVAWWqU3Weyo9kll1xSw65UPaT/QE5Is6tiemw1l2222aZWOoxkTfCVHecS8kWCr1TLpE/SO97xjnobDEdN8JUqzYTWCVma4Gv77bevy/RGmgRgK664YllooYW6t5S6tPqGG27oXnttZSOPvoF3Gtbnc2KgskwyP0Oj/+6RABBpTZBlkI1M9jheADAxhF8DkJPonFz+5Cc/6Z11SgiUHWqyFGn//fcv3/3ud+uONM0llWEf/OAH631HovQ0S3PwvsFX+vPkZ06PJD0XGO7yXu0bfKXfSALpBF/ppzVSl+umX0o+fxrPP/987+6rr7Usw0x4leb8keArFbEDXbo42WST1Utj8sknrzP8ANBXNnqZlJs2AYDwawDS5DmN7bOdf6R6IVsy77rrrmXdddetuzP2b945kmV2LcuoEhw0wVdm4PKzZqmY4IvhLoFMliU3wVc2aEjT+FRojuTga0wS6qWibbAkAJtpppnqn7N08dlnn+3daGNsMomQf4tU0TayW2UaIANAX83kSiOTLgnEAGBCCb8GIH1p0mgz/YJijjnmqM2y2xgCNcHX4YcfPtqueGuvvXYNvrITJQxnGSyfdNJJ9dIEX+kdkua52UV1pAdfOSFIs/hGwqNUZQ6WVH713Yk2O3Ldc8893WuvLhVq9913X/03iUwY5DNU30AA+uvf4yvHOpOvAEwM4dcApLoh2/I3MvOU6oexGcylSJNKE3wdfPDB5dxzz61hXxN8bbfddiOqOTivT03wlQb3GTQ3wdcXv/jF2ih+OAUtCYGuuuqqct1119XeVwOR5cjZcv6OO+7o3lJq770FF1ywe+21lyWXiy66aPdaKQ888EC58sorx/ozpOorz/nqq6/u3vLKjrFLLLFE9xoAvCJ9dXNsbCZhIxPPjhkATAzh1wD0X5rTzEaNqc9NTvIefvjhcuaZZ9YT25FC8MVIN5KCr8hzPPTQQ8tee+1Vn3eqosYWICX4uvTSS8sZZ5zRWz2VJY9ZzjmY78+EbdnoI73H4umnny7nnXdeDcBe7TMxGw/kZ8zJTOR5L7bYYnXzAQDaK5PBGV9efvnloy17fzVpan/xxReXk08+uTz66KP1tozDE3wZiwIwMab4Zo/un3kVacqcE9XLLrusVoGlB1jCoVlnnbWGYtkBLdcTit14443l+OOPr/2G8j2N2Wefvay66qqjLRdq5PEyMGjCsrHd99Xk77rwwgt7e+/k5HSdddapfx6InJwm+Epol5+lCQ7S5ysnuwkWBnLJyXuq4vL9MFgSDJ199tl1g4bmfZfwNptOZInyiy++OMbf1/6XhEp5v+c9/VrL88wOstk9NtVcjz32WK0WTRCdStNc8nMlXLr55ptrKH3CCSfUkCmBUiywwAJ1OXJ2gBwsaVCf1yi7TN599931tiwNz/LHNLPvdDr1MyQnMI8//njtG5jNQk4//fTenSGH4nnDcPb0n0u5/N5S7n6ylJmnK2XFBUoZNXv3izAIMr7N53YuGZf2vfzud7+rx6BGqo1zbO17n4z/8vmfyY2+br/99rLffvuV0047rT52jmv5fyZLcqzI9+Z6jiE5pmSX8WOOOaYeGyO9vrJZTVoXqPwCYGJM1nOg6nT/zFgkmNp9991r5UVkFmrxxRcvK6ywQg2HcqKaE9ecxP72t7+tg4Asj3z55Zfrn5deeula4ZFm2/3l5DY7RB5wwAH1+tju+2rOP//8stNOO/Uuh8qOjEcffXT987jkRDozbDvssENvRUlOcLMsKQHY+HjPe95TtthiizLvvPN2b4HXXnpOZXB93HHHdW95ZVfE/P6OT0P1BLfpC7bJJpt0b3nt3HnnnWXfffet771GnvOoUaPqey8ba0ROFPLz5aSgeX9Glh+mgX9OCGaeeeburYMjYeJZZ51Vn3+zEUg+M/KccnKSvmAJyPJ885mU556TnBjK5w3D1a2PlrLP2aWcflMpC89WytfXKmXjpbtfhEHw0EMP1eApkxb9ZdOnX/3qV91rpVbuZnK0r0x65viVsWvGyI1MHO+88851bJzjRI4PuV8meDNJFRlDp5flvffeW8OyhGGRHp2pbv785z9fNt98cw3vAZg4Cb8Yt54DcafnJLWz5JJLdqaaaqoEhq96mXbaaTsrr7xyp+cEujP33HPX25ZeeunOeeed13200T311FOdXXbZpff7x3bfV5P7L7LIIr2PsfXWW3e/Mm49J9ed/fffv/d7J+by/ve/v3PRRRd1HxkGx1VXXdVZddVVx/g7OT6XnoF5p2eQ3X3U19Zzzz3XOeGEEzqrrLJK521ve9sYn8+YLvl8yWdE3rMPP/xw99EG3x//+MfOMcccM6DPxFyGy/OG4eiWRzqdDQ/vdKbsOXQvukenc8p13S/AIDn77LM788wzzxg/vwd6WWuttToPPvhg9xFfceedd3a22mqrzowzzjjG7xnTZfLJJ+/MMsssnbXXXrtz4okndl544YXuowHAhLPscYAy+5SKhVxS0p1LZqqaHj1TTz11bcaZRtA9B/+yzTbb1MqwLIPMcqZUcqy22mr1//3lMXK/LA9KpdjY7vtqshtlqtKydCvPbdllly1rrrlm96tjl1L3VKFkOVV+pomR5Uz5+bN0EwZLlvvm/TOQXQfHJpVfWcrxgQ98oHvLaycz2D0nGrU6LUuoZ5pppvr3p2Iqy0HyvozMpqdfWaop0+8k7+stt9yyrLfeenUGfahkaWieU9/PxDznVHjlcyyyo2PukyqBVAOkInWonzcMR5Y9MtRSoZvWF6k2nhA5duV4lmNU3x6bOVakyjfVYDnG5f85rvWcg/RWBEfG0dm5ODs6poI4lWVf+MIX6nh4pO/SDMDwYNnjeMrJXfoSNDuuNTs65mCek8CEPynnzoE+jTrTCDr9tFLenebxY9qmOUuIsgtaenblpHds93016b+TfgzpI5RBQnrpJIQaqCxdSk+e9O6ZGAn/Pvaxjw275uK0Wxrqpj9IGupOjCw7TPC13HLLdW8ZHAmds9QkSz4efPDB+hmT3a4iJwlZGpKgLJ8v880337B6f/X9TEz4mGXcTeP7LN3M51nz3C1zhDGz7JGhlvAr/Wqzg++EyJLGZZZZpmy66aZl+umn7976X+lnmYnaLGvM35HJ2qZPbeS4Nv/889exdJY6ZgLYMkcAJiXhFwDAEBJ+AQC8tibv/h8AAAAAWkf4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAK0l/AIAAACgtYRfAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAK0l/AIAAACgtYRfAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAwhKZ9UymzTFfKVFOUMn3Pn982bfcLAABMEpN1enT/DADAIHvxX6VcfV8pF95RyryzlLLeEqXMOkP3iwAATDThFwDAEMto7D8v9/y/58+pAAMAYNIRfgEAAADQWnp+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAK0l/AIAAACgtYRfAAAAALSW8AsAAACA1hJ+AQAAANBawi8AAAAAWkv4BQAAAEBrCb8AAAAAaC3hFwAAAACtJfwCAAAAoLWEXwAAAAC0lvALAAAAgNYSfgEAAADQWsIvAAAAAFpL+AUAAABAawm/AAAAAGgt4RcAAAAArSX8AgAAAKC1hF8AAAAAtJbwCwAAAIDWEn4BAAAA0FrCLwAAAABaS/gFAAAAQGsJvwAAAABoLeEXAAAAAC1Vyv8HhVbh1xp0uZYAAAAASUVORK5CYII=)

In this case also the subarray are not valid because 6 is not less than or equal to 4. Thus these are not the halves we were looking for. Let us try another combination.

![](data:image/png;base64,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1jYJFtiBvhJotVCaPafH1Xzzzdd5pO+yLSlbDA0cMPwl/E7fve222+51t80337z27Mu2joRX6V2Sfn1f/OIX61bEq666qte9+QZKTn666KKL6kS1qQTNNms9+QBGprTCyGFDTUCR1/4cVLT88svX+9BII/hUcOeE9yzkZ6th5jA5MCZbDgH6SqA1meQi8pe//GW9wEwD93POOaf2vGlu6S2TZs6TIhe3OfK3P9LAUo8saIds1dtpp53K9773vdfdTj755HLkkUfWwxwSbjXbDLOFOaHSoYceWm688cb62GB4+eWXayP4/NuRU1cTnCdAB2Bk+sUvflGuu+667p0Gee3PDoDZZput3uf1Mlb2PNUwi8vZfTHS5doorQjOPPPM7qb6OWU985fsPAGYFAKtAdasUuViMxeTOX0wjdrT72bHHXfsvuWxBF0AkypVTwmLttlmm3LYYYfVRvBNqJWtf+lRcdZZZ73uePHJJdumc1FzwQUXdDeCT1VZAi0ARqYcNJRt5rfeemu9n4qbVGetttpq9T7/LQ3ge/bNHbun1kiUFgS33XZbOfHEE+tif6RtSk4/Tk/gSW2hAiDQGkDPP/98vZjbf//965af73znO7WfQCq1EnQBTC6p4soppQm3mt4c2YZ477331pOEJresNl9zzTV1m2PMMccctX9KmsLntXFctzQRzkp1IyFcvk7z/kz68xgAw1P6IaUSOIeBRIKZbDUfqlN2B8NUU031ulMKE+r1Z54/9qmHI03CrCyw5XCbzBNi+umnLx/60Ifq4VY5tR1gUgm0BkguvNLg8Gtf+1q57LLL6sCW8uGFFlqovmBn9WGHHXbovm2xxRZlkUUW6Xw2QP8l1MqqeE4VbORiIydPTW5Zbb799tvLSy+9VO8niPr5z39ejj766PHeTjnllLpi20glWbYrNu///ve/331iFgDDS06rywEkPbe2Z/xJb8eR3KM11dEzzTRT595r2/yfe+65zr2Jy9a7nlsOU9GcViAjURNmHXXUUXXRP9tSE2atu+66Zdddd60nYQL0h0BrAGSrTV6sTz311LrlJnJhuckmm5T99tuvvoifdNJJtVlzc8tjCboABlJWx3O6VCMT7TRqn9wS4vec0D/yyCPlW9/6VjnkkEPGe/vf//3fcv3113c+o5Rnn3229hds3v/Nb37zde8HYPj47W9/W/sm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VhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFUEWgAAAAC0ikALAAAAgFYRaAEAAADQKgItAAAAAFpFoAUAAABAqwi0AAAAAGgVgRYAAAAArSLQAgAAAKBVBFoAAAAAtIpACwAAAIBWEWgBAAAA0CoCLQAAAABaRaAFAAAAQKsItAAAAABoFYEWAAAAAK0i0AIAAACgVQRaAAAAALSKQAsAAACAVhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFVGdY3ReRt67U9/+lN5/PHHy29/+9vy3HPPlZdeeqk+PvXUU5dZZpmlzDrrrGWuueYq73znO+vjMJz861//Kn/4wx/Kb37zm/L888/X3+c8NuWUU5a3vvWt3b/D+f19y1ve0vmsoZXn98c//rE888wz5Xe/+119++9//3t935vf/OYy44wzlne9611lttlmK9NOO219HBgZnvh9KUdcVspJ15Uyx4yl7LFOKZ9erfNOGCL//ve/61j061//+r/mgxlPMxZlPH3ve99b5phjjvK2t72tvm+o5XlnLL3jjjvKr371q/pc55133rLiiiv26Tnm+7355pvr1+ir97///WXllVcu008/fecRACaFQIteywQgF//33ntvue2228rdd99dnnjiiTqReeGFF+rHJAyYffbZ60C95JJLltVXX70sscQS5e1vf3t9PwylBEBPPfVUue+++8pdd91Vbw8//HCdiP/jH/8oo0ePriHWAgssUH9vl1lmmbLSSivVcGuoJMjKpDl/b7fffnu5//77yyOPPFK/j+bCIRPw973vfWXBBReszze3+eabb9iEcUD/CLQYbrKwcsstt9Tbgw8+WOeDGZcScEXG03e84x01zJpnnnnKWmutVdZff/0acA2lP//5z3U8veiii8pPfvKT8tBDD9Xnuskmm5TDDjusBm+9lc//whe+UL9GX6255prl0EMPrXNlACadQIte+ec//1lDgB/84AflyiuvrG/nsQlJuLXsssuWnXfeuU5ihFoMpRdffLHcdNNN9Xf46quvrkHsxMw555xlxx13LNtss00NjAZb/sYSYJ177rl14vzAAw903jN+We1dY401yic+8Ymy2mqrCbVgBBBoMVxkcTOLKhlLL7jggjpGTWw+GKussko55JBD6oLLUMjzTiXV5ZdfXp93Kqv+8pe/dN5bykc+8pFy5JFHlrnnnrvzyMSdeOKJZZdddunc65sVVlihfOUrX6njNQCTTqBFr2Rr1re//e1y7LHHdk8Asr3wPe95T5lpppnq6tZf//rXujqXrVyNPP6BD3yg7LXXXnWy8KY3vanzHhhcN9xwQ/09zGpyTDHFFDVkzWpxwtdmS9/vf//77q188e53v7vssMMOZddddx30Sq3HHnusTrBPPfXUWkGWv59sLcy2wummm65uk/jb3/5WnnzyyVpllu8h8ne36qqrlq9+9atlueWWq48B7SXQYjhIKJRqrOOPP76cc8453dVYqcRaeOGF68JPs4UuY1Pmg6nsT5CUBaIDDjhgSAKc7CK49dZby49//ONyySWXjHNBq7+BViqlU901wwwz1PsTs9RSS5VPfepTZf755+88AsCkEGjRKz//+c/rStIPf/jDOnFZdNFFu2+5yJ9qqqlqH6J83BVXXFG3Rr3yyiv1c3NxvcEGG9TS6vQogKFw+umnl+23376GQgmpFlpoobpFL5PwbDNMYJRANoHX9ddfX5599tnOZ5Y6Sc+2gp122qn+Pg+WVJLttttutTIr/bGyBTK3hMTN310uKLLSnAquPPcmcM5FRaq0DjrooBrYAe0l0GI4SO/ULG6edtppdezJwma26K+33np1C10znkYWOdOnKguiv/jFL8qoUaPqx6QlxWBJ5VgWhjI+pqIsWw3zWBaDMpYnoGsWgvobaCWYyuLX0ksvXe9PzMwzz1znxBnHAZh0Ux44RudtGK/0SkjfrAz+W221VfnkJz9Zttxyy1oyncE/DeAzqcnFdqpHUjGScCBeffXVktw0q3OLL754fQwGW7ZFJKjKNthtt922fPazny0bb7xxXSXNpDLh1vLLL1/Dopdffrn88pe/rP+N9NzIxD1bJgZz62z+jhJWJczKc064teGGG9a/uUyGm2qtfA/pUZJV8DzvSJVZgqxUaOVjgfZ6ccxL0c/G/Gnf+WQp009TygpjrrmXnqvzThgEGQcvvPDCcsIJJ9S+jgliMp7usccedVt+Ap1pphnzy9mR92cBNHO/jFG55f5gSgCX0Omkk06q/TIjY2a24+f5piK7WQRK38l11lmnT8/xzjvvLBdffHF9O0Fd5sfpFZY58cRuGZcTrAHQP1N0/gsTlG2FWb3ad9996+QlF/bjOpklk5k0gs8qVSYNjazQ9ab/D0wumWxm22AqDT/zmc/Uyey4+kvl41LZlN/jRlZws9I8KScZ9Ue29G6xxRbly1/+ctl9993Hu3KcleY0lt18881f93eZqslsRQSA/shWw1TpN9v1Mh5lrMzccFzzweEgjeqvvfbauiib5vR5rhlLMw/YeuutBz1gA2DgCbTolfQZ2nTTTevqU8KtCUmolSqXnmXXKT1vei3AUEilUgpSU1U4sUbpmagn0Or5cfkdbk7zHCxZMU4lWbZzTOw55/05YTST9kaCuGylBIBJlYrfO+64o/zsZz+r99MvKmPkhz70oWG9Za4ZF9dee+3uICsLWtkaaasfwMgg0JoMUpadfgHXXXddPZ0spc7f+ta36u24446rj914443l6aef7u4zNSGZSKQnVfoWHHPMMfWUwTTbjJRLX3PNNbVpdL5+SqvTdyeP95QqjfQPyMeceeaZtadA5GvnuOHzzjuv++ufffbZtZqqN89tfLLq1bNCC9okk+D0qLJVD4A3uswh0yO12Z7XLPo0/bKGq1Rcp/F6qpwFWQAjk0BrACVEuuyyy8rRRx9djybOAPrFL36xbtFL75vc8vbee+9dK0WOOOKI2o9g7PBpbAnI0tAyq0u5JbzKqTEJzdLLYP/9968Nq5uv/41vfKP2u+opRyzn38vHHHzwwTVQy3akhGM5CS3Ps/n6eX4JvfpTjZKeWemdBW2VBrZt62+Raqyex5AnmJt22mk79wCg77IImgqtRvpOtuEE3SxMpYosvb4EWQAjk0BrgKR5dCql9ttvv1rS/P3vf79WaKXnTs8LzFREpdFzqqiOPfbY+rHnn39+Da3GJ8FQPi8ns2QL0UsvvVTuueeeWk31zW9+s5aAN+FTtkWlz0ECrJ7y+c3zyMfkeV1++eXl61//ejnrrLNq48zm66c/wn333Vf/nUmVz03o1khD7cFspg39kcMPctx4z/5TmQz3bHg73OQ1JH/3zXPOaY7Zfphm8QAwKTIeZt7azCuz3TCVTzktGACGmkBrgORi8q677qonniQYypa7FVdcsTZpzomAn//852u5cxo8p3lzAp6ERynhzpbEnL7WW2lOnW2B55xzTg2ypptuurLYYovVEwbf97731a89IXl+t956a91imBPUcqGeHgNZbVtiiSXqyWn9lTCgaRwaKUvPSTfQBgl9n3322df1n0rT26z2Dkd5vj/96U9rON485zSUz+ENLjoAmFRZDM28s1kUzdhioQSA4WLKA7P3jX5LT6uEWal0WnXVVcsmm2xSj9lPoPXRj360nqyy5pprluWXX772HkhFV1a8EmollErlRz7vzW9+c+cr/kcuVm+55ZZy00031fsJz/K52TKYSUUatX/sYx+rTS8TbC200EI1NOsZIOUo/yuuuKKe9JLVtlys5/SXhGEf/OAH65HLec5pmJ3T3xZffPF6y7H/fZXvLRVo6cvV9PpacMEFy5ZbblkDNxjusr0iv7+pVIyExAmHNt5443H+jQ6FvHbkoIW85lx11VXllFNOqac5RXp/JTzffvvt69840G4vvlzKz35Zyp1PljL9NKWsMHcpS8/VeSdMRlmgzA6EzENjrrnmqtv4MsfMXDI9V9PmIq0sbrjhhvpxWazN6daZp6ZaOFVdw82jjz5a225kXhw5hGWdddbp08mHmfdffPHF9e3MDdJuI5Vs+Rk0t/wssisi7UXSyiDz/ba1MwAYzkaNefHt6rxNPyTEyda/9LVKMJX+AuO78M2FaC5ADzjggNrsPdZdd91y+OGH14aVY3vuuefq1sLDDjus88hrMvh+7nOfq6HZxE4eTG+vPffcs048GrnQXX/99evXSGXWQF2oJwRIX67/+7//q/czkUm4d9BBB030ecJQy/bcHE2+zz77dFcZJpBNr7qEskMhIfb999/ffZhD5Hlme2Eez6Q5zzUBdALznIqY49TzNtB+T/y+lCMuK+Wk60qZY8ZS9linlE+v1nknTEYJaA499NBy2mmn1fuZL+688861jUSCrLw/Cys9q7gy78uW94ReOfU6QVE+bzgFW5dcckntP5s2HZGF5yOPPLJP42YOYtpll13q26NHjy5TTDFF3QXRU77nVEqnwnuBBRaouymyeJxgMGEfAP1jy+EAyYpLKrByxP4iiywywXAog17CqFRRNbKKleCqt1LyvfXWW9fbpIRE2WaYQTXbIbPVcKDCrFx4p5Ks5xbKVJFlMiPMog1SuXjppZd2h1mpzsrfSioZh0qCq+OPP74Gw80tFxQ5eCKVZHmueZ6ZLKfa8tOf/rQwC4B+S6V95qiNBFc5OCgbPNLLNf1YU+3Us19s3s4J2hlLjzrqqNovNgFSz48ZCTJ3btp8ZLF67DAr8j3n55O2ABnHsziWRer02R1pPw+AoSDQGiIJwHpuBco2wFdeeaVzb8Ky2pPthdlmmL4+kyINPfP5A3lKTb6Hu+++u/zgBz+oZeiRECvPNatRMNy9+OKLdbtstudGVlsTEm2wwQblXe96V31sKORgiImdGpoTDbPam4uIVGTee++9tYoLAAZK5ndZuMxCS1pUZPvhDjvsUHvF5vapT32qbLjhht2LKgltEubkBPBsSRxJ8v1na/9mm21WF5p23XXX7p9DFrjzc8lOiFR5N8FXtmLm4KiEWtmm2du5PwDjpofWEBm7L1ZKkVdbbbVxVlWM/bEpU87AmY/vrZ49tGL11VevA+5AHumfvl7f+c53amPqhFsZvPPvpBxbtQjDXVZWM9nOinNzmlO2CeRvLX3qBqqKcVLk7ynN3hOCL7root23bG1Ov6w8t/TnSJ+OhMp5rXjqqae6G9k7rhzaTQ8thkp2D6SaKIslkbld2mNstNFGdWzMbdNNN609JtM+I3PT7EDI+Jlx6emnn64LMpl/ZofCsssuOyy2Hg5ED60ceJTvJxXcCfbyM0mAlZ9DFnPTe3PppZeuC2NZyM6/lZ0MmW+k0i0/l4zlA3EYE8AblQqtySQDVvblp9rj3HPPrScZfutb3+q+5f4dd9zR+ei+yUXtLLPM0rk3aRJkDeQWwEx40nfowgsvrAN1Gl6mOX16Do2rLxgMJ9kqkF5U3/ve92p4HPkbyeQ2v8MDGfxOilSHZYvhGWec8bpbAuSs8u677771giKVl5Fm8flb/PrXv94dhANAf2WRZLvttqtb3rPFPQcIJdhppJdj5n+pXMqCZnNAUSqG0yA9jdRHilRGJ7jLgUcZp3suHiW8y88lhzUl9Ntvv/3qzohm/p7KtfTeTZUWAJNOoDXA0mcgVR7ZJ5/G6Nkr/8UvfrHsscceZbfdduu+pSF8wq6RIN9z+iSkYWiqQiITmPT3ygrVUFa2wMSk+inN1nNKYKoLI7+z2Y674447DuvqwgRtuZhIFVkOlUjvrCbUSkiXC4ezzjqrrpIDQH+lmihb6HqGWOOSYCvj6EorrdR55LXtitkx8EaU0CsB4Morr9x5pNT+l3fddVf3ieAA9J1AawCln8A555xTV60OPvjgcvbZZ5ebb765bgMaqY0fE2alIWgqzpqTYnKyTS6wt9hii0nu8QWDIWFWmsB/97vfrb3fsq0vYVZCoo9//OOvm3gOd1kdToicv71mO0dWxNNLK6vAADCYMi41iyyR6uFstXujys8iWxAbGaMT8r3wwgudRwDoK4HWAEkFxI9+9KNyxBFHlGuvvbYGWLmozHHFm2++eT1NsGkUmVu2Dy211FKdz26nJszKFsoEd5EwK00wU9mSMmwYrpowK9v2cktviybM+tznPleb2rZNLh7SvyT9OhoJ1JttlADQF2MfYpRqorTV6I23v/3tr+sPlblxQq03qlStzTbbbK/7maRNhwotgEkn0BoAuTBOP6xUeTSl1Al2UlqcrYWHHnpoOfLII2uvm+aWCq411lijfmwbZTJz1VVXvS7Mes973lO/55122qnMPvvs9TEYrnLSUM8wKycEpt9bwqxNNtmk9sZoo2wDydaGRk5uzLYGAOirsfu2JpDKjoTeGDVqVL010l81vaXeyNJnqznxEID+E2gNgJxCmEaX9913X72fwT+nneyzzz61yiOnEg6HE10GSkqkU/GRPmFNmJVTYfK9fuITnxBmMeylovK8887rDrOmmGKKuhUgYWybw6xxSVA3kr4fAAZPqopmmGGGzr3XAq0sCL3yyiudR8bvpZdeel0Px1RsTaz31kiWBfD8PJ5//vnOI6+N0XrNAkw6gdYAyOCeZugpG46UE6+66qojMthpwqzjjjuuNr+PhFkbbLBBDbN69kqA4SiTyZzImYrKJsxK6Jxtsptttlnrw58E7H/4wx86915rHJ/qSQDoq7G3yWXb4OOPP157P01MKrkefvjhzr3/7qn1RpMgKzs5muuFVGvlxPHMowGYNAKtAZDTxNJMupEL4qxCTUi2AfVmMjCcNGHWUUcdVS655JI6IDdhVrZpLbnkkp2PhOGpCbOOOeaY8sADD3SHWelxl0C2Z1+LoZZtvffcc09t6p6/vd54+eWXy/33318/p5GtIvPPP3/nHgD0TcbJJZZYonOv1JBqYoeNZNzKGHb77bd3Hil1oTdb+9+Imjn0T3/6084jr7XqWHTRRWtoCMCkEWgNgLHLsVP1kRWYcZVjp9z4ySefLBdeeGG56aabOo8Of8Is2q5NYVY89thjtUfdgQceWC644IL6ujGhYCth1q233lo/Nq9Bka0M88wzz+tOVQKAvkhfxowjTf+rzHEz1vSsvuopY1VaUpx11ll1LIvMGXMY0rzzzlvvt1kqoRPoZU6RarWJbb/Mx9944421MrxpT5LqrBwctdJKK9X7AEyaKcdcLB3YeZtJlAvjDO7XXXddrdbKwJXAJ6XVCbpyQkzu5yLzzjvvLKeffno5++yzuxvIx6yzzlpPJ5t77rk7j/xHvl7CpCYAm9DHjk/+rSuuuKL7QjeD6Ec+8pH6dm889NBDNcxKEJfvJY09c5Ja+mblNMOUlffmlpNcUr2Wz4fBkrAnJ3IefvjhNcyKbMVba6216u/wq6++Wv82JnZLZWX+3gejoWv+Zs8555x6+EJeN5p/PxPn3PJ3mNeGHPedi4qcrprJcr7PBOcxxxxzlO23376svfba9T7QTi++XMrPxkwZ7nyylOmnKWWFMcP/0nN13gmTWXYeZP6WMCbb5jLXzSJRxqXIGJpxKeNRTg++5pprysknn1zHr4xHmfMluNlll13qQtJgyb+dPl55Xql67nnLXCDjZt4Xc845Zw3c8lx7fly+xtitCNJD7IQTTqjfY1qOZMdFxueMy/k55PNy/5lnnqkV05deemkdn6+++ur6MbHgggvWE89XWWUVc2KAfhjVNUbnbfohYdN+++3XXUqcqq3FFlusDuAJfLIlMQNeBraUX2dikAEyk4C8vcwyy5SDDjqorLvuuvXze3ruuefqyYiHHXZYvT+hjx2fyy67rOy5557dF/Npfp2BuDcymGeV7fOf/3z3wJ9Vugz+CbX6YvHFFy877LDD605hg8ktK8T5++n5O5/GtPkbTf+K3srhDuuss07ZdNNNO49MPgmRDznkkHLmmWd2HnntOacaMmF203Mjk/X8Xee1pbm4iJlnnrlst912Zffdd6+vQUB7PfH7Uo64rJSTritljhlL2WOdUj69WuedMAgyF00okyrnp59+uj6WeWx6YmUszfiUuW4+LsFXU5mVsCbhzW677Va23nrrWpk0WBIoZZHn7rvv7jzyHwneUjWVPriReenKK69cD3bqKVv2swCcxeTGgw8+WMfnzI1j+umnL/PNN1/9WTRN7zN3/tOf/lQruDKeN/9Ofh4ZwxPuZT6czwWgHxJo0X9jLiq7xgxsXWMuNrve9KY3JSQc723MRXHXqquu2rXVVlt1zTHHHPWxZZZZpuvSSy/tfLXXe/bZZ7v23nvv7s+f0MeOTz5+oYUW6v4aO+20U+c9E/fnP/+569BDD+3+3P7cll9++a6rrrqq85VhcNx2221da6211jh/J/tyGz16dNfOO+/c+aqT1wsvvNB16qmn1r/3MRPecT6fcd2mnnrq+ree14xHH32089WANnv8d11dnzmjq2v0mKH7/Xt3dR13TecdMIgee+yxrgMOOKBr7rnnHuf4M/btHe94R9d6663Xddppp3X98Y9/7HyVwXPzzTf3e+xfccUVu6655vV/cJmXZ14866yzjvNzxndrfh6nnHJK1+9+N+aPGoB+s+VwgOTI3fe+9731ltWn3LJSleqryBalnBKzyCKLlPXXX7+WGWdFK1uJUrqcaqdsC8p/x5avkY9LP4JUdE3oY8cnJdGpHsu2vzy35ZZbrowZVDvvnbCUlmc1KitZPZvfT4r0Tsj333OlCya3bJHIqZyPPPJI55FJk7/j5ZdfvlZpTW75t7Lam9XhbI/MVt1Ufo4aNar+TeYW2QKZyrG8vqRiMiespifYtttuWx8D2s+WQ4aDtNHIPC5VSKk0Sp/GVCI1c908loqjjF3ZTbDRRhvV+W7mrEPR+Dzz62wrTJXUpErlVp5/z5PLU5mWKugcupL+m/m5ZMwec13V/bOIPJYK6VRk5eeRSq/8PDKHmNjhUQD0ji2HAywXmc2e+WwDak4yzECesCsTgZzwkm1Ov/71r+u++pQiZ7BLg/WeA2Yj/X/SfDI9sLI3f0IfOz4prU4z9/TlSfiWsuoES72V8vHzzz+/u2R6UiXQ23jjjZVYM6iyVTZ/a7n1Rybx+btJ763BlAa7CaVzgmFCubydrYaR7b+ZUDevLQnAhluDe6B/bDlkOMmYlJAoY1L+m22GkUAr2+HTJyvbDDNfHYogq5HndeWVV9ZF4UmVhaLMuce1dT9z/iyYZVxOeJZb87OIfO85yTC3jNHpazmUPw+AkUigBQAwjAm0AAD+2xSd/wIAAABAKwi0AAAAAGgVgRYAAAAArSLQAgAAAKBVBFoAAAAAtIpACwAAAIBWEWgBAAAA0CoCLQAAAABaRaAFAAAAQKsItAAAAABoFYEWAAAAAK0i0AIAAACgVQRaAAAAALSKQAsAAACAVhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFUEWgAAAAC0ikALAAAAgFYRaAEAAADQKgItAAAAAFpFoAUAAABAqwi0AAAAAGgVgRYAAAAArSLQAgAAAKBVBFoAAAAAtIpACwAAAIBWEWgBAAAA0CoCLQAAAABaRaAFAAAAQKsItAAAAABoFYEWAAAAAK0i0AIAAACgVQRaAAAAALSKQAsAAACAVhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFUEWgAAAAC0ikALAAAAgFYRaAEAAADQKgItAAAAAFpFoAUAAABAqwi0AACGsbe9uZR3TVfKlGNmbc3bAABvdKO6xui8DQDAMHTHr0o57ppS5pmllB1XEmoBAAi0AABaIDO2UaM6dwAA3uBsOQQAaAFhFgDAfwi0AAAAAGgVgRYAAAAArSLQAgAAAKBVBFoAAAAAtIpACwAAAIBWEWgBAAAA0CoCLQAAAABaRaAFAAAAQKsItAAAAABoFYEWAAAAAK0i0AIAAACgVQRaAAAAALSKQAsAAACAVhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFUEWgAAAAC0ikALAAAAgFYRaAEAAADQKgItAAAAAFpFoAUAAABAqwi0AAAAAGgVgRYAAAAArSLQAgAAAKBVBFoAAAAAtIpACwAAAIBWEWgBAAAA0CoCLQAAAABaRaAFAAAAQKsItAAAAABoFYEWAAAAAK0i0AIAAACgVQRaAAAAALSKQAsAAACAVhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFUEWgAAAAC0ikALAAAAgFYRaAEAAADQKgItAAAAAFpFoAUAAABAqwi0AAAAAGgVgRYAAAAArSLQAgAAAKBVBFoAAAAAtIpACwAAAIBWEWgBAAAA0CoCLQAAAABaRaAFAAAAQKsItAAAAABoFYEWAAAAAK0i0AIAAACgVQRaAAAAALSKQAsAAACAVhFoAQAAANAqAi0AAAAAWkWgBQAAAECrCLQAAAAAaBWBFgAAAACtItACAAAAoFUEWgAAAAC0SCn/H3bj7R7WRiYtAAAAAElFTkSuQmCC)

It can be observed that in this combination of elements, 4<=6 and 3<=7. This means that all the elements on the right half are smaller than or equal to all the elements on the left half. Thus, this is the valid merged array that is the one we were looking for.

Thus, we checked the extreme elements of both the subarray to match the condition of a merged and sorted array. In the right half of the merged array, last element of arr1 is denoted by l1 and last element of arr2 is denoted by l2. In the left half of the merged array, first element of arr1 is denoted by r1 and first element of arr2 is denoted by r2. Therefore, the checking condition can be written as: ((l1 <= r2) and (l2 <=r1))

The mean of the merged array will be: (max(l1, l2) + min(r1, r2))/2

Now, to implement this approach to median of two sorted arrays using binary search, we just need to figure out where to make the partition in the arrays such that the checking condition is valid. We will find the partition using binary search by checking the condition for the extreme elements for each iteration. As per the binary search algorithm, the lower index will move downwards if the required element for partition should be smaller or it will move upwards if the required element for partition is larger.

##### Implementation in C++:

```cpp
class Solution {
    public:
        double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
            if(nums2.size() < nums1.size()) return findMedianSortedArrays(nums2, nums1);
            int n1 = nums1.size();
            int n2 = nums2.size(); 
            int low = 0, high = n1;
            
            while(low <= high) {
                int cut1 = (low+high) >> 1;
                int cut2 = (n1 + n2 + 1) / 2 - cut1; 
                
            
                int left1 = cut1 == 0 ? INT_MIN : nums1[cut1-1];
                int left2 = cut2 == 0 ? INT_MIN : nums2[cut2-1]; 
                
                int right1 = cut1 == n1 ? INT_MAX : nums1[cut1];
                int right2 = cut2 == n2 ? INT_MAX : nums2[cut2]; 
                
                
                if(left1 <= right2 && left2 <= right1) {
                    if( (n1 + n2) % 2 == 0 ) 
                        return (max(left1, left2) + min(right1, right2)) / 2.0; 
                    else 
                        return max(left1, left2); 
                }
                else if(left1 > right2) {
                    high = cut1 - 1; 
                }
                else {
                    low = cut1 + 1; 
                }
            }
            return 0.0; 
        }
    };
```

##### Implementation in JAVA:

```java
class Solution {
        public double findMedianSortedArrays(int[] nums1, int[] nums2) {
            if(nums2.length < nums1.length) return findMedianSortedArrays(nums2, nums1);
            int n1 = nums1.length;
            int n2 = nums2.length; 
            int low = 0, high = n1;
            
            while(low <= high) {
                int cut1 = (low+high) >> 1;
                int cut2 = (n1 + n2 + 1) / 2 - cut1; 
                
            
                int left1 = cut1 == 0 ? Integer.MIN_VALUE : nums1[cut1-1];
                int left2 = cut2 == 0 ? Integer.MIN_VALUE : nums2[cut2-1]; 
                
                int right1 = cut1 == n1 ? Integer.MAX_VALUE : nums1[cut1];
                int right2 = cut2 == n2 ? Integer.MAX_VALUE : nums2[cut2]; 
                
                
                if(left1 <= right2 && left2 <= right1) {
                    if( (n1 + n2) % 2 == 0 ) 
                        return (Math.max(left1, left2) + Math.min(right1, right2)) / 2.0; 
                    else 
                        return Math.max(left1, left2); 
                }
                else if(left1 > right2) {
                    high = cut1 - 1; 
                }
                else {
                    low = cut1 + 1; 
                }
            }
            return 0.0; 
        }
    }
```


##### Analysis of the algorithm:

This solution to median of two sorted arrays uses binary search, so the time complexity for this code is O(log n) where ‘n’ is the total number of elements in the final merged array. This time complexity can also be O(1) for the best case that is, if we find the partition right away with the middle element. And the binary search space complexity is O(1) because it uses no additional data structure.

**Also Read: [How to Reverse an Array](https://codewithgeeks.com/how-to-reverse-an-array/)**

### Conclusion:

This problem is an extension of median of arrays of equal size problem. It can be solved by a simpler approach if we directly merge the arrays while keeping the final array sorted. But the more efficient approach would be to use binary search because it uses no extra space and the time complexity is also significantly low.

