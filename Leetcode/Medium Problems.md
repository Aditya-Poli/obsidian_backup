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


## 73. Set Matrix Zeroes

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

