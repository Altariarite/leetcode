```python3
from collections import Counter
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        # two pointers, j is at least k ch ahead of i
        # s[i:j+1] is the substring in the window
        i= 0 
        c = Counter(s[0:k+1])
        
        ans = min(k,len(s))
    
        for j in range(k+1,len(s)):
            c[s[j]] +=1
            if j-i+1 - max(c.values()) > k:# unable to edit
                c[s[i]]-=1
                i+=1   
                # Note we don't need to worry about j
                # as the window should be at least as big as the previous one
                # for ans to increase
            ans = max(ans,j-i+1)
        return ans
```
