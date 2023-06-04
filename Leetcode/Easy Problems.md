## [58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/description/)[👍]

Given a string `s` consisting of words and spaces, return _the length of the **last** word in the string._

A **word** is a maximal 

substring

 consisting of non-space characters only.

**Example 1:**

**Input:** s = "Hello World"
**Output:** 5
**Explanation:** The last word is "World" with length 5.

**Example 2:**

**Input:** s = "   fly me   to   the moon  "
**Output:** 4
**Explanation:** The last word is "moon" with length 4.

**Example 3:**

**Input:** s = "luffy is still joyboy"
**Output:** 6
**Explanation:** The last word is "joyboy" with length 6.

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of only English letters and spaces `' '`.
- There will be at least one word in `s`.

### Solution

```java
class Solution {

    public int lengthOfLastWord(String s) {

        int length = 0;

        // We are looking for the last word so let's go backward

        for (int i = s.length() - 1; i >= 0; i--) {

            if (s.charAt(i) != ' ') { // a letter is found so count

                length++;

            } else {  // it's a white space instead

                //  Did we already started to count a word ? Yes so we found the last word

                if (length > 0) return length;

            }

        }

        return length;

    }

}
```



## [169. Majority Element](https://leetcode.com/problems/majority-element/description/)[👍]

### Approach 1: Brute Force

#### Intuition

We can exhaust the search space in quadratic time by checking whether each  
element is the majority element.

#### Algorithm

The brute force algorithm iterates over the array, and then iterates again  
for each number to count its occurrences. As soon as a number is found to  
have appeared more than any other can possibly have appeared, return it.

#### Implementation

#### Complexity Analysis

- Time complexity : O(n2)O(n^2)O(n2)
    
    The brute force algorithm contains two nested `for` loops that each run  
    for nnn iterations, adding up to quadratic time complexity.
    
- Space complexity : O(1)O(1)O(1)
    
    The brute force solution does not allocate additional space proportional  
    to the input size.
    

  

---

### Approach 2: HashMap

#### Intuition

We know that the majority element occurs more than ⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋  
times, and a `HashMap` allows us to count element occurrences efficiently.

#### Algorithm

We can use a `HashMap` that maps elements to counts in order to count  
occurrences in linear time by looping over `nums`. Then, we simply return the  
key with maximum value.

#### Implementation

#### Complexity Analysis

- Time complexity : O(n)O(n)O(n)
    
    We iterate over `nums` once and make a constant time `HashMap` insertion  
    on each iteration. Therefore, the algorithm runs in O(n)O(n)O(n) time.
    
- Space complexity : O(n)O(n)O(n)
    
    At most, the `HashMap` can contain n−⌊n2⌋n - \lfloor \dfrac{n}{2} \rfloorn−⌊2n​⌋  
    associations, so it occupies O(n)O(n)O(n) space. This is because an arbitrary  
    array of length nnn can contain nnn distinct values, but `nums` is  
    guaranteed to contain a majority element, which will occupy (at minimum)  
    ⌊n2⌋+1\lfloor \dfrac{n}{2} \rfloor + 1⌊2n​⌋+1 array indices. Therefore,  
    n−(⌊n2⌋+1)n - (\lfloor \dfrac{n}{2} \rfloor + 1)n−(⌊2n​⌋+1) indices can be occupied by  
    distinct, non-majority elements (plus 1 for the majority element itself),  
    leaving us with (at most) n−⌊n2⌋n - \lfloor \dfrac{n}{2} \rfloorn−⌊2n​⌋ distinct  
    elements.
    

  

---

### Approach 3: Sorting

#### Intuition

If the elements are sorted in monotonically increasing (or decreasing) order,  
the majority element can be found at index  
⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋ (and also at ⌊n2⌋−1\lfloor \dfrac{n}{2} \rfloor - 1⌊2n​⌋−1, if nnn is even).

#### Algorithm

For this algorithm, we simply do exactly what is described: sort `nums`, and  
return the element in question. To see why this will always return the  
majority element (given that the array has one), consider the figure below  
(the top example is for an odd-length array and the bottom is for an  
even-length array):

![Sorting middle index overlap](https://leetcode.com/problems/majority-element/Figures/169/sorting.png)

For each example, the line below the array denotes the range of indices that  
are covered by a majority element that happens to be the array minimum. As  
you might expect, the line above the array is similar, but for the case where  
the majority element is also the array maximum. In all other cases, this line  
will lie somewhere between these two, but notice that even in these two most  
extreme cases, they overlap at index ⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋ for both  
even- and odd-length arrays. Therefore, no matter what value the majority  
element has in relation to the rest of the array, returning the value at  
⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋ will never be wrong.

#### Implementation

#### Complexity Analysis

- Time complexity : O(nlgn)O(nlgn)O(nlgn)
    
    Sorting the array costs O(nlgn)O(nlgn)O(nlgn) time in Python and Java, so it  
    dominates the overall runtime.
    
- Space complexity : O(1)O(1)O(1) or (O(n)O(n)O(n))
    
    We sorted `nums` in place here - if that is not allowed, then we must  
    spend linear additional space on a copy of `nums` and sort the copy  
    instead.
    

  

---

### Approach 4: Bit Manipulation

#### Intuition

If an element `majority_element` occurs more than ⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋ times, then there are at least ⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋ elements of identical values with `num` at each bit. That is, we can reconstruct the exact value of `num` by combining the most frequent value (0 or 1) at each bit.

#### Algorithm

Starting from the least significant bit, we enumerate each bit to determine which value is the majority at this bit, 0 or 1, and put this value to the corresponding bit of the result. Finally, we end up with the most least significant bit of all elements and return the result.

#### Implementation

Because all numbers are in the range [−109,109][-10^9, 10^9][−109,109], which can be represented in 32-bit, we only need to enumerate 32 bits.

For Python solution, notice that the sign of an integer is not represented in its bits. To check if the majority element is positive or negative, we need to figure out the majority sign additionally.

#### Complexity Analysis

- Time complexity : O(nlog⁡C)O(n\log{C})O(nlogC)
    
    CCC is the max absolute value in `nums`, i.e., 10510^5105 in this problem. We enumerate all log⁡C\log{C}logC bits for each number in `nums`.
    
- Space complexity: O(1)O(1)O(1)
    
    We count the majority of each bit in O(1)O(1)O(1) space as it only has the two potential values, 0 and 1. After that, we only need to put the majority values to their corresponding bit in the returned result, and no extra space is used.
    

---

### Approach 5: Randomization

#### Intuition

Because more than ⌊n2⌋\lfloor \dfrac{n}{2} \rfloor⌊2n​⌋ array indices are occupied  
by the majority element, a random array index is likely to contain the  
majority element.

#### Algorithm

Because a given index is likely to have the majority element, we can just  
select a random index, check whether its value is the majority element,  
return if it is, and repeat if it is not. The algorithm is verifiably correct  
because we ensure that the randomly chosen value is the majority element  
before ever returning.

#### Implementation

#### Complexity Analysis

- Time complexity : O(∞)O(\infty)O(∞)
    
    It is technically possible for this algorithm to run indefinitely (if we  
    never manage to randomly select the majority element), so the worst  
    possible runtime is unbounded. However, the expected runtime is far  
    better - linear, in fact. For ease of analysis, convince yourself that  
    because the majority element is guaranteed to occupy _more_ than half of  
    the array, the expected number of iterations will be less than it would  
    be if the element we sought occupied exactly _half_ of the array.  
    Therefore, we can calculate the expected number of iterations for this  
    modified version of the problem and assert that our version is easier.
    
    EV(itersprob)≤EV(itersmod)=lim⁡n→∞∑i=1ni⋅12i=2\begin{aligned} EV(iters_{prob}) &\leq EV(iters_{mod}) \\ &= \lim_{n\to\infty} \sum_{i=1}^{n} i \cdot \frac{1}{2^i} \\ &= 2 \end{aligned}EV(itersprob​)​≤EV(itersmod​)=n→∞lim​i=1∑n​i⋅2i1​=2​
    
    Because the series converges, the expected number of iterations for the  
    modified problem is constant. Based on an expected-constant number of  
    iterations in which we perform linear work, the expected runtime is  
    linear for the modifed problem. Therefore, the expected runtime for our  
    problem is also linear, as the runtime of the modifed problem serves as  
    an upper bound for it.
    
- Space complexity : O(1)O(1)O(1)
    
    Much like the brute force solution, the randomized approach runs with  
    constant additional space.
    

  

---

### Approach 6: Divide and Conquer

#### Intuition

If we know the majority element in the left and right halves of an array, we  
can determine which is the global majority element in linear time.

#### Algorithm

Here, we apply a classical divide & conquer approach that recurses on the  
left and right halves of an array until an answer can be trivially achieved  
for a length-1 array. Note that because actually passing copies of subarrays  
costs time and space, we instead pass `lo` and `hi` indices that describe the  
relevant slice of the overall array. In this case, the majority element for a  
length-1 slice is trivially its only element, so the recursion stops there.  
If the current slice is longer than length-1, we must combine the answers for  
the slice's left and right halves. If they agree on the majority element,  
then the majority element for the overall slice is obviously the same[1](https://leetcode.com/problems/majority-element/editorial/#user-content-fn-1). If  
they disagree, only one of them can be "right", so we need to count the  
occurrences of the left and right majority elements to determine which  
subslice's answer is globally correct. The overall answer for the array is  
thus the majority element between indices 0 and nnn.

#### Implementation

#### Complexity Analysis

- Time complexity : O(nlgn)O(nlgn)O(nlgn)
    
    Each recursive call to `majority_element_rec` performs two recursive  
    calls on subslices of size n2\frac{n}{2}2n​ and two linear scans of length  
    nnn. Therefore, the time complexity of the divide & conquer approach  
    can be represented by the following recurrence relation:
    
    T(n)=2T(n2)+2nT(n) = 2T(\frac{n}{2}) + 2nT(n)=2T(2n​)+2n
    
    By the [master theorem](https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms)),  
    the recurrence satisfies case 2, so the complexity can be analyzed as such:
    
    T(n)=Θ(nlogbalog⁡n)=Θ(nlog22log⁡n)=Θ(nlog⁡n) \begin{aligned} T(n) &= \Theta(n^{log_{b}a}\log n) \\ &= \Theta(n^{log_{2}2}\log n) \\ &= \Theta(n \log n) \\ \end{aligned}T(n)​=Θ(nlogb​alogn)=Θ(nlog2​2logn)=Θ(nlogn)​
    
- Space complexity : O(lgn)O(lgn)O(lgn)
    
    Although the divide & conquer does not explicitly allocate any additional  
    memory, it uses a non-constant amount of additional memory in stack  
    frames due to recursion. Because the algorithm "cuts" the array in half  
    at each level of recursion, it follows that there can only be O(lgn)O(lgn)O(lgn)  
    "cuts" before the base case of 1 is reached. It follows from this fact  
    that the resulting recursion tree is balanced, and therefore all paths  
    from the root to a leaf are of length O(lgn)O(lgn)O(lgn). Because the recursion  
    tree is traversed in a depth-first manner, the space complexity is  
    therefore equivalent to the length of the longest path, which is, of  
    course, O(lgn)O(lgn)O(lgn).
    

  

---

### Approach 7: Boyer-Moore Voting Algorithm

#### Intuition

If we had some way of counting instances of the majority element as +1+1+1  
and instances of any other element as −1-1−1, summing them would make it  
obvious that the majority element is indeed the majority element.

#### Algorithm

Essentially, what Boyer-Moore does is look for a suffix sufsufsuf of `nums`  
where suf[0]suf[0]suf[0] is the majority element in that suffix. To do this, we  
maintain a count, which is incremented whenever we see an instance of our  
current candidate for majority element and decremented whenever we see  
anything else. Whenever `count` equals 0, we effectively forget about  
everything in `nums` up to the current index and consider the current number  
as the candidate for majority element. It is not immediately obvious why we can  
get away with forgetting prefixes of `nums` - consider the following  
examples (pipes are inserted to separate runs of nonzero `count`).

[7, 7, 5, 7, 5, 1 | 5, 7 | 5, 5, 7, 7 | 7, 7, 7, 7]

Here, the `7` at index 0 is selected to be the first candidate for majority  
element. `count` will eventually reach 0 after index 5 is processed, so the  
`5` at index 6 will be the next candidate. In this case, `7` is the true  
majority element, so by disregarding this prefix, we are ignoring an equal  
number of majority and minority elements - therefore, `7` will still be the  
majority element in the suffix formed by throwing away the first prefix.

[7, 7, 5, 7, 5, 1 | 5, 7 | 5, 5, 7, 7 | **5, 5, 5, 5**]

Now, the majority element is `5` (we changed the last run of the array from  
`7`s to `5`s), but our first candidate is still `7`. In this case, our  
candidate is not the true majority element, but we still cannot discard more  
majority elements than minority elements (this would imply that `count` could  
reach -1 before we reassign `candidate`, which is obviously false).

Therefore, given that it is impossible (in both cases) to discard more  
majority elements than minority elements, we are safe in discarding the  
prefix and attempting to recursively solve the majority element problem for the  
suffix. Eventually, a suffix will be found for which `count` does not hit  
`0`, and the majority element of that suffix will necessarily be the same as  
the majority element of the overall array.

#### Implementation

#### Complexity Analysis

- Time complexity : O(n)
    
    Boyer-Moore performs constant work exactly nnn times, so the algorithm  
    runs in linear time.
    
- Space complexity : O(1)
    
    Boyer-Moore allocates only constant additional memory.
    

  

### Footnotes

### Footnotes

1. This is a constant optimization that could be excluded without hurting our  
    overall runtime. [↩](https://leetcode.com/problems/majority-element/editorial/#user-content-fnref-1)

### [Original Solution Link]([https://leetcode.com/problems/majority-element/solution/](https://leetcode.com/problems/majority-element/solution/))

## [283. Move Zeros](https://leetcode.com/problems/move-zeroes/description/)[👍]
Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

**Example 1:**

**Input:** nums = [0,1,0,3,12]
**Output:** [1,3,12,0,0]

**Example 2:**

**Input:** nums = [0]
**Output:** [0]

**Constraints:**

- `1 <= nums.length <= 104`
- `-231 <= nums[i] <= 231 - 1`

**Follow up:** Could you minimize the total number of operations done?

### Solution1
use bubble sort like algorithm and move zeros to the end.
#### Code
```java
class Solution {

    public void moveZeroes(int[] nums) {

        for(int i = 0; i < nums.length - 1; i++){

            for(int j = i + 1; j< nums.length; j++){

                if(nums[i] == 0){

                    swap(nums, i, j);

                } else {

                    break;

                }

            }

        }

    }

  

    static void swap(int[] array, int idx1, int idx2){

        if(idx1 == idx2 || array[idx1] == array[idx2]) return;

        int temp = array[idx1];

        array[idx1] = array[idx2];

        array[idx2] = temp;

    }

}
```


### Solution2
#### Practise Questions

**Q1) Move All Zeros to End of an Array**  
You have been given a random integer array of size N. You have been required to push all the zeros that are present in the array to the end of it such that the relative order of the non-zero elements should be maintained.

```java
Sample Input/Output
​Input:  arr[]={3,0,1,5,0,5}
Output: arr[]={3,1,5,5,0,0}
```

#### [Approach](https://utkarsh1504.github.io/DSA-Java/practise-question#approach)

Before we discuss the approach for this question let’s see what exactly the question requires us to do. It seems that we have to push all the 0s in the array towards the end of the array. It can also be looked at as pushing all the non-zero elements in the array towards the beginning of the array.  
First, traverse the whole array and initialize a variable count whose value should be equal to zero. Now, check each element of the array whether it is equal to zero or not. If the element is not equal to zero,put that element at the count position of the array(arr[count]) and increment the value of count by one.  
Now, after traversing the whole array fill the remaining positions of the array with zeroes.

#### [Program](https://utkarsh1504.github.io/DSA-Java/practise-question#program)

```java
package main;
import java.util.*;
public class Main {
	public static void pushZerosToEnd(int[] arr, int n) {
        int count=0;
        for(int i=0;i<arr.length;i++)
        {
            if(arr[i]!=0)
            {
                arr[count++]=arr[i];
            }
        }
        for(int j=count;j<n;j++)
        {
            arr[count++]=0;
        }}
	public static void main(String[] args) {
		int arr[]= {3,0,5,4,0,2,2};
		pushZerosToEnd(arr,7);
		for(int i=0;i<7;i++)
		{
	          System.out.print(arr[i]);
		}}
}
```

```java
Output
3542200
```

#### [Explanation](https://utkarsh1504.github.io/DSA-Java/practise-question#explanation)

- Initialize a variable count with a value equal to zero.  
    
- Make a function named pushZeroToEnd and input an array.  
    
- Traverse through the array and check each element whether it is equal to zero or not.  
    
- If the element is not equal to zero, put the element at the countth position of the array.  
    
- Increase the value of count by 1.  
    
- At last, fill the remaining positions of the array with 0.  
    

#### [Time Complexity](https://utkarsh1504.github.io/DSA-Java/practise-question#time-complexity)

Since we will be traversing the whole array twice therefore the time complexity of algorithm would be:

- **Time complexity of first loop O(N) + Time complexity of second loop O(N) = O(N)**, where n is number of elements in input array.

## [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/?envType=list&envId=o8wvvpl2)[👍]
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

**Input:** strs = ["flower","flow","flight"]
**Output:** "fl"

**Example 2:**

**Input:** strs = ["dog","racecar","car"]
**Output:** ""
**Explanation:** There is no common prefix among the input strings.

**Constraints:**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

### Solution
### Approach

This code is used to find the longest common prefix of an array of strings, which is defined as the longest string that is a prefix of all the strings in the array. By sorting the array and then comparing the first and last elements, the code is able to find the common prefix that would be shared by all strings in the array.

1. Sort the elements of an array of strings called "strs" in lexicographic (alphabetical) order using the Arrays.sort(strs) method.
2. Assign the first element of the sorted array (the lexicographically smallest string) to a string variable s1.
3. Assign the last element of the sorted array (the lexicographically largest string) to a string variable s2.
4. Initialize an integer variable idx to 0.
5. Start a while loop that continues while idx is less than the length of s1 and s2.
6. Within the while loop, check if the character at the current index in s1 is equal to the character at the same index in s2. If the characters are equal, increment the value of idx by 1.
7. If the characters are not equal, exit the while loop.
8. Return the substring of s1 that starts from the first character and ends at the idxth character (exclusive).

### Complexity

- Time complexity:

1. Sorting the array of strings takes O(Nlog(N)) time. This is because most of the common sorting algorithms like quicksort, mergesort, and heapsort have an average time complexity of O(Nlog(N)).
2. Iterating over the characters of the first and last strings takes O(M) time. This is because the code compares the characters of the two strings until it finds the first mismatch.

Therefore, the total time complexity is O(Nlog(N) + M).

- Space complexity:  
    The space used by the two string variables s1 and s2 is proportional to the length of the longest string in the array. Therefore, the space complexity is O(1) as it does not depend on the size of the input array.

### Reason for Sorting

The reason why we sort the input array of strings and compare the first and last strings is that the longest common prefix of all the strings must be a prefix of the first string and a prefix of the last string in the sorted array. This is because strings are ordered based on their alphabetical order (Lexicographical order).  
For example, consider the input array of strings {"flower", "flow", "flight"}. After sorting the array, we get {"flight", "flow", "flower"}. The longest common prefix of all the strings is "fl", which is located at the beginning of the first string "flight" and the second string "flow". Therefore, by comparing the first and last strings of the sorted array, we can easily find the longest common prefix.

### Code

```typescript
class Solution {
    public String longestCommonPrefix(String[] strs) {
        Arrays.sort(strs);
        String s1 = strs[0];
        String s2 = strs[strs.length-1];
        int idx = 0;
        while(idx < s1.length() && idx < s2.length()){
            if(s1.charAt(idx) == s2.charAt(idx)){
                idx++;
            } else {
                break;
            }
        }
        return s1.substring(0, idx);
    }
}
```


**Submitted Solution**
```java
class Solution {

    public String longestCommonPrefix(String[] strs) {

        // sorting the array

        Arrays.sort(strs);

  

        // take the shortest and the longest string

        String small = strs[0];

        String large = strs[strs.length - 1];

  

        // Now check for the prefix

        int i;

        for(i = 0; i< Math.min(small.length(), large.length()); i++){

            // break if the char is not same

            if(small.charAt(i) != large.charAt(i)) break;

        }

  

        // return the prefix

        return small.substring(0, i);

    }

}
```


## [1304. Find N Unique Integers Sum up to Zero](https://leetcode.com/problems/find-n-unique-integers-sum-up-to-zero/description/)[👍]
Given an integer `n`, return **any** array containing `n` **unique** integers such that they add up to `0`.

**Example 1:**

**Input:** n = 5
**Output:** [-7,-1,1,3,4]
**Explanation:** These arrays also are accepted [-5,-1,1,2,3] , [-3,-1,2,-2,4].

**Example 2:**

**Input:** n = 3
**Output:** [-1,0,1]

**Example 3:**

**Input:** n = 1
**Output:** [0]

**Constraints:**

- `1 <= n <= 1000`

### Solution
### **Intuition**

Naive idea  
`n = 1, [0]`  
`n = 2, [-1, 1]`

Now write more based on this  
`n = 3, [-2, 0, 2]`  
`n = 4, [-3, -1, 1, 3]`  
`n = 5, [-4, -2, 0, 2, 4]`

It spreads like the wave.  
  

### **Explanation**

Find the rule  
`A[i] = i * 2 - n + 1`  
  

### **Math Observation**

@zzg_zzm helps explain in math.

Actually, this rule could be derived from constructing an arithmetic sequence.

(Note that any arithmetic sequence must have unique values if the common delta is non-zero)

We need the sequence sum, so that

`(a[0] + a[n-1]) * n / 2 = 0`, which means `a[0] + a[n-1] = 0`.

Note that `a[n-1] - a[0] = (n-1) * delta`, which is `-2 * a[0]`,

so we simply set `delta = 2, a[0] = 1 - n`  
  

### **Note**

It's not bad to sum up `1 + 2 + 3 + ... + (N - 1)`.  
Personally I don't really like it much.  
What is the possible problem of this approach?  
It doesn't work if `N` goes up to `10^5`  
  

### **Complexity**

Time `O(N)`  
Space `O(N)`  
  

**Java:**

```java
    public int[] sumZero(int n) {
        int[] A = new int[n];
        for (int i = 0; i < n; ++i)
            A[i] = i * 2 - n + 1;
        return A;
    }
```

**C++:**

```cpp
    vector<int> sumZero(int n) {
        vector<int> A(n);
        for (int i = 0; i < n; ++i)
            A[i] = i * 2 - n + 1;
        return A;
    }
```

**Python:**

```python
    def sumZero(self, n):
        return range(1 - n, n, 2)
```

### Solution 2
- start filling up from left and right complementary values (so if we insert 1 from left, insert -1 from right, then insert 2 from left and insert -2 from right and so on) :

```java
public int[] sumZero(int n) {
        int[] res = new int[n];
        int left = 0, right = n - 1, start = 1;
        while (left < right) {
            res[left++] = start;
            res[right--] = -start;
            start++;
        }
        return res;
    }
```


## [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)[👎]
