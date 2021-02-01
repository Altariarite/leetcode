## 1 Naive Recursive Solution
Think of the smallest triangle at the top -> each of the two bottom point has a min_path connected to them, a min_path through the two large triangles with these points as the apex.
```python3
class Solution:
    def minimumTotal(self, tri: List[List[int]]) -> int:
        def min_path(row,i):
            # base case (operator +)
            if row==len(tri) or i==len(tri[row]):
                return 0
            # choose the smaller min path up to the two points below
            # add with current number
            return tri[row][i] + min(min_path(row+1,i),min_path(row+1,i+1))
        return min_path(0,0)
```

## 2 Recursive Solution with Memo
Pretty much the same. But instead of calculating `min_path` every time we first check the memo, and use the memo when we are doing the calculation
```python3
class Solution:
    def minimumTotal(self, tri: List[List[int]]) -> int:
        memo = {}
        def min_path(row,i):
            if row==len(tri) or i==len(tri[row]):
                return 0

            if (row+1,i) not in memo:
                memo[(row+1,i)] = min_path(row+1,i)
            if (row+1,i+1) not in memo:
                memo[(row+1,i+1)] = min_path(row+1,i+1)
            
            return tri[row][i] + min(memo[(row+1,i)],memo[(row+1,i+1)])
        return min_path(0,0)
```
