# Matrix Spiral Copy

## Problem Statement

Given a 2D array (`inputMatrix`) of integers, create a function `spiralCopy` that copies the matrix’s values into a 1D array in a **clockwise spiral order**. The function should return the resulting array.

---

## Example

**Input:**
```python
inputMatrix = [
    [1,   2,   3,  4,  5],
    [6,   7,   8,  9, 10],
    [11, 12, 13, 14, 15],
    [16, 17, 18, 19, 20]
]



````markdown


## Code

```python
from typing import List

def spiral_copy(inputMatrix: List[List[int]]) -> List[int]:
    row = len(inputMatrix) - 1
    col = len(inputMatrix[0]) - 1

    top = 0 
    bot = row
    left = 0 
    right = col 

    output = []

    while top <= bot and left <= right:
        # Traverse from left to right along the top row
        for i in range(left, right + 1): 
            output.append(inputMatrix[top][i])
        top += 1
        
        # Traverse from top to bottom along the right column
        for i in range(top, bot + 1):
            output.append(inputMatrix[i][right])
        right -= 1     
        
        # Traverse from right to left along the bottom row
        if top <= bot: 
            for i in range(right, left - 1, -1):
                output.append(inputMatrix[bot][i])
            bot -= 1

        # Traverse from bottom to top along the left column
        if left <= right:
            for i in range(bot, top - 1, -1):
                output.append(inputMatrix[i][left])
            left += 1

    return output
````

---

## Example Usage

```python
# Sample input
inputMatrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Function call
print(spiral_copy(inputMatrix))
```

**Output:**

```
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```










