---
layout: post
title: "recursive problem"
date: 2025-04-22

---
# Begging

# First Module 1 - Arrays, ArrayLists, Recursion

Given this recursive method and an input of n = 7, what will the output be? Please enter your answer as a Comma Separated List (e.g 1, 2, 3, 4)  
```python
public void recursiveMethod(int n) {  
    if (n <= 0) {  
        return;  
    } else {  
        System.out.println(n);  
        recursiveMethod(n - 2);  
        System.out.println(n - 1);  
    }  
}

```

```python
Your Answer:7,5,3,1
```

```python
Correct Answer: 7, 5, 3, 1, 0, 2, 4, 6  
```

The answer relies on a recognition that the output will come before the recursive call, and that the output after all recursive calls are made will output from smallest to largest instead of largest to smallest

# Then a CMU web, Towers of Hanoi

In this puzzle, we have three pegs and several disks, initially stacked from largest to smallest on the left peg. (See the 6-disk picture below.) The rules are simple:

1. Our goal is to move the entire tower to the middle peg.
2. We can only move one disk at a time.
3. We can never place a larger disk on a smaller one.

![](https://www.cs.cmu.edu/~cburch/survey/recurse/disk0.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)  
![](https://www.cs.cmu.edu/~cburch/survey/recurse/disk1.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)  
![](https://www.cs.cmu.edu/~cburch/survey/recurse/disk2.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)  
![](https://www.cs.cmu.edu/~cburch/survey/recurse/disk3.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)  
![](https://www.cs.cmu.edu/~cburch/survey/recurse/disk4.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)  
![](https://www.cs.cmu.edu/~cburch/survey/recurse/disk5.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/empty.gif)  
![](https://www.cs.cmu.edu/~cburch/survey/recurse/basea.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/baseb.gif)![](https://www.cs.cmu.edu/~cburch/survey/recurse/basec.gif)  

If JavaScript 1.2 is enabled on your browser, you can try it yourself. Just click on the disk you want to move, and then click on the peg you want to put it at. Although technically you are only allowed to move one disk at a time, the program will move several disks if it is necessary to complete the move.


We'll answer both of these questions in sequence.

To describe how the monks should solve this puzzle, the concept of recursion will be useful. We look at that next.

Next: [Recursion](https://www.cs.cmu.edu/~cburch/survey/recurse/recursion.html).

# Then a simple leetcode Q [104. Maximum Depth of Binary Tree](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)



[104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) eng ver

But most people did like this, correct, but..., not friendly for me at first

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))        
```

# Then two prob

### Reverse Linked List
https://neetcode.io/problems/reverse-a-linked-list
Not the normal Iteration
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None or head.next is None:
            return head
       	# weird place
        node = self.reverseList(head.next)
        
        head.next.next = head
        head.next = None
        return node
```


And [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) again , simple question again
I think it is a good way to understand?
```python
# Definition for a binary tree node.

# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right


class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:

        # I'm starting from the root node now

        if root is None:  # if there is no root, there is no root node at all, so I should return the value 0

            return 0

        # OK, the logic now is that there is at least one root node. Now, based on the logic of the recursive function,

        # we can know the depth of the left and right nodes starting from the root

        # which is

        left_depth = self.maxDepth(root.left)

        right_depth = self.maxDepth(root.right)

        # OK, now, we start to think, we have the depth of the root nodes root.left and root.right, now we want to add

        # the depth of the root layer itself, so we need to add 1. At the same time, we want the maximum depth, so we have the max function

        return max(left_depth, right_depth) + 1

```


# Right now, the problems are
1. Reinforce point
2. Return type, and helper method (create a new helper method)

# A simple Leetcode Q,
The thinking flow of recursive Q in BST
[617. Merge Two Binary Trees](https://leetcode.cn/problems/merge-two-binary-trees/)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1:
            return root2
        if not root2:
            return root1
        def merge(node1,node2):
            # if two entering roots are None, direct return one of trees, 
            # return node2 # ? wired, wanna change [root1s] val, but it return a value, 

            if node1 is None and node2 is None:
                return 
            
            if node1 and node2:
                node1.val += node2.val
            
            if not node2:
                return 
            if not node1.left and node2.left:
                node1.left = TreeNode(0)
            if not node1.right and node2.right:
                node1.right = TreeNode(0)
            merge(node1.left,node2.left)
            merge(node1.right,node2.right)
            
            
        merge(root1,root2)
        return root1
```


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:

        def merge(root1,root2): # -> treeNode
            if not root1:
                return root2
            if not root2:
                return root1
            # if root1 and root2 # adding value logic
            
            root1.val += root2.val
            root1.left = merge(root1.left,root2.left)
            root1.right = merge(root1.right,root2.right)
            
            return root1
        return merge(root1,root2)
        
```
# Leetcode 450
[450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:

        def dfsFinder(node,val): # Unsure of the return type, changing the tree structure, so should the return type be treeNode?

        # Or do I only need a single return, because I'm only changing the tree structure?  Confused

            # no root , return None
            if node is None:
                return None # Confused here. The question says if found, delete it; if not found, return None or the original?

                # I don't know whether to write return or return None, I can't convince myself.

            
            # if node: ... so right now this place has a node, first one is root
            # from root perspective
            if node.val == val:
                # using successor, that is the minimum value of the right subtree.

                node = successorHelp(node)
                
                # Oh, it can be using if statment here.
                # if node.right and not not node.left ....


            elif node.val > val: # node.left
                temp = dfsFinder(node.left,val)
                return temp #?
            elif node.val < val:
                return dfsFinder(node.right,val)
        
        def successorHelp(node):
            # When calling itself, the input cannot be None, but I think it's okay to check?

			# Wow, it seems that a check is necessary because of the recursive boundary problem, but can we directly check if it's a leaf node? No, what if there's only a left subtree and no right subtree?

            if node is None:
                return None # I suddenly don't know what to return.  Returning None feels strange.

                
                # It was written as None at the end, but after thinking about it, I don't think it will be called.

            # .right once
            node = node.right
            if node.right:
                while node.left:
                    node = node.left
                
                # delete that node
                new_value = node.val
                node = None
                return new_value
            else:
                return node.left
            
            # I think the above can be adjusted.  It's about `val` and an impossible `val`. If it's an impossible `val`, it means there's no right subtree starting from the node, so connect to the left subtree starting from the node, that is, `node = node.left`.

            
            
        
        
```