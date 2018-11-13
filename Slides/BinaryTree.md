## [Binary Tree](https://en.wikipedia.org/wiki/Binary_tree)

A tree data structure that each node has at most two children.

### Balanced Binary Tree
A binary tree in which the left and right subtrees of **every** node differ in height by 1 or less.

### Complete Binary Tree
A binary tree in which every level, except the last level, is completely filled, and all nodes are as far left as possible.

## [Binary Search Tree](https://en.wikipedia.org/wiki/Binary_search_tree)

For **any** node in a binary tree, **all nodes** in its left subtree is smaller than itself and **all nodes** in its right subtree is larger than itself.

### Basic Operations

- `search()` 
	- worst case time complexity `O(n)`
	- average `O(logn)`
- `insert()`
	- worst case time complexity `O(n)`
	- average `O(logn)`
- `remove()`
	- worst case time complexity `O(n)`
	- average `O(logn)`


### Balanced Binary Search Tree

- All basic operations `search(), insert(), remove()` are guaranteed to be `O(logn)`.
- For example, Red-Black tree. In Java, `TreeMap` and `TreeSet` are implemented in Red-Black tree.


## [Tree Traversal](https://en.wikipedia.org/wiki/Tree_traversal)

For a given tree as following:
```
      7
    /  \
   5    6
 /  \  /  \
 1  2  3  4
```

There are three kinds of traversal:

- Pre-order: 7 5 1 2 6 3 4
- In-order: 1 5 2 7 3 6 4
- Post-order: 1 2 5 3 4 6 7

## Exercises

- [144: Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
- [94: Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- [145: Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- [100: Same Tree](https://leetcode.com/problems/same-tree/)
- [110: Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)
- [173: Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)
- [98: Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
- [700: Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)
- [701: Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)
- [450: Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)
- [105: Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
- [106: Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
- [230: Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
