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
-   `-106 <= nums1[i], nums2[i] <= 106`

