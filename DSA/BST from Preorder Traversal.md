# [1008. Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/description/?envType=list&envId=o8wvvpl2)

Given an array of integers preorder, which represents the **preorder traversal** of a BST (i.e., **binary search tree**), construct the tree and return _its root_.

It is **guaranteed** that there is always possible to find a binary search tree with the given requirements for the given test cases.

A **binary search tree** is a binary tree where for every node, any descendant of `Node.left` has a value **strictly less than** `Node.val`, and any descendant of `Node.right` has a value **strictly greater than** `Node.val`.

A **preorder traversal** of a binary tree displays the value of the node first, then traverses `Node.left`, then traverses `Node.right`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/03/06/1266.png)

**Input:** preorder = [8,5,1,7,10,12]
**Output:** [8,5,10,1,7,null,12]

**Example 2:**

**Input:** preorder = [1,3]
**Output:** [1,null,3]

**Constraints:**

- `1 <= preorder.length <= 100`
- `1 <= preorder[i] <= 1000`
- All the values of `preorder` are **unique**.

### Solution
My solution I thought of splitting the array into left and right but didn't strike any so I just inserted into tree by writing the insert function.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode bstFromPreorder(int[] preorder) {
        if(preorder.length == 0){
            return null;
        }
        TreeNode root = null;
        for(int i: preorder){
            root = insert(root, i);
        }
        return root;
    }

    private TreeNode insert(TreeNode root, int data){
        if(root == null){
            return new TreeNode(data);
        } else {
            if(data < root.val){
                root.left = insert(root.left, data);
            } else {
                root.right = insert(root.right, data);
            }
        }
  
        return root;
    }
}
```

which performed worst on memory may be due to the stack space.

### Solution 

#### **Intuition**:

Find the left part and right part,  
then recursively construct the tree.  
  

#### **Solution 1**:

Binary search

**Python, `O(N^2)`**

```ruby
    def bstFromPreorder(self, A):
        if not A: return None
        root = TreeNode(A[0])
        i = bisect.bisect(A, A[0])
        root.left = self.bstFromPreorder(A[1:i])
        root.right = self.bstFromPreorder(A[i:])
        return root
```

**Python, `O(NlogN)`**

```python
    def bstFromPreorder(self, A):
        def helper(i, j):
            if i == j: return None
            root = TreeNode(A[i])
            mid = bisect.bisect(A, A[i], i + 1, j)
            root.left = helper(i + 1, mid)
            root.right = helper(mid, j)
            return root
        return helper(0, len(A))
```

  

#### **Solution 2**

Give the function a bound the maximum number it will handle.  
The left recursion will take the elements smaller than `node.val`  
The right recursion will take the remaining elements smaller than `bound`

**Complexity**  
`bstFromPreorder` is called exactly `N` times.  
It's same as a preorder traversal.  
Time `O(N)`  
Space `O(H)`

**Java**

```java
    int i = 0;
    public TreeNode bstFromPreorder(int[] A) {
        return bstFromPreorder(A, Integer.MAX_VALUE);
    }

    public TreeNode bstFromPreorder(int[] A, int bound) {
        if (i == A.length || A[i] > bound) return null;
        TreeNode root = new TreeNode(A[i++]);
        root.left = bstFromPreorder(A, root.val);
        root.right = bstFromPreorder(A, bound);
        return root;
    }
```

**C++**

```cpp
    int i = 0;
    TreeNode* bstFromPreorder(vector<int>& A, int bound = INT_MAX) {
        if (i == A.size() || A[i] > bound) return NULL;
        TreeNode* root = new TreeNode(A[i++]);
        root->left = bstFromPreorder(A, root->val);
        root->right = bstFromPreorder(A, bound);
        return root;
    }
```

**Python**

```python
    i = 0
    def bstFromPreorder(self, A, bound=float('inf')):
        if self.i == len(A) or A[self.i] > bound:
            return None
        root = TreeNode(A[self.i])
        self.i += 1
        root.left = self.bstFromPreorder(A, root.val)
        root.right = self.bstFromPreorder(A, bound)
        return root
```

  

#### Solution 2.1

Some may don't like the global variable `i`.  
Well, I first reused the function in python,  
so I had to use it, making it a "stateful" function.

I didn't realize there would be people who care about it.  
If it's really matters,  
We can discard the usage of global function.

**C++**

```cpp
    TreeNode* bstFromPreorder(vector<int>& A) {
        int i = 0;
        return build(A, i, INT_MAX);
    }

    TreeNode* build(vector<int>& A, int& i, int bound) {
        if (i == A.size() || A[i] > bound) return NULL;
        TreeNode* root = new TreeNode(A[i++]);
        root->left = build(A, i, root->val);
        root->right = build(A, i, bound);
        return root;
    }
```

**Java**

```java
    public TreeNode bstFromPreorder(int[] A) {
        return bstFromPreorder(A, Integer.MAX_VALUE, new int[]{0});
    }

    public TreeNode bstFromPreorder(int[] A, int bound, int[] i) {
        if (i[0] == A.length || A[i[0]] > bound) return null;
        TreeNode root = new TreeNode(A[i[0]++]);
        root.left = bstFromPreorder(A, root.val, i);
        root.right = bstFromPreorder(A, bound, i);
        return root;
    }
```

**Python**

```ruby
    def bstFromPreorder(self, A):
        return self.buildTree(A[::-1], float('inf'))

    def buildTree(self, A, bound):
        if not A or A[-1] > bound: return None
        node = TreeNode(A.pop())
        node.left = self.buildTree(A, node.val)
        node.right = self.buildTree(A, bound)
        return node
```



### Solution
ok lets do this!!  
so we are given an array which is the preorder traversal of the some tree!  
we are used to traverse a tree a but are not privy to reconstruct the tree from the array!!  
anyways!!!  
so we are given an array whose first element is the root of out tree!!(because of preorder traversal)!  
NOTE:this is not a linear solution!i have posted linear solutions here [https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/discuss/589801/JAVA-3-WAYS-TO-DO-THE-PROBLEM!-O(N)-APPROACH](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/discuss/589801/JAVA-3-WAYS-TO-DO-THE-PROBLEM!-O(N)-APPROACH)  
BUT i strongly suggest you go through this soution below so that you can get the gist of the logic and then move on to the more complex linear solutions i posted!

LETS DO THIS:

so we follow steps:  
1>we create the node  
2>we traverse the array for values which are less than the current node!-- these values will become our left subtree.we stop whenever we get a value larger than the current root of the subtree!  
3>we take the rest of the array(values whuch are greater than the value of the current root)-these are the values which will make out right subtree!

so we make a root!  
make the left subtree(recursively)  
then make right subtree(recursively)

code here!!  
do a couple of dry runs!  
u will get it!

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode bstFromPreorder(int[] preorder) {
     return helper(preorder, 0, preorder.length - 1);   
    }
    
    private TreeNode helper(int[] preorder, int start, int end) {
        if(start > end) return null;
        
        TreeNode node = new TreeNode(preorder[start]);
        int i;
        for(i=start;i<=end;i++) {
        if(preorder[i] > node.val)
            break;
        }
        
        node.left = helper(preorder, start+1, i-1);
        node.right = helper(preorder, i, end);
        return node;
        
        
        
    }
    
    
}
```

### Solution

THIS IS A CONTINUATION OF MY PREVIOUS POST!  
WHICH HAD O(N^2) APPROACH!  
[https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/discuss/589059/java-easiest-solution-with-clear-explanation-of-logic](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/discuss/589059/java-easiest-solution-with-clear-explanation-of-logic)

AS A LOT OF PEOPLE ARE ASKING FOR LINEAR SOLUTONS HERE IT IS!

APPROACH 1-O(N)  
JAVA-LOWER AND UPPER BOUND RECURSIVE

```java
class Solution {
    int nodeIndex;
    public TreeNode bstFromPreorder(int[] preorder) {
        if(preorder == null) {
            return null;
        }
        nodeIndex = 0;
        return bstHelper(preorder, Integer.MIN_VALUE , Integer.MAX_VALUE);
    }
    private TreeNode bstHelper(int[] preorder, int start, int end) {
        if(nodeIndex == preorder.length || preorder[nodeIndex]<start || preorder[nodeIndex]>end) {
            return null;
        }
        int val = preorder[nodeIndex++];
        TreeNode node = new TreeNode(val);
        node.left = bstHelper(preorder, start, val);
        node.right = bstHelper(preorder, val, end);
        return node;   
    }   
} 
```

APPROACH 2- O(N)!  
JAVA ONLY UPPER BOUND- RECURSIVE  
EXPLANATION-  
Every node has an upper bound.

Left node is bounded by the parent node's value.  
Right node is bounded by the ancestor's bound.  
Using the example in the question:  
The nodes [5, 1, 7] are all bounded by 8.  
The node 1 is bounded by 5.  
8 is the root node, but if you think deeper about it, it is bounded by Integer.MAX_VALUE. i.e. imagine there is a root parent node Integer.MAX_VALUE with left node being 8.  
This also means that both 10 and 12 nodes, which are also right nodes, are also bounded by Integer.MAX_VALUE.  
We use a recursive function together with an outer index variable i to traverse and construct the tree. When we create a tree node, we increment i to process the next element in the preorder array.

We don't need to care about lower bound. When we construct the tree, we try to create left node first. If the condition fails (i.e. current number is greater than the parent node value), then we try to create the right node which automatically satisfies the condition, hence no lower bound is needed

```php
class Solution {
int i = 0;
    public TreeNode bstFromPreorder(int[] arr) {
        return helper(arr, Integer.MAX_VALUE);
    }

    public TreeNode helper(int[] arr, int bound) {
        if (i == arr.length || arr[i] > bound) return null;
        TreeNode root = new TreeNode(arr[i++]);
        root.left = helper(arr, root.val);
        root.right = helper(arr, bound);
        return root;
    }
	}
	```
	
EXPLANATON-
"explanation- It is  possible to do this because when we construct the " left child " the upper bound will be the node value itself and no lower bound will be needed!
	-no lower bound is required for "right child" because we have arrived at this point of creating the right child only because these elements failed to satisfy the left subtree conditions!"
	
 
```java

APPROACH 3-IF YOU ARE NOT COMFORTABLE WITH RECURSION!  
JAVA ITERATIVE APPROACH -

```java
class Solution {
    public TreeNode bstFromPreorder(int[] preorder) {
        
        if(preorder == null){
            return null;
        }
        int size = preorder.length;
        if(size==0){
            return null;
        }
        TreeNode root = new TreeNode(preorder[0]);
		
        for(int i=1;i<size;i++){
             generateBST(preorder[i],root);
        }
        return root;
    }
    
    public void generateBST(int target, TreeNode tree){
        TreeNode root = tree;
        TreeNode node = new TreeNode(target);
            while(root!=null){
                if(target<root.val){
                    if(root.left==null){
                        root.left = node;
                        break;
                    }
                    else{
                         root=root.left;
                    }
                }else{
                    if(root.right==null){
                        root.right=node;
                        break;
                    }else{
                        root=root.right;
                    }
                }
            }
      }
}
```

