# Day 37

## 738. Monotone Increasing Digits

[link](https://leetcode.com/problems/monotone-increasing-digits/description/)

```python
class Solution:
    def monotoneIncreasingDigits(self, n: int) -> int:
        # 从前向后遍历不可以，比如10不好处理
        # 从后向前遍历，若str[i]<str[i-1]，则str[i-1]-=1，str[i]=9（10会报错）
        # str[i]=9修改为从i位到之后均为9
        nums = list(str(n))
        for i in range(len(nums)-1,0,-1):
            if int(nums[i])<int(nums[i-1]):
                nums[i:] = '9'*(len(nums)-i)
                nums[i-1] = str(int(nums[i-1])-1)
        return int("".join(nums))
```
