## [2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/description/)[👍]

In a linked list of size `n`, where `n` is **even**, the `ith` node (**0-indexed**) of the linked list is known as the **twin** of the `(n-1-i)th` node, if `0 <= i <= (n / 2) - 1`.

-   For example, if `n = 4`, then node `0` is the twin of node `3`, and node `1` is the twin of node `2`. These are the only nodes with twins for `n = 4`.

The **twin sum** is defined as the sum of a node and its twin.

Given the `head` of a linked list with even length, return _the **maximum twin sum** of the linked list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/12/03/eg1drawio.png)

**Input:** head = [5,4,2,1]
**Output:** 6
**Explanation:**
Nodes 0 and 1 are the twins of nodes 3 and 2, respectively. All have twin sum = 6.
There are no other nodes with twins in the linked list.
Thus, the maximum twin sum of the linked list is 6. 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/12/03/eg2drawio.png)

**Input:** head = [4,2,2,3]
**Output:** 7
**Explanation:**
The nodes with twins present in this linked list are:
- Node 0 is the twin of node 3 having a twin sum of 4 + 3 = 7.
- Node 1 is the twin of node 2 having a twin sum of 2 + 2 = 4.
Thus, the maximum twin sum of the linked list is max(7, 4) = 7. 

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/12/03/eg3drawio.png)

**Input:** head = [1,100000]
**Output:** 100001
**Explanation:**
There is only one node with a twin in the linked list having twin sum of 1 + 100000 = 100001.

**Constraints:**

-   The number of nodes in the list is an **even** integer in the range `[2, 105]`.
-   `1 <= Node.val <= 105`

Accepted

`128.7K`

Submissions

`156.3K`

Acceptance Rate

`82.3%`

**[Solution 1](**)**
1. My approach is to traverse the linked list and store the elements in a stack and queue simultaneously. 
2. After that iterate through the stack and queue and find the sum i.e. sum of element from stack and an element from queue. 
3. And compare the current iteration sum with the previous iteration sum and check the maximum.

```java
/**

 * Definition for singly-linked list.

 * public class ListNode {

 *     int val;

 *     ListNode next;

 *     ListNode() {}

 *     ListNode(int val) { this.val = val; }

 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }

 * }

 */

class Solution {

    public int pairSum(ListNode head) {

        int sum = 0;

        Queue<Integer> q = new LinkedList<Integer>();

        Stack<Integer> s = new Stack<Integer>();

		//1
        while(head != null){

            q.add(head.val);

            s.push(head.val);

            head = head.next;

        }

  
		//2 and 3
        while(!q.isEmpty()){

            int currSum = q.remove() + s.pop();

            sum = (currSum > sum)?currSum:sum;

        }

  

        return sum;

    }

}
```

**[Solution 2](**)**
[![](https://assets.leetcode.com/users/aryan_0077/avatar_1587989855.png)](https://leetcode.com/aryan_0077/)

Image Explanation🏆- [Fastest, Easiest & Concise] - C++/Java/Python

[aryan_0077](https://leetcode.com/aryan_0077/)

4079

5809

11 hours ago

C++

Java

Python3

Linked List

### Video Solution (`Aryan Mittal`) - Link in LeetCode Profile

`Maximum Twin Sum of a Linked List` by `Aryan Mittal`  
![lc.png](https://assets.leetcode.com/users/images/c68c6de4-4912-4bd1-bb85-59eb6f111502_1684286771.1539989.png)

### Approach & Intution

![image.png](https://assets.leetcode.com/users/images/c84f966e-8e5d-4f85-a4f0-c115562115a5_1684286216.5786326.png)  
![image.png](https://assets.leetcode.com/users/images/b3b89710-e30e-499a-a4f4-205f193bcf9a_1684286224.703438.png)  
![image.png](https://assets.leetcode.com/users/images/bb4d9205-3960-451b-bd9e-928d374772cf_1684286231.9536028.png)  
![image.png](https://assets.leetcode.com/users/images/7140d305-836e-4d50-a9bd-6621eddc1e88_1684286250.2656589.png)  
![image.png](https://assets.leetcode.com/users/images/e33fb55f-192c-4526-ba64-b831f520e346_1684286264.7647347.png)  
![image.png](https://assets.leetcode.com/users/images/97dfb59d-39f5-4ddc-a35b-2d1e611f8cc1_1684286275.0009816.png)  
![image.png](https://assets.leetcode.com/users/images/06e07577-83d7-4d47-b2dc-1200ecfd8654_1684286282.0596707.png)  
![image.png](https://assets.leetcode.com/users/images/31e5bd4a-46c8-492c-b2b1-e5d632b82a78_1684286312.8254578.png)  
![image.png](https://assets.leetcode.com/users/images/2550c2cb-f83f-46f7-9ec5-d45ee60b1ec6_1684286320.8130295.png)




```java
class Solution {
    public int pairSum(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        int maxVal = 0;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode nextNode, prev = null;
        while (slow != null) {
            nextNode = slow.next;
            slow.next = prev;
            prev = slow;
            slow = nextNode;
        }

        while (prev != null) {
            maxVal = Math.max(maxVal, head.val + prev.val);
            prev = prev.next;
            head = head.next;
        }

        return maxVal;
    }
}
```

### Another approach without modifying the given LinkedList


You are modifying the linked list which I don't think is a good way to do it. I agree that the space is O(1) but the original Linked List is getting mutated.  
Without mutating can be done by using a stack to store the second half.  
Then get the top most element of the stack and add with the ListNode->val to get the max.

```cpp
int pairSum(ListNode* head) {
        stack<int> stk;
        int res=0;
        ListNode *slow = head, *fast = head;

        while(fast!=NULL && fast->next!=NULL) {
            slow = slow->next;
            fast = fast->next->next;
        }

        while(slow!=NULL) {
            stk.push(slow->val);
            slow = slow->next;
        }

        ListNode* p = head;
        while(!stk.empty()) {
            int sum = p->val + stk.top();
            res = max(res, sum);
            p = p->next;
            stk.pop();
        }

        return res;
    }
```


## [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)[👍]

Medium


Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

**Input:** matrix = [[1,1,1],[1,0,1],[1,1,1]]
**Output:** [[1,0,1],[0,0,0],[1,0,1]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

**Input:** matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
**Output:** [[0,0,0,0],[0,4,5,0],[0,3,1,0]]

**Constraints:**

-   `m == matrix.length`
-   `n == matrix[0].length`
-   `1 <= m, n <= 200`
-   `-231 <= matrix[i][j] <= 231 - 1`

**Follow up:**

-   A straightforward solution using `O(mn)` space is probably a bad idea.
-   A simple improvement uses `O(m + n)` space, but still not the best solution.
-   Could you devise a constant space solution?


### Method 1: (Brute force)  
-using another matrix (let's say it matrix2)

1.  we can copy all the elements of given matrix to matrix2
2.  while traversing given matrix whenever we encounter 0, we will make the entire row and column of the matrix2 to 0
3.  finally we can again copy all the elements of matrix2 to given matrix  
    -**Time:** O((mn)*(m+n)), **Space:** O(mn)

![image](https://assets.leetcode.com/users/images/edb17693-61dd-424b-88e7-f37b79c602f1_1662224098.764936.png)

```cpp
public void setZeroes(int[][] matrix){

		int m= matrix.length, n= matrix[0].length;
        int matrix2[][]= new int[m][n];
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++)
                matrix2[i][j]=matrix[i][j];
        }
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){
                    for(int k=0;k<n;k++)
                        matrix2[i][k]=0;

                    for(int k=0;k<m;k++)
                        matrix2[k][j]=0;
                }
            }
        }
    
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++)
                matrix[i][j]=matrix2[i][j];
        }
    }
```

### Method 2: (Better)

1.  we can use two separate arrays one for rows (rowsArray) and one for columns (colsArray) and initialize them to 1
2.  while traversing the given matrix whenever we encounter 0 at (i,j), we will set rowsArray[i]=0 and colsArray[j]=0
3.  After completion of step 2, again iterate through the matrix and for any (i,j), if rowsArray[i] or colsArray[j] is 0 then update matrix[i][j] to 0.  
    -**Time:** O(mn), **Space:** O(m+n)

![image](https://assets.leetcode.com/users/images/985c05ee-ba5b-43ec-a7c2-41983d8bdae1_1662224319.5420349.png)

```cpp
public void setZeroes(int[][] matrix){

		int m=matrix.length, n=matrix[0].length;
        int rowsArray[]= new int[m];
        int colsArray[]= new int[n];
        
        Arrays.fill(rowsArray,1);
        Arrays.fill(colsArray,1);
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){
                    rowsArray[i]=0;
                    colsArray[j]=0;
                }
            }
        }
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(rowsArray[i]==0 || colsArray[j]==0)
                    matrix[i][j]=0;
            }
        }
    }
```

**Method 3:** (Optimal)  
-we can use the 0th row and 0th column of the given matrix itself instead of using two separate arrays

1.  first we will traverse the 0th row and 0th column of the given matrix and if we encounter any 0 then we will set the isRow0/isCol0 variable to true which indicates that the 0th row/0th column of the given matrix will become 0
2.  next we will traverse the remaining matrix except 0th row and 0th column and if we encounter any 0, we will make the corresponding row no. and column no. equal to 0 in the 0th column and 0th row respectively
3.  Now we will update the values of the matrix except first row and first column to 0 if matrix[i][0]=0 or matrix[0][j]=0 for any (i,j).
4.  finally we will traverse the 0th row and 0th column and if we find any 0, we will make the whole row and whole column equal to 0  
    -**Time:** O(mn), **Space:** O(1)

![image](https://assets.leetcode.com/users/images/75193089-d14a-4cf9-aacf-5f97cc935f02_1662224420.9994516.png)

```java
public void setZeroes(int[][] matrix){

		int m=matrix.length, n=matrix[0].length;
        boolean isRow0=false, isCol0=false;
        
        for(int j=0;j<n;j++){
            if(matrix[0][j]==0)
                isRow0=true;
        }
        
        for(int i=0;i<m;i++){
            if(matrix[i][0]==0)
                isCol0=true;
        }
        
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(matrix[i][j]==0){
                    matrix[i][0]=0;
                    matrix[0][j]=0;
                }
            }
        }
        
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(matrix[0][j]==0 || matrix[i][0]==0)
                    matrix[i][j]=0;
            }
        }
        
        if(isRow0){
            for(int j=0;j<n;j++)
                matrix[0][j]=0;
        }
        
        if(isCol0){
            for(int i=0;i<m;i++)
                matrix[i][0]=0;
        }
    }
```



## [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)[👍]

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = `["eat","tea","tan","ate","nat","bat"]`
**Output:** `[["bat"],["nat","tan"],["ate","eat","tea"]]`

**Example 2:**

**Input:** strs = `[""]`
**Output:** `[[""]]`

**Example 3:**

**Input:** strs = `["a"]`
**Output:** `[["a"]]`

**Constraints:**

-   `1 <= strs.length <= 104`
-   `0 <= strs[i].length <= 100`
-   `strs[i]` consists of lowercase English letters.


### solution
```java
class Solution {

    public List<List<String>> groupAnagrams(String[] strs) {

        Map<String, ArrayList<String>> map = new HashMap<>();

  

        for( String s: strs ){

  

            char[] valArr = s.toCharArray();

            Arrays.sort( valArr );

            String key = new String(valArr);

  

            ArrayList<String> ll = map.getOrDefault( key,

                                     new ArrayList<String>() );

            ll.add(s);

            map.put( key, ll );

        }

  

        List<List<String>> ans = new ArrayList<>();

        for( Map.Entry<String, ArrayList<String>> entry: map.entrySet() ){

            ans.add( entry.getValue() );

        }

  

        return ans;

    }

}
```



## [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)[👍]

Given a string `s`, find the length of the **longest** 

**substring**

 without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"
**Output:** 3
**Explanation:** The answer is "abc", with the length of 3.

**Example 2:**

**Input:** s = "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

**Input:** s = "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

**Constraints:**

-   `0 <= s.length <= 5 * 104`
-   `s` consists of English letters, digits, symbols and spaces.
-

### Solution
  
So, the prerequisit of this problem is **Sliding Window**, if you know then it's a plus point. But, if you don't know don't worry I'll try to teach you.

Let's understand first of all what the problem is saying!!

```csharp
Given a string s, find the length of the longest substring without repeating characters.
```

Okay, so from the given statement we will try to find out wether it is a **Sliding Window** problem or not>>

So, to check that out I'm giving you a tempelate & it'll work in almost all of the questions of **sliding window**

```csharp
To, find out a sliding window problem :-
> First thing is, we have given something like an "Array" | OR | "String"
> Second thing is, they are talking about either "subsequence" | OR | "substring"
> And third most thing is, either we have given a "window size i.e. k" | OR | we have to "manually find out window size" 
```

Now, using above keys let's understand wether this problem is of a sliding window or not.

```rust
> Are they talking about, "Array" or "String" --> yes they are talking about "string" +1 point
> Are they asking to find out "subsequence" or "substring" --> yes they are talking about "substring" +1 point
> Do, we have given a window size --> No, we don't have

Total score is "2 / 3" so, it's a 100% sliding window problem. If your score lies from 2/3 to 3/3 that's a gauranteed sliding window problem 
```

Now, let's talk about how we gonna implement sliding window in this problem, but before that I just want to tell you one more thing. There's exist basically 2 types of sliding window.

1.  Fix size sliding window **{means K is given}**
    
2.  Variable silze sliding window **{means K is not given}**
    

**Before moving to the problem I want to give you a template which you can use in any sliding window `{Variable size}` problem**

```kotlin
while(j < size()){

    // Calculation's happen's here
-----------------------------------------------
    if(condition < k){
        j++;
    }
-----------------------------------------------

-----------------------------------------------
    else if(condition == k){
        // ans <-- calculation
        j++;
    }
----------------------------------------------

----------------------------------------------
    else if(condition > k){
        while(condition > k){
            // remove calculation for i
            i++;
        }
        j++;
    }
----------------------------------------------
}
return ans;
```

So, in this problem we gonna deal with variable size sliding window. Let's take one example :-

```javascript
Input: s = "abcabcbb"
Output: 3
```

So, inorder to solve this, what I'm thinking is, we should have to use one more Data Structure to store the occurence of these characters, I thing HashMap will be best to use.

-   Now, what I'll do is create 2 pointer's i & j initally they both start from 0
-   The j pointer will helps us to fill the array while the i pointer will helps in removing from the map {Don't know what I'm talking about} just wait. You'll understand :)

```rust
Let's understand it visually :-
```

![image](https://assets.leetcode.com/users/images/664cc9c6-1440-4b88-a11f-ca27a67b5266_1654838647.047003.png)

![image](https://assets.leetcode.com/users/images/088afd9c-bc21-46ca-b651-a46a75c02c4e_1654838698.0517573.png)

![image](https://assets.leetcode.com/users/images/61717331-f54a-4940-9000-2bf95dc8af56_1654838746.162897.png)

![image](https://assets.leetcode.com/users/images/3c62fa7f-e7e3-4063-b306-0a3495071004_1654838786.1087303.png)

![image](https://assets.leetcode.com/users/images/c1aae088-b5e1-4328-aa1f-af414b0ef112_1654838837.5751796.png)

![image](https://assets.leetcode.com/users/images/fe893a02-e560-4a8f-aaa1-f92e55dd35cd_1654838885.7713046.png)

![image](https://assets.leetcode.com/users/images/6a268e77-c099-4f01-b0d5-136995310d3f_1654838919.9853337.png)

![image](https://assets.leetcode.com/users/images/6811ecde-9e2a-47e6-b688-682bb3f0f5a2_1654838956.3712077.png)

![image](https://assets.leetcode.com/users/images/a751f95a-f42b-4922-9609-c88ad5f339fb_1654838991.3203616.png)

![image](https://assets.leetcode.com/users/images/f789c5cb-3e73-449e-80de-38f61d5404b9_1654839058.5881085.png)

![image](https://assets.leetcode.com/users/images/65c28458-d89a-4008-afde-264598e4d127_1654839089.2232268.png)

![image](https://assets.leetcode.com/users/images/2fb45c3b-a510-4a3b-be1d-02a53fc0ff02_1654839123.2810624.png)

![image](https://assets.leetcode.com/users/images/5c80c220-70d8-4a9e-9689-a7cd1fb9e11d_1654839162.3931215.png)

![image](https://assets.leetcode.com/users/images/b10fc6ab-9f8b-4035-bfbf-5b9e4cca3cb0_1654839175.0759387.png)

#### Code
**Java**

```python
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int i = 0;
        int j = 0;
        int max = 0;
        while(j < s.length()){
            map.put(s.charAt(j), map.getOrDefault(s.charAt(j), 0) + 1);
            if(map.size() == j - i + 1){
                max = Math.max(max, j - i + 1);
                j++;
            }
            else if(map.size() < j - i + 1){
                while(map.size() < j - i + 1){
                    map.put(s.charAt(i), map.get(s.charAt(i)) - 1);
                    if(map.get(s.charAt(i)) == 0) map.remove(s.charAt(i));
                    i++;
                }
                j++;
            }
        }
        return max;
    }
}
```

**C++**

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(s.length()==0)return 0;   //if string of length zero comes simply return 0
        unordered_map<char,int> m;   //create map to store frequency,(get to know all unique characters
        int i=0,j=0,ans=INT_MIN; 
        while(j<s.length())   
        {
            m[s[j]]++;  //increase the frequency of the element as you traverse the string
            if(m.size()==j-i+1)  // whem map size is equal to the window size means suppose window size is 3 and map size is also three that means in map all unique characters are their
            {
                ans = max(ans,j-i+1);  //compare the length of the maximum window size
            }
            else if(m.size()<j-i+1)   //if the map size is less than the window size means there is some duplicate present like window size = 3 and map size = 2 means there is a duplicates
            {
                while(m.size()<j-i+1)  //so till the duplicates are removed completely
                {
                    m[s[i]]--;   //remove the duplicates
                    if(m[s[i]]==0)  //if the frequency becomes zero 
                    {
                        m.erase(s[i]);//delete it completely
                    }
                    i++;  //go for next element 
                }
            }
             j++;  //go for the next element
        }
        return ans;
    }
};
```



## [146. LRU Cache](https://leetcode.ca/2016-04-24-146-LRU-Cache/#146-lru-cache)[👎]


### [Question](https://leetcode.ca/2016-04-24-146-LRU-Cache/#question)

Formatted question description: [https://leetcode.ca/all/146.html](https://leetcode.ca/all/146.html)

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

-   `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
-   `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
-   `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

**Input**
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
**Output**
[null, null, null, 1, null, -1, null, -1, 3, 4]

**Explanation**
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4

**Constraints:**

-   `1 <= capacity <= 3000`
-   `0 <= key <= 104`
-   `0 <= value <= 105`
-   At most `2 * 105` calls will be made to `get` and `put`.

### [Algorithm](https://leetcode.ca/2016-04-24-146-LRU-Cache/#algorithm)

#### [Solution](https://leetcode.ca/2016-04-24-146-LRU-Cache/#solution)

Create a class `MyNode`, which contains data fields `int key`, `int value`, `Node prev` and `Node next`. That is, each node of type `MyNode` has a key and a value, and have references to its previous node and the next node.

In class `LRUCache`, data fields include `int capacity` that stores the capacity of the cache, `Map<Integer, MyNode> map` that maps each key to its node, `MyNode head` and `Node tail` that represents the head node and the tail node respectively. For Least Recently Used cache, the most recently used node is the head node and the least recently used node is the tail node.

In the constructor, initialize `capacity` with the given `capacity`.

In `get(key)`, if `key` is not in `map`, then `key` is not in the cache, so return -1. If `key` is in `map`, obtain the node and its `value`, remove the node and set the node to be the head, and return `value`.

In `put(key, value)`, if `map` contains `key`, then obtain the node and update its `value`, remove the node, and set the node to be the head. If `map` does not contain `key`, then create a new node using `key` and `value`, and set the new node to be the head. If the size of `map` is greater than or equal to `capacity`, then remove the node `tail` and remove the corresponding entry in `map`. Add a new entry of the new node into the map.

Two supplementary methods are needed.

1.  Method `remove(MyNode node)`. Obtain `MyNode`’s previous node and next node, and update their references to other nodes accordingly. If `MyNode` is `head` or `tail`, then update `head` or `tail` accordingly.
2.  Method `setHead(MyNode node)`. Set `MyNode` to be the new head and set the previous head’s reference accordingly. If `tail` is `null`, then update `tail` as well.

#### [Code](https://leetcode.ca/2016-04-24-146-LRU-Cache/#code)

Java

  ```java
    class LRUCache {
        int capacity;
        Map<Integer, MyNode> map = new HashMap<Integer, MyNode>(); // key => Node[key,val]
        MyNode head = null;
        MyNode tail = null;
    
        public LRUCache(int capacity) {
            this.capacity = capacity;
        }
    
        public int get(int key) {
            MyNode node = map.get(key);
            if (node == null) {
                return -1;
            } else {
                remove(node);
                setHead(node);
                return node.value;
            }
        }
    
        public void put(int key, int value) {
            if (map.containsKey(key)) {
                MyNode node = map.get(key);
                node.value = value;
                remove(node);
                setHead(node);
            } else {
                MyNode node = new MyNode(key, value);
                setHead(node);
                map.put(key, node);
                if (map.size() >= capacity) { // @note: also = , after if will add one more
                    map.remove(tail.key);
                    remove(tail);
                }
            }
        }
    
        public void remove(MyNode node) {
            MyNode prev = node.prev;
            MyNode next = node.next;
    
            // process previous node
            if (prev != null)
                prev.next = next;
            else
                head = next;
    
            // process next node
            if (next != null)
                next.prev = prev;
            else
                tail = prev;
        }
    
        public void setHead(MyNode node) {
            node.next = head;
            node.prev = null;
            if (head != null)
                head.prev = node;
            head = node;
            if (tail == null)
                tail = head;
        }
    }
    
    class MyNode {
        int key;
        int value;
        MyNode prev;
        MyNode next;
    
        public MyNode(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    /**
     * Your LRUCache object will be instantiated and called as such:
     * LRUCache obj = new LRUCache(capacity);
     * int param_1 = obj.get(key);
     * obj.put(key,value);
     */
    
    
    ############
    
    class Node {
        int key;
        int val;
        Node prev;
        Node next;
    
        Node() {
        }
    
        Node(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
    
    class LRUCache {
        private Map<Integer, Node> cache = new HashMap<>();
        private Node head = new Node();
        private Node tail = new Node();
        private int capacity;
        private int size;
    
        public LRUCache(int capacity) {
            this.capacity = capacity;
            head.next = tail;
            tail.prev = head;
        }
    
        public int get(int key) {
            if (!cache.containsKey(key)) {
                return -1;
            }
            Node node = cache.get(key);
            moveToHead(node);
            return node.val;
        }
    
        public void put(int key, int value) {
            if (cache.containsKey(key)) {
                Node node = cache.get(key);
                node.val = value;
                moveToHead(node);
            } else {
                Node node = new Node(key, value);
                cache.put(key, node);
                addToHead(node);
                ++size;
                if (size > capacity) {
                    node = removeTail();
                    cache.remove(node.key);
                    --size;
                }
            }
        }
    
        private void moveToHead(Node node) {
            removeNode(node);
            addToHead(node);
        }
    
        private void removeNode(Node node) {
            node.prev.next = node.next;
            node.next.prev = node.prev;
        }
    
        private void addToHead(Node node) {
            node.next = head.next;
            node.prev = head;
            head.next = node;
            node.next.prev = node;
        }
    
        private Node removeTail() {
            Node node = tail.prev;
            removeNode(node);
            return node;
        }
    }
    
    /**
     * Your LRUCache object will be instantiated and called as such:
     * LRUCache obj = new LRUCache(capacity);
     * int param_1 = obj.get(key);
     * obj.put(key,value);
     */
    ```
    

### [All Problems](https://leetcode.ca/all/problems.html)[old](https://leetcode.ca/2016-04-24-146-LRU-Cache/#all-problems)

### [All Solutions](https://leetcode.ca/blog)


## [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)[👎]

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = `["eat","tea","tan","ate","nat","bat"]`
**Output:** `[["bat"],["nat","tan"],["ate","eat","tea"]]`

**Example 2:**

**Input:** strs = `[""]`
**Output:** `[[""]]`

**Example 3:**

**Input:** strs =` ["a"]`
**Output:** `[["a"]]`

**Constraints:**

-   `1 <= strs.length <= 104`
-   `0 <= strs[i].length <= 100`
-   `strs[i]` consists of lowercase English letters.


### Solution

```java
class Solution {

    public List<List<String>> groupAnagrams(String[] strs) {

        Map<String, ArrayList<String>> map = new HashMap<>();

  

        for( String s: strs ){

  

            char[] valArr = s.toCharArray();

            Arrays.sort( valArr );

            String key = new String(valArr);

  

            ArrayList<String> ll = map.getOrDefault( key,

                                     new ArrayList<String>() );

            ll.add(s);

            map.put( key, ll );

        }

  

        List<List<String>> ans = new ArrayList<>();

        for( Map.Entry<String, ArrayList<String>> entry: map.entrySet() ){

            ans.add( entry.getValue() );

        }

  

        return ans;

    }

}
```


## [15. 3Sum](https://leetcode.com/problems/3sum/description/)[👍]
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = `[-1,0,1,2,-1,-4]`
**Output:** `[[-1,-1,2],[-1,0,1]]`
**Explanation:** 
`nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
`nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.`
`nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.`
The distinct triplets are` [-1,0,1] `and `[-1,-1,2]`.
Notice that the order of the output and the order of the triplets does not matter.

**Example 2:**

**Input:** nums = `[0,1,1]`
**Output:**` []`
**Explanation:** The only possible triplet does not sum up to 0.

**Example 3:**

**Input:** nums = `[0,0,0]`
**Output:**` [[0,0,0]]`
**Explanation:** The only possible triplet sums up to 0.

**Constraints:**

- `3 <= nums.length <= 3000`
- `-10^5 <= nums[i] <= 10^5`

### Solution 1
#### Intuition of this Problem:

Set is used to prevent duplicate triplets and parallely we will use two pointer approach to maintain J and k.

**NOTE - PLEASE READ APPROACH FIRST THEN SEE THE CODE. YOU WILL DEFINITELY UNDERSTAND THE CODE LINE BY LINE AFTER SEEING THE APPROACH.**

#### Approach for this Problem:

1. Sort the input array
2. Initialize a set to store the unique triplets and an output vector to store the final result
3. Iterate through the array with a variable i, starting from index 0.
4. Initialize two pointers, j and k, with j starting at i+1 and k starting at the end of the array.
5. In the while loop, check if the sum of nums[i], nums[j], and nums[k] is equal to 0. If it is, insert the triplet into the set and increment j and decrement k to move the pointers.
6. If the sum is less than 0, increment j. If the sum is greater than 0, decrement k.
7. After the while loop, iterate through the set and add each triplet to the output vector.
8. Return the output vector

#### Code:
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int target = 0;
        Arrays.sort(nums);
        Set<List<Integer>> s = new HashSet<>();
        List<List<Integer>> output = new ArrayList<>();
        for (int i = 0; i < nums.length; i++){
            int j = i + 1;
            int k = nums.length - 1;
            while (j < k) {
                int sum = nums[i] + nums[j] + nums[k];
                if (sum == target) {
                    s.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++;
                    k--;
                } else if (sum < target) {
                    j++;
                } else {
                    k--;
                }
            }
        }
        output.addAll(s);
        return output;
    }
}
```

#### Time Complexity and Space Complexity:

- Time complexity: **O(n^2 logn)** // where n is the size of array  
    Sorting takes O(nlogn) time and loop takes O(n^2) time, So the overall time complexity is O(nlogn + n^2 logn) - O(n^2 logn)

- Space complexity: **O(n)** // for taking hashset.


### Solution 2
```java
class Solution {

    public List<List<Integer>> threeSum(int[] nums) {

        Arrays.sort(nums);

        List<List<Integer>> list = new ArrayList<List<Integer>>();

        for(int i = 0; i < nums.length-2; i++) {

            if(i > 0 && (nums[i] == nums[i-1])) continue; // avoid duplicates

            for(int j = i+1, k = nums.length-1; j<k;) {

                if(nums[i] + nums[j] + nums[k] == 0) {

                    list.add(Arrays.asList(nums[i],nums[j],nums[k]));

                    j++;k--;

                    while((j < k) && (nums[j] == nums[j-1]))j++;// avoid duplicates

                    while((j < k) && (nums[k] == nums[k+1]))k--;// avoid duplicates

                }else if(nums[i] + nums[j] + nums[k] > 0) k--;

                else j++;

            }

        }

        return list;

    }

}
```

### Multiple Methods
#### without sort

```csharp
    //Runtime: 384 ms, faster than 24.18% of Java online submissions for 3Sum.
    //Memory Usage: 120.2 MB, less than 15.92% of Java online submissions for 3Sum.
    //without sort
    //Time: O(N * N * log3); Space:O(N)
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> resultSet = new HashSet();

        Set<Integer> duplicatedSet = new HashSet<>();
        Map<Integer, Integer> map = new HashMap<>();

        for(int i = 0; i < nums.length - 2; i++) {
            if (!duplicatedSet.add(nums[i])) continue;

            for (int j = i + 1; j < nums.length; j++) {
                int value = 0 - nums[i] - nums[j];
                if (map.containsKey(value) && map.get(value) == i) {
                    List<Integer> list = new ArrayList<>(Arrays.asList(nums[i], nums[j], value));
                    Collections.sort(list);
                    resultSet.add(list);
                }
                map.put(nums[j], i);
            }
        }
        return new ArrayList<>(resultSet) ;
    }
```

#### Two pointers

```java

    //Runtime: 47 ms, faster than 35.83% of Java online submissions for 3Sum.
    //Memory Usage: 60.1 MB, less than 32.20% of Java online submissions for 3Sum.
    //Two pointers
    //Time: O(N * LogN + N * N); Space : O(N + LogN)
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> resultSet = new HashSet();
        Arrays.sort(nums);

        for(int i = 0; i <= nums.length - 3 && nums[i] <= 0;){
            int left = i + 1, right = nums.length - 1;
            if (0 - nums[i] - nums[left] < 0) break;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum > 0) {
                    right--;
                    while (left < right && nums[right] == nums[right + 1]) right--; //skip duplicated number
                } else {
                    if (sum == 0) {
                        resultSet.add(Arrays.asList(nums[i], nums[left], nums[right]));
                        right--;
                        while (left < right && nums[right] == nums[right + 1]) right--;
                    }
                    left++;
                    while (left < right && nums[left] == nums[left - 1]) left++;
                }
            }
            i++;
            while(i < nums.length - 2 && nums[i] == nums[i - 1]) i++;
        }
        return new ArrayList<>(resultSet);
    }
```

#### Binary Search

```java

    //Runtime: 99 ms, faster than 29.77% of Java online submissions for 3Sum.
    //Memory Usage: 60.2 MB, less than 31.74% of Java online submissions for 3Sum.
    //Binary Search
    //Time: O(N * logN + N * N * logN); Space:O(N + LogN)
    public List<List<Integer>> threeSum_3(int[] nums) {
        Set<List<Integer>> resultSet = new HashSet();
        Arrays.sort(nums);

        for(int i = 0; i < nums.length - 2 && nums[i] <= 0;){
            for (int j = i + 1; j < nums.length && nums[i] + nums[j] <= 0;) {
                int value = 0 - nums[i] - nums[j];
                if (value < 0) return new ArrayList<>(resultSet);
                int idx = Arrays.binarySearch(nums, j + 1, nums.length, value);
                if (idx >= 0)
                    resultSet.add(Arrays.asList(nums[i], nums[j], value));
                j++;
                while (j < nums.length && nums[j] == nums[j - 1]) j++;
            }
            i++;
            while(i < nums.length - 2 && nums[i] == nums[i - 1]) i++;
        }
        return new ArrayList<>(resultSet);
    }
```

#### HashMap

```csharp

    //Runtime: 106 ms, faster than 29.54% of Java online submissions for 3Sum.
    //Memory Usage: 70.8 MB, less than 23.87% of Java online submissions for 3Sum.
    //HashMap
    //Time:O(N * logN + N * N); Space: O(N + logN + N)
    public List<List<Integer>> threeSum_2(int[] nums) {
        Set<List<Integer>> resultSet = new HashSet();
        Arrays.sort(nums);
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) map.put(nums[i], i);

        for(int i = 0; i < nums.length - 2 && nums[i] <= 0;){
            for (int j = i + 1; j < nums.length && nums[i] + nums[j] <= 0;) {
                int value = 0 - nums[i] - nums[j];
                //if (value < 0) break;
                if (value < 0) return new ArrayList<>(resultSet);
                if (value < nums[j]) break;
                if (map.containsKey(value) && map.get(value) > j)
                    resultSet.add(Arrays.asList(nums[i], nums[j], value));
                j++;
                while(j < nums.length && nums[j] == nums[j - 1]) j++;
            }
            i++;
            while(i < nums.length - 2 && nums[i] == nums[i - 1]) i++;
        }
        return new ArrayList<>(resultSet) ;
    }
```

#### brute force

```java

    //TLE
    //brute force
    //Time: O(N * N * N * log3); Space: O(N)
    public List<List<Integer>> threeSum_brute(int[] nums) {
        Set<List<Integer>> resultSet = new HashSet();
        for (int i = 0; i < nums.length - 2; i++)
            for (int j= i + 1; j < nums.length - 1; j++)
                for (int k = j + 1 ; k < nums.length; k++)
                    if (0 == nums[i] + nums[j] + nums[k]) {
                        List<Integer> list = new ArrayList<>(Arrays.asList(nums[i], nums[j], nums[k]));
                        Collections.sort(list);
                        resultSet.add(list);
                    }
        return new ArrayList<>(resultSet);
    }
	
```



## [229. Majority Element II](https://leetcode.com/problems/majority-element-ii/description/)[👎]

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** [3]

**Example 2:**

**Input:** nums = [1]
**Output:** [1]

**Example 3:**

**Input:** nums = [1,2]
**Output:** [1,2]

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-109 <= nums[i] <= 109`

**Follow up:** Could you solve the problem in linear time and in `O(1)` space?

### Solution
There can be at most `k - 1` major element in an array if the major element appears more than `⌊n / k⌋` times.

In the begining, we assume there are `k - 1` candidates:

1. These candidates can take **any** value;
2. The vote of these candidates **must** be 0

Then we traverse the array:

1. If current element equals to the value of any candidate, the candidate get a vote; (one voter can only vote for one candidate)
2. If the vote of any candidate is 0, then current element is set as a new candidate and he can get a vote immediately; (A voter can also be elected)
3. Otherwise, current element vote against all candidates and all candidates lose a vote.

Assume you're voting for the president. If you want to select Trump or Biden. Ok, just vote for them (case 1). If Trump is impeached or Biden is dead, now you can run for the president (case 2). If you want to vote for Lebron James, of course both Biden or Trump won't get your vote (case 3).

After election, we need to count the vote of each candidate to see whether they are qualified for the position, i.e., the vote is larger than `⌊n / k⌋`.

```java
public List<Integer> majorityElement(int[] nums) {
	List<Integer> result = new ArrayList<Integer>();
	if (nums.length == 0)
		return result;
	// In the begining, both Trump and Biden don't get a vote
	int firstMajor = Integer.MAX_VALUE, firstSum = 0, secondMajor = Integer.MIN_VALUE, secondSum = 0;
	
	for (int i = 0; i < nums.length; i++) {
		// case 1: I want to vote for Biden or Trump
		if (nums[i] == firstMajor)
			firstSum++;
		else if (nums[i] == secondMajor)
			secondSum++;
		// case 2: I want to run for the president
		else if (firstSum == 0) {
			firstMajor = nums[i];
			firstSum = 1;
		}
		else if (secondSum == 0) {
			secondMajor = nums[i];
			secondSum = 1;
		}
		// case 3: fuck sleepy Joe and crazy Trump, let James be the president
		else {
			firstSum--;
			secondSum--;
		}
	}
	// After election, we need to count the vote again.
	firstSum = 0;
	secondSum = 0;
	for (int i = 0; i < nums.length; i++) {
		if (nums[i] == firstMajor)
			firstSum++;    
		else if (nums[i] == secondMajor)
			secondSum++;
	}
	if (firstSum > nums.length / 3)
		result.add(firstMajor);
	if (secondSum > nums.length / 3)
		result.add(secondMajor);
	return result;
}
```




## [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)[👍]
Given an integer array `nums`, find a 

subarray

 that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

**Example 1:**

**Input:** nums = [2,3,-2,4]
**Output:** 6
**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]
**Output:** 0
**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

- 1 <= `nums.length` <= 2 * 10<sup>4</sup>
- `-10 <= nums[i] <= 10`
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

### Solution
**Intution:** Since we have to find the contiguous subarray having maximum product then your approach should be combination of following three cases :

- **Case1 :- All the elements are positive :** Then your answer will be product of all the elements in the array.
- **Case2 :- Array have positive and negative elements both :**
    1. If the number of negative elements is even then again your answer will be complete array because on multiplying all the negative numbers it will become positive.
    2. If the number of negative elements is odd then you have to remove just one negative element and for that u need to check your subarrays to get the max product.
- **Case3 :- Array also contains 0 :** Then there will be not much difference...its just that your array will be divided into subarray around that 0. What u have to so is just as soon as your product becomes 0 make it 1 for the next iteration, now u will be searching new subarray and previous max will already be updated.  
    *(These cases are much clear in approach 3)

**As it is said "Talk is Cheap, Show me the Code", so based on above discussion we can frame our code in many different ways, out of which I have mentioned 3 intutive approaches.**

**Approach 1:** For each index i keep updating the max and min. We are also keeping min because on multiplying with any negative number your min will become max and max will become min. So for every index i we will take max of (i-th element, prevMax * i-th element, prevMin * i-th element).

```java
class Solution {
    public int maxProduct(int[] nums) {
        
        int max = nums[0], min = nums[0], ans = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            
            int temp = max;  // store the max because before updating min your max will already be updated
            
            max = Math.max(Math.max(max * nums[i], min * nums[i]), nums[i]);
            min = Math.min(Math.min(temp * nums[i], min * nums[i]), nums[i]);
            
            if (max > ans) {
                ans = max;
            }
        }
        
        return ans;

    }
}
```

**Approach 2:** Just the slight modification of previous approach. As we know that on multiplying with negative number max will become min and min will become max, so why not as soon as we encounter negative element, we swap the max and min already.

```java
class Solution {
    public int maxProduct(int[] nums) {
        
        int max = nums[0], min = nums[0], ans = nums[0];
        int n = nums.length;
        
        for (int i = 1; i < n; i++) {
        
			// Swapping min and max
            if (nums[i] < 0){
                int temp = max;
                max = min;
                min = temp;
            }
                


            max = Math.max(nums[i], max * nums[i]);
            min = Math.min(nums[i], min * nums[i]);


            ans = Math.max(ans, max);
        }
        
        return ans;

    }
}
```

**Approach 3:** Two pointer Approach  
Explanation :  
1.) Through intution explanation we know that if all the elements are positive or the negative elements are even then ur answer will be product of complete array which u will get in variable l and r at the last iteration.  
2.) But if negative elements are odd then u have to remove one negative element and it is sure that it will be either right of max prefix product or left of max suffix product. So u need not to modify anything in your code as u are getting prefix product in l and suffix prduxt in r.  
3.) If array also contains 0 then your l and r will become 0 at that point...then just update it to 1(or else u will keep multiplying with 0) to get the product ahead making another subarray.

![image](https://assets.leetcode.com/users/images/2ce0da10-9355-4018-a256-cba3a41af56d_1638500369.5001783.jpeg)

```java
class Solution {
    public int maxProduct(int[] nums) {
        
        int n = nums.length;
        int l=1,r=1;
        int ans=nums[0];
        
        for(int i=0;i<n;i++){
            
			//if any of l or r become 0 then update it to 1
            l = l==0 ? 1 : l;
            r = r==0 ? 1 : r;
            
            l *= nums[i];   //prefix product
            r *= nums[n-1-i];    //suffix product
            
            ans = Math.max(ans,Math.max(l,r));
            
        }
        
        return ans;

    }
}
```

Thanks for giving it a read...I hope it helped u!!
## [39. Combination Sum](https://leetcode.com/problems/combination-sum/description/?envType=list&envId=o8wvvpl2)[👎]
Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the 

frequency

 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7
**Output:** [[2,2,3],[7]]
**Explanation:**
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8
**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1
**Output:** []

**Constraints:**

- `1 <= candidates.length <= 30`
- `2 <= candidates[i] <= 40`
- All elements of `candidates` are **distinct**.
- `1 <= target <= 40`

### Solution I
refer to [A general approach to backtracking questions in Java (Subsets, Permutations, Combination Sum, Palind...](./A general approach to backtracking questions in Java (Subsets, Permutations, Combination Sum, Palind...)

### Solution II
```java
class Solution {
    
    List<List<Integer>> resultList = new ArrayList<>();
    
    public List<List<Integer>> combinationSum(int[] arr, int target) {
            
        getTargetCombination(arr, 0, target, new ArrayList<Integer>());
        return resultList;
    }
    
    
    public void getTargetCombination(int[] arr, int position, int currentTarget, List<Integer> result) {

        /**
         * Base case
         * 1. If currentTarget is reaching to Zero
         * 2. Current Position is equal to the length of the Array
         */
        if (currentTarget == 0) {
            resultList.add(new ArrayList<>(result));
            return;
        }
        if (position == arr.length) {
            return;
        }

        /**
         * There are two cases
         * 1. Pick the current value if the current value (i.e arr[position]) is less than or equal to the currentTarget
         *    value then use the same attribute by passing the same position
         *
         *  2. Not picking up the current element by not reducing the currentTarget value and increasing the position
         */
        if (arr[position] <= currentTarget) {
            result.add(arr[position]);
            getTargetCombination(arr, position, currentTarget - arr[position], result);
            // removing the last element because post adding of the value the call came back
            result.remove(result.size() - 1);
        }
        // not picked
        getTargetCombination(arr, position + 1, currentTarget, result);
    }
    
}
```

### Solution III
```java
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        // sort candidates to try them in asc order
        Arrays.sort(candidates); 
        // dp[t] stores all combinations that add up to t
        List<List<Integer>>[] dp = new ArrayList[target+1];
        
        
        // build up dp
        for(int t=0; t<=target; t++) {
            // initialize
            dp[t] = new ArrayList();
            // initialize
            List<List<Integer>> combList = new ArrayList();
            
            // for each t, find possible combinations
            for(int j=0; j<candidates.length && candidates[j] <= t; j++) {
                if(candidates[j] == t) {
                    combList.add(Arrays.asList(candidates[j])); // itself can form a list
                } else {
                    for(List<Integer> prevlist: dp[t-candidates[j]]) { // here use our dp definition
                        // i thought it makes more sense to compare with the last element
                        // only add to list when the candidates[j] >= the last element
                        // so the list remains ascending order, can prevent duplicate (ex. has [2 3 3], no [3 2 3])
                        // equal is needed since we can choose the same element many times   
                        if(candidates[j] >= prevlist.get(prevlist.size()-1)){
                            List temp = new ArrayList(prevlist); // temp is needed since 
                            temp.add(candidates[j]); // cannot edit prevlist inside 4eeach looop
                            combList.add(temp);
                        }
                    }
                }
            }
            dp[t] = combList;
        }
        return dp[target];
    }    
```

### Solution IV
```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        combinationSum(result,new ArrayList<Integer>(),candidates,target,0);
        return result;
    }
    public void combinationSum(List<List<Integer>> result, List<Integer> cur, int[] candidates, int target,int start) {
        if (target > 0) {
            for (int i = start;i < candidates.length;i++) { // not using the condition "target >= candidates[i]"
                cur.add(candidates[i]);
                combinationSum(result, cur, candidates, target-candidates[i],i);
                cur.remove(cur.size() - 1);
            }
        }
        if (target == 0) result.add(new ArrayList<Integer>(cur));
    }
}
```
## [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/?envType=list&envId=o8wvvpl2)[👍]

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return _a string of the words in reverse order concatenated by a single space._

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1:**

**Input:** s = "the sky is blue"
**Output:** "blue is sky the"

**Example 2:**

**Input:** s = "  hello world  "
**Output:** "world hello"
**Explanation:** Your reversed string should not contain leading or trailing spaces.

**Example 3:**

**Input:** s = "a good   example"
**Output:** "example good a"
**Explanation:** You need to reduce multiple spaces between two words to a single space in the reversed string.

**Constraints:**

- 1 <= s.length <= 10<sup>4</sup>
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is **at least one** word in `s`.

### Solution 1
Clean Java two-pointers solution (no trim( ), no split( ), no StringBuilder)
Java

```java
public class Solution {
  
  public String reverseWords(String s) {
    if (s == null) return null;
    
    char[] a = s.toCharArray();
    int n = a.length;
    
    // step 1. reverse the whole string
    reverse(a, 0, n - 1);
    // step 2. reverse each word
    reverseWords(a, n);
    // step 3. clean up spaces
    return cleanSpaces(a, n);
  }
  
  void reverseWords(char[] a, int n) {
    int i = 0, j = 0;
      
    while (i < n) {
      while (i < j || i < n && a[i] == ' ') i++; // skip spaces
      while (j < i || j < n && a[j] != ' ') j++; // skip non spaces
      reverse(a, i, j - 1);                      // reverse the word
    }
  }
  
  // trim leading, trailing and multiple spaces
  String cleanSpaces(char[] a, int n) {
    int i = 0, j = 0;
      
    while (j < n) {
      while (j < n && a[j] == ' ') j++;             // skip spaces
      while (j < n && a[j] != ' ') a[i++] = a[j++]; // keep non spaces
      while (j < n && a[j] == ' ') j++;             // skip spaces
      if (j < n) a[i++] = ' ';                      // keep only one space
    }
  
    return new String(a).substring(0, i);
  }
  
  // reverse a[] from a[i] to a[j]
  private void reverse(char[] a, int i, int j) {
    while (i < j) {
      char t = a[i];
      a[i++] = a[j];
      a[j--] = t;
    }
  }
  
}
```


### Solution 2
```java
public String reverseWords(String s) {
        Stack<String> st = new Stack<String>();
        for (String a : s.trim().split(" ")) {
            if (!a.isEmpty())
                st.push(a);
        }
        
        StringBuilder sb = new StringBuilder();
        while (!st.isEmpty()) {
            sb.append(st.pop());
            sb.append(" ");            
        }
        
        return sb.toString().trim();
    }
}
```

### Solution 3
Just to keep it more interesting made it in-place in Java without using any additional library functions except converting String to char[]. Check it out. :)

```java
// reverses the part of an array and returns the input array for convenience
public char[] reverse(char[] arr, int i, int j) {
    while (i < j) {
        char tmp = arr[i];
        arr[i++] = arr[j];
        arr[j--] = tmp;
    }
    return arr;
}

public String reverseWords(String s) {
    // reverse the whole string and convert to char array
    char[] str = reverse(s.toCharArray(), 0, s.length()-1);
    int start = 0, end = 0; // start and end positions of a current word
    for (int i = 0; i < str.length; i++) {
        if (str[i] != ' ') { // if the current char is letter 
            str[end++] = str[i]; // just move this letter to the next free pos
        } else if (i > 0 && str[i-1] != ' ') { // if the first space after word
            reverse(str, start, end-1); // reverse the word
            str[end++] = ' '; // and put the space after it
            start = end; // move start position further for the next word
        }
    }
    reverse(str, start, end-1); // reverse the tail word if it's there
    // here's an ugly return just because we need to return Java's String
    // also as there could be spaces at the end of original string 
    // we need to consider redundant space we have put there before
    return new String(str, 0, end > 0 && str[end-1] == ' ' ? end-1 : end);
}
```

### Solution 4
```java
public class Solution {
    public String reverseWords(String s) {
        String [] words = s.split(" ");
        StringBuilder sb = new StringBuilder();
        int end = words.length - 1;
        for(int i = 0; i<= end; i++){
            if(!words[i].isEmpty()) {
                sb.insert(0, words[i]);
                if(i < end) sb.insert(0, " ");
            }
        }
        return sb.toString();
    }
}
```

### Solution 5
**Java Solutions**

trim() function is used to remove side spaces of whole string!  
fg is used to check space if it is already added in between words!

**Approach 1**

Store words and add them in reverse order to answer with single space!

Java Solution 1

```java
public String reverseWords(String s) {
    
    s=s.trim()+" ";
    String ans="",word="";
    int fg=0;
    for(int i=0;i<s.length();i++)
    {
        if(s.charAt(i)!=' ')
        {
            fg=0;
            word+=s.charAt(i);
        }
        else if(fg==0)
        {
            fg=1;
            ans=word+" "+ans;
            word="";
        }
    }
    return ans.trim();
}
```

**Approach 2**

Reverse the String and store words in reverse order and add it to answer with single space!

Java Solution 2

```java
public String reverseWords(String s) {
    
    StringBuilder str=new StringBuilder(s);
    
    //reverse the string and trim the side spaces!
    s=str.reverse().toString().trim()+" ";
    
    String word="",ans=""; int fg=0;
    
    for(int i=0;i<s.length();i++)
    {
    	if(s.charAt(i)!=' ')
        {
            fg=0;
            word=s.charAt(i)+word;
        }
    	else if(fg==0) 
    	{
    		ans+=" "+word;
    		fg=1;
    		word="";
    	}
    }
    return ans.trim();
}
```

### Solution 6

```java
class Solution {
    public String reverseWords(String s) {
        String[] words = s.trim().split(" +");
        Collections.reverse(Arrays.asList(words));
        return String.join(" ",words);
    }
}
```

### Solution 7

#### Intuition:

The given solution aims to reverse the words in a given string while maintaining the order of the words. The approach is to first reverse the entire string, then iterate through the reversed string to reverse individual words.

#### Approach:

1. Reverse the entire string using the `reverse()` function from the STL library. This will reverse the order of all characters in the string.
2. Initialize variables: `start` to keep track of the start index of the current word, `end` to keep track of the end index of the current word, `i` as the current index, and `n` as the size of the string.
3. Iterate through the reversed string using a while loop until `i` reaches the end of the string:
    - Skip leading spaces by incrementing `i` while `i` is less than `n` and `s[i]` is equal to a space character.
    - Find the end of the current word by incrementing `end` while `i` is less than `n` and `s[i]` is not a space character. This will determine the range of characters representing the current word.
    - If the start index (`start`) is less than the end index (`end`), it means a word is found:
        - Reverse the characters in the current word by using the `reverse()` function with the range from `s.begin() + start` to `s.begin() + end`.
        - Add a space character after the reversed word by setting `s[end++]` to a space.
        - Update the start index (`start`) for the next word by assigning it the value of `end`.
    - Increment `i` to move to the next character in the string.
4. Check if there is an extra space at the end of the reversed string and remove it by resizing the string if `end` is greater than 0.
5. Return the reversed and reversed-words string.

#### Complexity:

- Time Complexity: The time complexity of this solution is O(n), where n is the length of the input string. Reversing the entire string takes O(n) time, and iterating through the string takes O(n) time as well.
- Space Complexity: The space complexity is O(1) since the operations are performed in-place, and no additional space is used apart from the input string itself.

#### C++

```csharp
class Solution {
public:
    string reverseWords(string s) {
        // Reverse the entire string
        reverse(s.begin(), s.end());

        int start = 0; // Start index of the current word
        int end = 0;   // End index of the current word
        int i = 0;     // Current index
        int n = s.size(); // Size of the string

        while (i < n) {
            // Skip leading spaces
            while (i < n && s[i] == ' ')
                i++;

            // Find the end of the current word
            while (i < n && s[i] != ' ')
                s[end++] = s[i++];

            if (start < end) {
                // Reverse the current word
                reverse(s.begin() + start, s.begin() + end);

                // Add a space after the reversed word
                s[end++] = ' ';

                // Update the start index for the next word
                start = end;
            }
            i++;
        }

        // Remove extra space at the end if present
        if (end > 0)
            s.resize(end - 1);

        return s;
    }
};
```

#### Java

```java
class Solution {
    public String reverseWords(String s) {
        // Reverse the entire string
        StringBuilder sb = new StringBuilder(s);
        sb.reverse();
        s = sb.toString();

        int start = 0; // Start index of the current word
        int end = 0;   // End index of the current word
        int i = 0;     // Current index
        int n = s.length(); // Length of the string

        sb = new StringBuilder(); // Create a new StringBuilder to store the result

        while (i < n) {
            // Skip leading spaces
            while (i < n && s.charAt(i) == ' ')
                i++;

            // Find the end of the current word
            start = i;
            while (i < n && s.charAt(i) != ' ')
                i++;

            if (start < i) {
                // Reverse the current word
                StringBuilder reversedWord = new StringBuilder(s.substring(start, i));
                reversedWord.reverse();

                // Add the reversed word to the result StringBuilder
                sb.append(reversedWord);

                // Add a space after the reversed word
                sb.append(' ');
            }
        }

        // Remove extra space at the end if present
        if (sb.length() > 0)
            sb.setLength(sb.length() - 1);

        return sb.toString();
    }
}
```







## [103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/?envType=list&envId=o8wvvpl2)[👎]
Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** [[3],[20,9],[15,7]]

**Example 2:**

**Input:** root = [1]
**Output:** [[1]]

**Example 3:**

**Input:** root = []
**Output:** []

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-100 <= Node.val <= 100`

### Solution
```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
   TreeNode c=root;
   List<List<Integer>> ans =new ArrayList<List<Integer>>();
   if(c==null) return ans;
   Stack<TreeNode> s1=new Stack<TreeNode>();
   Stack<TreeNode> s2=new Stack<TreeNode>();
   s1.push(root);
   while(!s1.isEmpty()||!s2.isEmpty())
   {
       List<Integer> tmp=new ArrayList<Integer>();
        while(!s1.isEmpty())
        {
            c=s1.pop();
            tmp.add(c.val);
            if(c.left!=null) s2.push(c.left);
            if(c.right!=null) s2.push(c.right);
        }
        ans.add(tmp);
        tmp=new ArrayList<Integer>();
        while(!s2.isEmpty())
        {
            c=s2.pop();
            tmp.add(c.val);
            if(c.right!=null)s1.push(c.right);
            if(c.left!=null)s1.push(c.left);
        }
        if(!tmp.isEmpty()) ans.add(tmp);
   }
   return ans;
}
```

Because of the FILO property of stack, when you fill up a stack with one level of node, the output order of stack is reversed order of the input order. So you do it level by level, you will get zigzag order. Hope it helps.

`while(!s1.isEmpty()||!s2.isEmpty())`

is not necessary, because when s1 is empty s2 must be empty, so just judge

`while(!s1.isEmpty())` is enough.

### [Solution Page](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/solutions/33904/java-double-stack-solution/?envType=list&envId=o8wvvpl2)





## [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/description/?envType=list&envId=o8wvvpl2)[👍]
Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = [[1,3],[2,6],[8,10],[15,18]]
**Output:** [[1,6],[8,10],[15,18]]
**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals = [[1,4],[4,5]]
**Output:** [[1,5]]
**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

- 1 <= intervals.length <= 10<sup>4</sup>
- `intervals[i].length == 2`
- 0 <= starti <= endi <= 10<sup>4</sup>

### Solution

> **Note:** Debug sortIntervals is s not working properly.
```java
class Solution {
    public int[][] merge(int[][] intervals) {

        sortIntervals(intervals);
        List<int[]> list = new ArrayList<>();

        int i = 0;

        while(i < intervals.length){
            int[] bound = intervals[i];
            while(i < intervals.length && in(intervals[i], bound[1])){
                bound[1] = Math.max(intervals[i][1], bound[1]);
                i++;
            }

            list.add(bound);

        }

        int[][] mergedIntervals = new int[list.size()][2];
        for(i = 0; i < mergedIntervals.length; i++){
            mergedIntervals[i] = list.get(i);
        }

        return mergedIntervals;
        
    }

    static boolean in(int[] array, int val){
        return val >= array[0] && (val <= array[1] || val > array[1]);
    }

    static void sortIntervals(int[][] intervals){
        for(int i = 0; i < intervals.length; i++){
            for(int j = i + 1; j < intervals.length - i; j++){
                if(isLess(intervals[j], intervals[i])){
                    swap(intervals, i, j);
                }
            }
        }
    }

    static boolean isLess(int[] int1, int[] int2){
        return int1[0] < int2[0];
    }

    static void swap(int[][] array, int idx1, int idx2){
        int[] temp = array[idx1];
        array[idx1] = array[idx2];
        array[idx2] = temp;
    }
}
```

### Solution 2
```java
class Solution {
    public int[][] merge(int[][] intervals) {

        Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));
        List<int[]> list = new ArrayList<>();

        int i = 0;

        while(i < intervals.length){
            int[] bound = intervals[i];
            while(i < intervals.length && in(intervals[i], bound[1])){
                bound[1] = Math.max(intervals[i][1], bound[1]);
                i++;
            }

            list.add(bound);

        }

        int[][] mergedIntervals = new int[list.size()][2];
        for(i = 0; i < mergedIntervals.length; i++){
            mergedIntervals[i] = list.get(i);
        }

        return mergedIntervals;
        
    }

    static boolean in(int[] array, int val){
        return val >= array[0] && (val <= array[1] || val > array[1]);
    }

    
}
```

### Solution 3
The idea is to sort the intervals by their starting points. Then, we take the first interval and compare its end with the next intervals starts. As long as they overlap, we update the end to be the max end of the overlapping intervals. Once we find a non overlapping interval, we can add the previous "extended" interval and start over.

Sorting takes O(n log(n)) and merging the intervals takes O(n). So, the resulting algorithm takes O(n log(n)).

I used a lambda comparator (Java 8) and a for-each loop to try to keep the code clean and simple.

EDIT: The function signature changed in april 2019.  
Here is a new version of the algorithm with arrays. To make more memory efficient, I reused the initial array (sort of "in-place") but it would be easy to create new subarrays if you wanted to keep the initial data.  
It takes less memory than 99% of the other solutions (sometimes 90% depending on the run) and is more than 10 times faster than the previous version with lists.

```java
class Solution {
	public int[][] merge(int[][] intervals) {
		if (intervals.length <= 1)
			return intervals;

		// Sort by ascending starting point
		Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));

		List<int[]> result = new ArrayList<>();
		int[] newInterval = intervals[0];
		result.add(newInterval);
		for (int[] interval : intervals) {
			if (interval[0] <= newInterval[1]) // Overlapping intervals, move the end if needed
				newInterval[1] = Math.max(newInterval[1], interval[1]);
			else {                             // Disjoint intervals, add the new interval to the list
				newInterval = interval;
				result.add(newInterval);
			}
		}

		return result.toArray(new int[result.size()][]);
	}
}
```

Previous version with lists.

```java
public List<Interval> merge(List<Interval> intervals) {
    if (intervals.size() <= 1)
        return intervals;
    
    // Sort by ascending starting point using an anonymous Comparator
    intervals.sort((i1, i2) -> Integer.compare(i1.start, i2.start));
    
    List<Interval> result = new LinkedList<Interval>();
    int start = intervals.get(0).start;
    int end = intervals.get(0).end;
    
    for (Interval interval : intervals) {
        if (interval.start <= end) // Overlapping intervals, move the end if needed
            end = Math.max(end, interval.end);
        else {                     // Disjoint intervals, add the previous one and reset bounds
            result.add(new Interval(start, end));
            start = interval.start;
            end = interval.end;
        }
    }
    
    // Add the last interval
    result.add(new Interval(start, end));
    return result;
}
```

EDIT: Updated with Java 8 lambda comparator.  
EDIT 25/05/2019: Updated for new method signature.

```csharp
public int[][] merge(int[][] intervals) {
        List<int[]> res = new ArrayList<>();
        if(intervals.length == 0 || intervals == null) return res.toArray(new int[0][]);
        
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        
        int start = intervals[0][0];
        int end = intervals[0][1];
        
        for(int[] i : intervals) {
            if(i[0] <= end) {
                end = Math.max(end, i[1]);
            }
            else {
                res.add(new int[]{start, end});
                start = i[0];
                end = i[1];
            }
        }
        res.add(new int[]{start, end});
       return res.toArray(new int[0][]);
         
    }
```

Mine is similar, but one difference is I use the iterator to iterate through the original list and then directly modify it, So the final results are already in the "intervals" list.

```ruby
	public List<Interval> merge(List<Interval> intervals) {
	if (intervals == null || intervals.isEmpty())
		return intervals;
	Collections.sort(intervals, new Comparator<Interval>() {
		public int compare(Interval i1, Interval i2) {
			if (i1.start != i2.start) {
				return i1.start - i2.start;
			}
			return i1.end - i2.end;
		}
	});
	ListIterator<Interval> it = intervals.listIterator();
	Interval cur = it.next();
	while (it.hasNext()) {
		Interval next = it.next();
		if (cur.end < next.start) {
			cur = next;
			continue;
		} else {
			cur.end = Math.max(cur.end, next.end);
			it.remove();
		}
	}
	return intervals;
}
```

Was asked to solve this question by FB without using the new operator (ie creating new objects). Below is my solution in O(1) space.

```csharp
public class Solution {
    public List<Interval> merge(List<Interval> itv) {
        if (itv == null)    throw new IllegalArgumentException();
        
        Collections.sort(itv, new Comparator<Interval>(){
            @Override
            public int compare(Interval a, Interval b) {
                if (a.start == b.start)     return b.end - a.end;
                return a.start - b.start;
            }
        });
        
        int i = 0;
        while (i < itv.size() - 1) {
            Interval a = itv.get(i), b = itv.get(i + 1);
            if (a.end >= b.start) {
                a.end = Math.max(a.end, b.end);
                itv.remove(i + 1);
            }
            else    i++;
        }
        return itv;
    }
}
```

## [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)[👍]
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store_.

**Notice** that you may not slant the container.

**Example 1:**

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

**Input:** height = [1,8,6,2,5,4,8,3,7]
**Output:** 49
**Explanation:** The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

**Example 2:**

**Input:** height = [1,1]
**Output:** 1

**Constraints:**

- `n == height.length`
- 2 <= n <= 10<sup>5</sup>
- 0 <= height[i] <= 10<sup>4</sup>

### Solution - My Submission

**Brute Force Method**
Last Executed Input

---

[6801,4040,7716,493,526,2755,957,1298,2477,6189,6442,8476,4745,8663,2812,8476,3802,7743,7746,2513,4434,3625,2470,4902,8135,5773,5457,4527,6798,8800,8824,9067,3494,915,68,4671,5868,7224,371,4667,38,595...

```java
import static java.lang.Math.max;
import static java.lang.Math.min;
class Solution {
    public int maxArea(int[] height) {

			int area = 0;

			for(int i = 0; i< height.length; i++){
					for(int j = i + 1; j < height.length; j++){
							area = max(area, trap(height, i, j));
					}
			}

      return area;
    }

    static int trap(int[] height, int i, int j) {
			int mini = min(height[i], height[j]);
			return (j - i)*mini;
	}
}
```
**Final Submission - Optimized and understood from the trapping rain water**
```java
import static java.lang.Math.max;

class Solution {

    public int maxArea(int[] height) {

      int area = 0;

      int l = 0, r = height.length - 1;

  

      while(l < r){

        if(height[l] < height[r]){

          area = max(area, (r - l)*height[l++]);

        } else {

          area = max(area, (r - l)*height[r--]);

        }

      }

  

      return area;

    }

  

}
```

### Solution
How's going Ladies - n - Gentlemen, today we are going to solve another coolest problem i.e **Container With Most Water**

Okay, so let's understand what the problem statement is saying,

```php
You are given an integer array height of length n

Return the maximum amount of water a container can store.
```

Let's take one example in order to understand this problem,  
**Input**: height = [1,8,6,2,5,4,8,3,7]  
**Output**: 49

![image](https://assets.leetcode.com/users/images/8e3e5a1c-7a11-401d-a4d7-03cce76fd7f3_1649120493.739683.png)

So, we need to find max area in which most water can contains, where **`area = width * height`**

As, **height** is already given in our Array!  
But what about **width?**

So, to find **width** of a container, all we have to do is get the difference of line.

```
8				|	                                    |
7				|	                                    |	            |
6				|	    |	                            |	            |
5				|	    |	            |	            |	            |
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	            ^                                       ^
```

So, my one pointer is on index 1 & another pointer is on index 6

Therefore, **`width = right - left`** i.e. **`6 - 1 => 5`**

And if we look at height,  
**`height = min(8, 8)`**  
Thus, area will be:-  
**`area = 5 * 8 => 40`**

Now you'll ask why we are choosing the min height because, the water we fill in our container will got overflow, so to avoid that we are gabbing the min line.

So, now you ask. How do we solve this problem efficiently. We gonna solve this in linear time.

So, for that we have

```python
> max area which is intially 0
> Then, we going to have 2 pointers. One in left start at 0th index & one right start from last index.
```

Now, if I calculate the width & height our area will be:

```swift
8				|	                                    |
7				|	                                    |	            |                             width = 8 - 0 = 8
6				|	    |	                            |	            |                             height = min(1, 7)
5				|	    |	            |	            |	            |                             Area = 8 * 1 = 8
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 0 -> max = 8
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	   ^                                                                ^
	  left                                                            right
```

By this pretty much we have get one formula all it is **`area = width * height`**  
i.e. **`area = (right - left) * min(height[left], height[right])`**

So, now you ask which pointer we suppose to move. It's preety simple. We gonna move the smaller height pointer. **Why?**  
Because, we are trying to find very max. container

If we have smaller height on left or right we don't care about it. We always want a higher height line on our left & right.

**Okay, so now moving forward.** left pointer has smaller height, so it will move forward

```swift
8				|	                                    |
7				|	                                    |	            |                             width = 8 - 1 = 7
6				|	    |	                            |	            |                             height = min(8, 7)
5				|	    |	            |	            |	            |                             Area = 7 * 7 = 49
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 8 -> max = 49
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	            ^                                                       ^
	           left                                                   right
```

**Okay, so now moving forward.** right pointer has smaller height, so it will move backward

```python
8				|	                                    |
7				|	                                    |	            |                             width = 7 - 1 = 6
6				|	    |	                            |	            |                             height = min(8, 3)
5				|	    |	            |	            |	            |                             Area = 6 * 3 = 18
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 49
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	            ^                                               ^
	           left                                           right
```

**Okay, so now moving forward.** right pointer has smaller height, so it will move backward

```python
8				|	                                    |
7				|	                                    |	            |                             width = 6 - 1 = 5
6				|	    |	                            |	            |                             height = min(8, 8)
5				|	    |	            |	            |	            |                             Area = 8 * 5 = 40
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 49
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	            ^                                       ^
	           left                                   right
```

**Okay, so now moving forward.** now left & right pointer both have same height, so in this case we gonna move both the pointer's!!

```python
8				|	                                    |
7				|	                                    |	            |                             width = 5 - 2 = 3
6				|	    |	                            |	            |                             height = min(4, 6)
5				|	    |	            |	            |	            |                             Area = 4 * 3 = 12
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 49
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	                    ^                       ^
	                   left                   right
```

**Okay, so now moving forward.** right pointer has smaller height, so it will move backward

```python
8				|	                                    |
7				|	                                    |	            |                             width = 4 - 2 = 2
6				|	    |	                            |	            |                             height = min(5, 6)
5				|	    |	            |	            |	            |                             Area = 5 * 2 = 10
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 49
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	                    ^               ^
	                   left           right
```

**Okay, so now moving forward.** right pointer has smaller height, so it will move backward

```python
8				|	                                    |
7				|	                                    |	            |                             width = 3 - 2 = 1
6				|	    |	                            |	            |                             height = min(2, 6)
5				|	    |	            |	            |	            |                             Area = 2 * 1 = 2
4				|	    |	            |	    |	    |	            |
3				|	    |	            |	    |	    |	    |	    |                             max = 49
2				|	    |	    |	    |	    |	    |	    |	    |
1	   |	    |	    |	    |	    |	    |	    |	    |	    |
       0        1       2       3       4       5       6       7       8
	                    ^       ^
	                   left   right
```

The max area we get is **49**

I hope so, ladies & gentlemen approach is clear, **Let's code it**

**Java**

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int max = 0;
        while(left < right){
            int w = right - left;
            int h = Math.min(height[left], height[right]);
            int area = h * w;
            max = Math.max(max, area);
            if(height[left] < height[right]) left++;
            else if(height[left] > height[right]) right--;
            else {
                left++;
                right--;
            }
        }
        return max;
    }
}
```

**C++**

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0;
        int right = height.size() - 1;
        int maxi = 0;
        while(left < right){
            int w = right - left;
            int h = min(height[left], height[right]);
            int area = h * w;
            maxi = max(maxi, area);
            if(height[left] < height[right]) left++;
            else if(height[left] > height[right]) right--;
            else {
                left++;
                right--;
            }
        }
        return maxi;
    }
};
```

ANALYSIS :-

- **Time Complexity :-** BigO(N)
    
- **Space COmplexity :-** BigO(1)


### Solution 2
_(Note: This is part of a series of Leetcode solution explanations. If you like this solution or find it useful,_ _**please upvote**_ _this post.)_

---

_**Idea:**_

The first thing we should realize is that the amount of water contained is always going to be a rectangle whose area is defined as **length * width**. The width of any container will be the difference between the index of the two lines (**i** and **j**), and the height will be whichever of the two sides is the lowest (**min(H[i], H[j])**).

The brute force approach would be to compare every single pair of indexes in **H**, but that would be far too slow. Instead, we can observe that if we start with the lines on the opposite ends and move inward, the only possible time the area could be larger is when the height increases, since the width will continuously get smaller.

This is very easily observed with the use of visuals. Let's say we start with a graph of **H** like this:

![Visual 1](https://i.imgur.com/2xU6MPx.png)

The first step would be to find our starting container described by the lines on either end:

![Visual 2](https://i.imgur.com/bWpX3VY.png)

We can tell that the line on the right end will never make a better match, because any further match would have a smaller width and the container is already the maximum height that that line can support. That means that our next move should be to slide **j** to the left and pick a new line:

![Visual 3](https://i.imgur.com/pcyUfzx.png)

This is a clear improvement over the last container. We only moved over one line, but we more than doubled the height. Now, it's the line on the left end that's the limiting factor, so the next step will be to slide **i** to the right. Just looking at the visual, however, it's obvious that we can skip the next few lines because they're already underwater, so we should go to the first line that's larger than the current water height:

![Visual 4](https://i.imgur.com/25MGHYY.png)

This time, it doesn't look like we made much of a gain, despite the fact that the water level rose a bit, because we lost more in width than we made up for in height. That means that we always have to check at each new possible stop to see if the new container area is better than the current best. Just lik before we can slide **j** to the left again:

![Visual 5](https://i.imgur.com/c4VBpqn.png)

This move also doesn't appear to have led to a better container. But here we can see that it's definitely possible to have to move the same side twice in a row, as the **j** line is still the lower of the two:

![Visual 6](https://i.imgur.com/R6AAkNd.png)

This is obviously the last possible container to check, and like the last few before it, it doesn't appear to be the best match. Still, we can understand that it's entirely possible for the best container in a different example to be only one index apart, if both lines are extremely tall.

Putting together everything, it's clear that we need to make a **2-pointer sliding window solution**. We'll start from either end and at each step we'll check the container area, then we'll shift the lower-valued pointer inward. Once the two pointers meet, we know that we must have exhausted all possible containers and we should **return** our answer (**ans**).

---

_**Implementation:**_

Javascript was weirdly more performant when using both **Math.max()** and **Math.min()** rather than performing more basic comparisons, even with duplicated effort in the ternary.

For the other languages, it made more sense (and was ultimately more performant) to only have to do the basic comparisons once each.

---

_**Javascript Code:**_

The best result for the code below is **68ms / 41.1MB** (beats 100% / 41%).

```javascript
var maxArea = function(H) {
    let ans = 0, i = 0, j = H.length-1
    while (i < j) {
        ans = Math.max(ans, Math.min(H[i], H[j]) * (j - i))
        H[i] <= H[j] ? i++ : j--
    }
    return ans
};
```

---

_**Python Code:**_

The best result for the code below is **140ms / 16.4MB** (beats 100% / 75%).

```java
class Solution:
    def maxArea(self, H: List[int]) -> int:
        ans, i, j = 0, 0, len(H)-1
        while (i < j):
            if H[i] <= H[j]:
                res = H[i] * (j - i)
                i += 1
            else:
                res = H[j] * (j - i)
                j -= 1
            if res > ans: ans = res
        return ans
```

---

_**Java Code:**_

The best result for the code below is **1ms / 40.3MB** (beats 100% / 88%).

```cpp
class Solution {
    public int maxArea(int[] H) {
        int ans = 0, i = 0, j = H.length-1, res = 0;
        while (i < j) {
            if (H[i] <= H[j]) {
                res = H[i] * (j - i);
                i++;
            } else {
                res = H[j] * (j - i);
                j--;
            }
            if (res > ans) ans = res;
        }
        return ans;
    }
}
```

---

_**C++ Code:**_

The best result for the code below is **12ms / 17.6MB** (beats 100% / 100%).

```cpp
class Solution {
public:
    int maxArea(vector<int>& H) {
        int ans = 0, i = 0, j = H.size()-1, res = 0;
        while (i < j) {
            if (H[i] <= H[j]) {
                res = H[i] * (j - i);
                i++;
            } else {
                res = H[j] * (j - i);
                j--;
            }
            if (res > ans) ans = res;
        }
        return ans;
    }
};
```


### Solution 3
[Leetcode](https://leetcode.com/) [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/).

Here shows **2** Approaches to slove this problem: **Brute Force** and **Two Pointers**.

#### Intuition

![Problem 11](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

Suppose two pointers iii, jjj, the heights of the vertical lines are h[i]h[i]h[i], h[j]h[j]h[j], and the area in this state is S(i,j)S(i, j)S(i,j).

As we all known, the container is determined by the short line, the area formula can be easily obtained:

S(i,j)=min(h[i],h[j])×(j−i)S(i, j)= min(h[i], h[j]) \times (j - i)S(i,j)=min(h[i],h[j])×(j−i)

#### Brute Froce

It's easy to use the brute force approach, the total states is C(n,2)=n×(n−1)/2C(n, 2)= n \times (n - 1) / 2C(n,2)=n×(n−1)/2, we have to **enumerate all these states** to get the max area.

The time complexity is O(n2)O(n^2)O(n2), exceed the time limit.

```python
    // BF time: O(n^2) space: O(1)
    // TimeOut
    public static int maxArea_bf(int[] height) {
        int len = height.length;
        int max = 0;
        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                int area = Math.min(height[i], height[j]) * (j - i);
                max = Math.max(max, area);
            }
        }

        return max;
    }
```

##### Analysis

- **Time Complexity**: O(n<sup>2</sup>)
- **Space Complexity**: O(1)

#### Two Pointers

In each state S(i,j)S(i, j)S(i,j), no matter whether the left line or right line moves to the middle, it will cause less wide to width−1width - 1width−1:

- Move the short line, the short line min(h[i],h[j])min(h[i], h[j])min(h[i],h[j]) of the container may hold more water, the area may increase.
- Move the long line, the short line min(h[i],h[j])min(h[i], h[j])min(h[i],h[j]) of the container will **remain the same or less**, so the area will definitely become less.

Therefore, we can use two pointers to the left and right line of the container. We move the short line in each round, update the max area until the two pointers met each other as the below pictures show.

![Problem 11 1](https://assets.leetcode.com/users/images/1bbdebff-40e8-43b6-b975-050eced682e6_1649125223.181647.png)

![Problem 11 2](https://assets.leetcode.com/users/images/e7d55353-7491-44b2-af67-51e4aeee414f_1649125223.358524.png)

![Problem 11 3](https://assets.leetcode.com/users/images/395bbe7e-1218-4750-a744-21c590c5981c_1649125223.3798895.png)

##### Proof

Assuming that h[i]<h[j]h[i] \lt h[j]h[i]<h[j] under the state S(i,j)S(i, j)S(i,j), move the short line to S(i+1,j)S(i + 1, j)S(i+1,j), which means that we eliminate S(i,j−1),S(i,j−2),...,S(i,i+1)S(i, j - 1), S(i, j - 2), ... , S(i, i + 1)S(i,j−1),S(i,j−2),...,S(i,i+1) states. The area of all eliminated states must be smaller than the current area:

1. Short line height: same or less than S(i,j)S(i, j)S(i,j) (≤h[i]\le h[i]≤h[i]);
2. Width: less than S(i,j)S(i, j)S(i,j).

Therefore, each round moves the short line, and all the eliminated states will not cause the loss of the maximum area.

```python
    // Two Pointers time: O(n) space: O(1)
    public static int maxArea_tp(int[] height) {
        int len = height.length;
        int left = 0;
        int right = len - 1;
        int max = Math.min(height[left], height[right]) * (right - left);
        while (left < right) {
            // Move the shorter lines each time
            if (height[left] <= height[right]) {
                left++;
            } else {
                right--;
            }

            // update the max area
            max = Math.max(max, Math.min(height[left], height[right]) * (right - left));
        }

        return max;
    }
```

##### Analysis

- **Time Complexity**: O(n)
- **Space Complexity**: O(1)





## [396. Rotate Function](https://leetcode.com/problems/rotate-function/description/)[👎]
You are given an integer array `nums` of length `n`.

Assume `arrk` to be an array obtained by rotating `nums` by `k` positions clock-wise. We define the **rotation function** `F` on `nums` as follow:

- `F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1].`

Return _the maximum value of_ `F(0), F(1), ..., F(n-1)`.

The test cases are generated so that the answer fits in a **32-bit** integer.

**Example 1:**

**Input:** nums = [4,3,2,6]
**Output:** 26
**Explanation:**
F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26
So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.

**Example 2:**

**Input:** nums = [100]
**Output:** 0

**Constraints:**

- `n == nums.length`
- 1 <= n <= 10<sup>5</sup>
- `-100 <= nums[i] <= 100`

### Solution
my brute force approach (45/58 testcases passed)
```java
class Solution {

    public int maxRotateFunction(int[] nums) {

        int SOP = sop(nums);

        int maxSOP = SOP;

        for(int i = 0; i < nums.length - 1; i++){

            rr(nums);

            SOP = sop(nums);

            maxSOP = Math.max(SOP, maxSOP);

        }

  

        return maxSOP;

    }

  

    static void rr(int[] nums){

        if(nums.length <=1) return;

        int end = nums[nums.length - 1];

        for(int i = nums.length - 2; i >= 0; i--){

            nums[i+1] = nums[i];

        }

        nums[0] = end;

    }

  

    static int sop(int[] nums){

        int ans = 0;

        for(int i = 0;i < nums.length; i++){

            ans += (i*nums[i]);

        }

        return ans;

    }

}
```

### Solution 1
**EXPLANATION**

Let us do some pre-processing using basic Maths.

Let the array elements be: [_a b c d e_].

**Length of array _represented by N_** = 5  
**Sum of elements of array _represented by SUM_** = a + b + c + d + e

Now, as per the question :

F(0) = (0 * a) + (1 * b) + (2 * c) + (3 * d) + (4 * e) = 0 + b + 2c + 3d + 4e  
F(1) = (1 * a) + (2 * b) + (3 * c) + (4 * d) + (0 * e) = a + 2b + 3c + 4d + 0  
F(2) = (2 * a) + (3 * b) + (4 * c) + (0 * d) + (1 * e) = 2a + 3b + 4c + 0 + e

Now subtracting 2 equations,

**F(1) - F(0)** = a + b + c + d - 4e = a + b + c + d + e - 5e  
Therefore, **F(1)** = **F(0)** + a + b + c + d + e - 5e = **F(0) + SUM - N***e

**F(2) - F(1)** = a + b + c + e - 4d = a + b + c + d + e - 5d  
Therefore, **F(2)** = **F(1)** + a + b + c + d + e - 5d = **F(1) + SUM - N***d

Generalizing it, we get the following relation:

**F(K) = F(K-1) + SUM - N * (( K-1)th element from end of array)**  
i.e. **F(K) = F(K-1) + SUM - N * (array [N - 1 - (K-1)])** = **F(K-1) + SUM - N * (array [N - K])**

Now, I think it is pretty much clear that we can use a 1D DP array to solve this question as depicted in the code below.

_------Please upvote if you liked the solution. Please put your thoughts/doubts/queries in the comment section below. I will try my best to answer them.------_

```python
class Solution {
    public int maxRotateFunction (int[] A) {
        if (A == null || A.length == 0)
            return 0;
        int sum = 0, F0 = 0, max = Integer.MIN_VALUE;
        for (int i = 0; i < A.length; i++) {
            sum += A [i];
            F0 += i * A [i];
        }
        int dp [] = new int [A.length];
        dp [0] = F0;
        max = dp [0];
        for (int i = 1; i < A.length; i++) {
            dp [i] = dp [i-1] + sum - A.length * A [A.length - i];
            max = Math.max (max, dp [i]);
        }
        return max;
    }
}
```

Great solution, but no need to maintain DP. It is enough to maintain previous value.

```cpp
int maxRotateFunction(vector<int>& nums) {
    int maxval,sum=0,F0=0,cur,prev,n=nums.size();
    for(int i=0;i<n;i++)
    {
        sum+=nums[i];
        F0+=i*nums[i];
    }
    maxval=F0;
    prev=F0;
    for(int i=1;i<n;i++)
    {
        cur=prev+sum-n*nums[n-i];
        prev=cur;
        maxval=max(cur,maxval);
    }
    return maxval;
    }
```

### Solution 2
Consider we have 5 coins A,B,C,D,E

According to the problem statement  
F(0) = (0_A) + (1_B) + (2_C) + (3_D) + (4_E)  
F(1) = (4_A) + (0_B) + (1_C) + (2_D) + (3_E)  
F(2) = (3_A) + (4_B) + (0_C) + (1_D) + (2*E)

This problem at a glance seem like a difficult problem. I am not very strong in mathematics, so this is how I visualize this problem

We can construct F(1) from F(0) by two step:  
Step 1. taking away one count of each coin from F(0), this is done by subtracting "sum" from "iteration" in the code below  
after step 1 F(0) = (-1_A) + (0_B) + (1_C) + (2_D) + (3*E)

Step 2. Add n times the element which didn't contributed in F(0), which is A. This is done by adding "A[j-1]_len" in the code below.  
after step 2 F(0) = (4_A) + (0_B) + (1_C) + (2_D) + (3_E)

At this point F(0) can be considered as F(1) and F(2) to F(4) can be constructed by repeating the above steps.

Hope this explanation helps, cheers!

```java
    public int maxRotateFunction(int[] A) {
        if(A.length == 0){
            return 0;
        }
        
        int sum =0, iteration = 0, len = A.length;
        
        for(int i=0; i<len; i++){
            sum += A[i];
            iteration += (A[i] * i);
        }
        
        int max = iteration;
        for(int j=1; j<len; j++){
            // for next iteration lets remove one entry value of each entry and the prev 0 * k
            iteration = iteration - sum + A[j-1]*len;
            max = Math.max(max, iteration);
        }
        
        return max;
    }
```

### Solution 2
```
F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1]
F(k-1) = 0 * Bk-1[0] + 1 * Bk-1[1] + ... + (n-1) * Bk-1[n-1]
       = 0 * Bk[1] + 1 * Bk[2] + ... + (n-2) * Bk[n-1] + (n-1) * Bk[0]
```

Then,

```python
F(k) - F(k-1) = Bk[1] + Bk[2] + ... + Bk[n-1] + (1-n)Bk[0]
              = (Bk[0] + ... + Bk[n-1]) - nBk[0]
              = sum - nBk[0]
```

Thus,

```python
F(k) = F(k-1) + sum - nBk[0]
```

What is Bk[0]?

```python
k = 0; B[0] = A[0];
k = 1; B[0] = A[len-1];
k = 2; B[0] = A[len-2];
...
```

```python
int allSum = 0;
int len = A.length;
int F = 0;
for (int i = 0; i < len; i++) {
    F += i * A[i];
    allSum += A[i];
}
int max = F;
for (int i = len - 1; i >= 1; i--) {
    F = F + allSum - len * A[i];
    max = Math.max(F, max);
}
return max;   
```






## [796. Rotate String](https://leetcode.com/problems/rotate-string/description/)[👍]
Given two strings `s` and `goal`, return `true` _if and only if_ `s` _can become_ `goal` _after some number of **shifts** on_ `s`.

A **shift** on `s` consists of moving the leftmost character of `s` to the rightmost position.

- For example, if `s = "abcde"`, then it will be `"bcdea"` after one shift.

**Example 1:**

**Input:** s = "abcde", goal = "cdeab"
**Output:** true

**Example 2:**

**Input:** s = "abcde", goal = "abced"
**Output:** false

**Constraints:**

- `1 <= s.length, goal.length <= 100`
- `s` and `goal` consist of lowercase English letters.

### My solution - but failed
```java
class Solution {

    public boolean rotateString(String s, String goal) {

        if(s.length() ==0 || goal.length() == 0 || s.length() != goal.length()) return false;

        // find out the s[0] idx in goal

        // which is equal to the number of

        // roatations to be perfomed

        // after roatations if both are equal

        // then return true else false

  

        char firstChar = s.charAt(0);

  

        int k = findIdx(goal, firstChar);

  

        if(k == -1) return false;

  

        s = rr(s, k);

  

        return s.equals(goal);

    }

  

    static int findIdx(String s, char query){

        for(int i = 0; i < s.length(); i++){

            if(s.charAt(i) == query) return i;

        }

  

        return -1;

    }

  

    static String rr(String s, int k){

        if(k == 0) return s;

        char[] array = s.toCharArray();

  

        char[] kArray = new char[k];

  

        for(int i = 0; i < k; i++){

            kArray[i] = array[array.length - k + i];

        }

  

        for(int i = array.length-k-1; i >= 0; i--){

            array[i + k] = array[i];

        }

  

        for(int i = 0; i < k; i++){

            array[i] = kArray[i];

        }

  

        return String.valueOf(array);

    }

}
```

### Solution
There are a couple general solutions. The first is to do a naive O(n^2) time but O(1) solution. The second is to construct a larger string (A + A) and do a simple contains on it, which is shorter but uses O(n) memory. There is a third solution using rolling hashes that is O(n) in both time and space, and the KMP solution which is also O(n) in both, but can skip ahead depending on the prefix. There is also another solution using two-way string-matching [https://en.wikipedia.org/wiki/Two-way_string-matching_algorithm](https://en.wikipedia.org/wiki/Two-way_string-matching_algorithm) that runs in O(n) time and O(1) space by cleverly splitting the string up into two partitions. I won't be going into it because it's beyond the scope of the question.

The thing is, if I were to give out this question, and the applicant gave out the KMP solution from memory, would I really be all that impressed? My interview isn't supposed to test if the interviewee memorized a string matching algorithm beforehand. The KMP solution is long and complicated. As such, it's easy to make a mistake when coding it, and it's harder to maintain than other solutions. Furthermore, the question itself says that the maximum string length is only 100. If you have to build up a whole table of shifts just to calculate if one string is in another, then KMP may be slower than the naive approach in practice, especially if the average string length is closer to 10.

Furthermore, I don't think questions like this are really intended to be as hard as KMP. It's a leetcode easy that would be used as a warm up to a harder problem involving graphs, or dynamic programming. I think a better strategy would be to note the assumptions in the question and to challenge those. For example, what if A and B are both null? Some discussion-given answers ignore the possibility of either being null, some return true if both are null, and some return false. But really, if I give a function two null strings, I would almost certainly want an exception to occur.

```java
class Solution {
    public boolean rotateString(String A, String B) {
        if(A == null || B == null) {
            //throw exception on A and B both being null?
            return false;
        }
        if(A.length() != B.length()) {
            return false;
        }
        if(A.length() == 0) {
            return true;
        }
        for(int i = 0; i < A.length(); i++) {
            if(rotateString(A, B, i)) {
                return true;
            }
        }
        return false;
    }
    
    private boolean rotateString(String A, String B, int rotation) {
        for(int i = 0; i < A.length(); i++) {
            if(A.charAt(i) != B.charAt((i+rotation)%B.length())) {
                return false;
            }
        }
        return true;
    }
}
```

Here is my first solution. I just used the naive solution. It took me about 5 minutes to write it. I think there are some improvements that could be made, for example you could argue that not using braces for simple if statements, and using A.isEmpty() instead of A.length() == 0 for the empty check. You could consider merging the first two false cases. I think that using a function for the inner loop is better than not using one, because not only is that function potentially reusable, it is also easier to document. It's fairly simple to understand what the private function is doing just from the parameters.

I think an ideal interview would start off with a solution by this, making sure to ask about the length of average strings, whether or not this is a hot code path, and the possibility of using an exception rather than just returning false. Then, describe the time and space complexity of this solution. Then, if you have more time, press to figure out the KMP solution to get down to linear time. If you don't feel confident you can figure out the better time complexity answer, then at least describe to the interviewer the possiblity of creating one by using more space.

### Solution 1
```java
class Solution {  
	public boolean rotateString(String s, String goal) {
	
	
	 if(s.length() != goal.length())
	   return false;
	  
	  String ans=s+s;
	  
	  if(ans.contains(goal))
	    return true;
	  else
	    return false;
	}
}
```

### Solution 2
```java
  StringBuilder temp = new StringBuilder(s1);
    
    for(int i=0;i<s1.length();i++){
        temp.deleteCharAt(0);
        temp.append(s1.charAt(i));
        if(temp.toString().equals(s2)){
            return true;
        }
    }
    return false;
}
```

### One Line
C++

```php
return A.size() == B.size() && (A + A).find(B) != string::npos;
```

Java

```kotlin
return A.length() == B.length() && (A + A).contains(B);
```

Python

```python
return len(A) == len(B) and B in A + A
```
















## [18. 4Sum](https://leetcode.com/problems/4sum/description/?envType=list&envId=o8wvvpl2)[👎]
Given an array `nums` of `n` integers, return _an array of all the **unique** quadruplets_ `[nums[a], nums[b], nums[c], nums[d]]` such that:

- `0 <= a, b, c, d < n`
- `a`, `b`, `c`, and `d` are **distinct**.
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,0,-1,0,-2,2], target = 0
**Output:** [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

**Example 2:**

**Input:** nums = [2,2,2,2,2], target = 8
**Output:** [[2,2,2,2]]

**Constraints:**

- `1 <= nums.length <= 200`
- -10<sup>9</sup>  <= nums[i] <= 10<sup>9</sup> 
- 10<sup>9</sup> <= target <= 10<sup>9</sup> 

### Solution - Generalized for K Sum
#### General Idea

If you have already read and implement the 3sum and 4sum by using the sorting approach: reduce them into 2sum at the end, you might already got the feeling that, all ksum problem can be divided into two problems:

1. 2sum Problem
2. Reduce K sum problem to K – 1 sum Problem

Therefore, the ideas is simple and straightforward. We could use recursive to solve this problem. Time complexity is O(N^(K-1)).

```java
    public class Solution {
        int len = 0;
        public List<List<Integer>> fourSum(int[] nums, int target) {
            len = nums.length;
            Arrays.sort(nums);
            return kSum(nums, target, 4, 0);
        }
       private ArrayList<List<Integer>> kSum(int[] nums, int target, int k, int index) {
            ArrayList<List<Integer>> res = new ArrayList<List<Integer>>();
            if(index >= len) {
                return res;
            }
            if(k == 2) {
            	int i = index, j = len - 1;
            	while(i < j) {
                    //find a pair
            	    if(target - nums[i] == nums[j]) {
            	    	List<Integer> temp = new ArrayList<>();
                    	temp.add(nums[i]);
                    	temp.add(target-nums[i]);
                        res.add(temp);
                        //skip duplication
                        while(i<j && nums[i]==nums[i+1]) i++;
                        while(i<j && nums[j-1]==nums[j]) j--;
                        i++;
                        j--;
                    //move left bound
            	    } else if (target - nums[i] > nums[j]) {
            	        i++;
                    //move right bound
            	    } else {
            	        j--;
            	    }
            	}
            } else{
                for (int i = index; i < len - k + 1; i++) {
                    //use current number to reduce ksum into k-1sum
                    ArrayList<List<Integer>> temp = kSum(nums, target - nums[i], k-1, i+1);
                    if(temp != null){
                        //add previous results
                        for (List<Integer> t : temp) {
                            t.add(0, nums[i]);
                        }
                        res.addAll(temp);
                    }
                    while (i < len-1 && nums[i] == nums[i+1]) {
                        //skip duplicated numbers
                        i++;
                    }
                }
            }
            return res;
        }
    }
```

