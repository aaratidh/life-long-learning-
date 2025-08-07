```python
# depth first search Trees
# Inorder Traversal
# preorder Traversal
# post order Trversal
class Tree:
    def __init__(self , val , right=None , left = None):
        self.val = val
        self.right = right
        self.left = left
    def inorder( node):
        if node == None:
            return
        else:
            if self.left:
                inorder( node.left)
            print(root.val)
            if self.right:
                inorder(node.right)
    def preorder( node):
        if node == None:
            return
        else:
            print(root.val)
            if self.left:
                preorder( node.left)
            if self.right:
                preorder(node.right)
    def postorder( node):
        if node == None:
            return
        else:
            if self.left:
                postorder( node.left)
            if self.right:
                postorder(node.right)
        print(root.val)
```
```python
from typing import List

class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        triangle = []

        for i in range(numRows):
            # Start each row with 1
            row = [1] * (i + 1)
            
            # Fill in the middle elements
            for j in range(1, i):
                row[j] = triangle[i-1][j-1] + triangle[i-1][j]
            
            triangle.append(row)

        return triangle
```
