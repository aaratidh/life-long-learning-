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
   def generate(self, numRows: int) -> List[List[int]]:
        list1 = [] 
        array: List[List[int]] = []
        for i in range(numRows):
            # make the row
            array.append([0] * (i + 1))
            for j in range(i + 1):
                if j == 0 or j == i:                 # edges are 1
                    array[i][j] = 1
                else:                                 # middle = sum of two above
                    array[i][j] = array[i-1][j-1] + array[i-1][j]
        return array
                
```


# Note: The trick here is that array.append([0] * (i + 1))   this does as a list multiplication:
# Note: "The trick here is that moving row number i after completing j all posssible ranges "

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
