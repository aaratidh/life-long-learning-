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

## Q2 

```python
Q 2 from typing import List

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


The trick here is that array.append([0] * (i + 1))   this does as a list multiplication:

Create a new list of length (i + 1) filled with zeros, and append it as a new row in array."

Step-by-step:
[0] → a list with a single element 0.

[0] * (i + 1) → list multiplication in Python.
This repeats [0] i + 1 times.
Example:

If i = 0 → [0] * (1) → [0]

If i = 1 → [0] * (2) → [0, 0]

If i = 2 → [0] * (3) → [0, 0, 0]

array.append(...) → adds this list as the next row in the Pascal’s triangle structure.

and hence:  this   **array[i][j] = array[i-1][j-1] + array[i-1][j]**  create each non-boundary elements: 
