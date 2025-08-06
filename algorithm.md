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
