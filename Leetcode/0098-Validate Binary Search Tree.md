`Middle` 

> Given a binary tree, determine if it is a valid binary search tree (BST).
>
> 给定一个二叉树，判断其是否是一个有效的二叉搜索树。假设一个二叉搜索树具有如下特征：
>
> 节点的左子树只包含小于当前节点的数。
>节点的右子树只包含大于当前节点的数。
> 所有左子树和右子树自身必须也是二叉搜索树。

[TOC]

#### 1. BST的中序列是有序序列

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        if not root:
            return True
        visited = [] # 中序列
        def dfs(root):
            if not root: return
            dfs(root.left)
            visited.append(root.val)
            dfs(root.right)
        
        dfs(root)
        if len(visited) > len(set(visited)):   # 不能含有重复的值
            return False
        return visited == sorted(visited)   # 需要调用排序算法，不太优
```

---

#### 2. 二分法

左子树是BST, 右子树是BST，并且结点的值大于左子树的最小值，同时小于右子树的最大值

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def minOfTree(root):
            if not root: return float('-inf')
            m = root.val
            while root.left:
                if root.left.val < m:
                    m = root.left.val
                root = root.left
            return m

        def maxOfTree(root):
            if not root: return float('inf')
            m = root.val
            while root.right:
                if root.right.val > m:
                    m = root.right.val
                root = root.right
            return m

        if not root or (not root.left and not root.right): 
            return True
        if self.isValidBST(root.left):    # 左子树是否合法
            if root.left and root.val <= maxOfTree(root.left):
                return False
        else:
            return False
        if self.isValidBST(root.right):   # 右子树是否合法
            if root.right and root.val >= minOfTree(root.right):
                return False
        else:
            return False
        return True
```

---

#### 3. 子节点的可取值范围由其父节点确定:+1:

```python
class Solution:
    def isValidBST(self, root):
        def helper(node, lower = float('-inf'), upper = float('inf')):
            if not node: return True
            val = node.val
            if val <= lower or val >= upper:
                return False
            if not helper(node.right, val, upper):  # 父节点的值，父节点的upper
                return False
            if not helper(node.left, lower, val):   # 父节点的lower, 父点的的值 
                return False 
            return True

        return helper(root)
```

