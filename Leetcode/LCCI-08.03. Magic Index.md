`Easy`

> 魔术索引。 在数组A[0...n-1]中，有所谓的魔术索引，满足条件A[i] = i。给定一个有序整数数组，编写一种方法找出魔术索引，若有的话，在数组A中找出一个魔术索引，如果没有，则返回-1。若有多个魔术索引，返回索引值最小的一个。
>
> **说明:**
>
> 1. nums长度在[1, 1000000]之间
> 2. 此题为原书中的 Follow-up，即数组中**可能包含重复元素**的版本

#### 1. 暴力

```python
class Solution:
    def findMagicIndex(self, nums: List[int]) -> int:
        for i in range(len(nums)):
            if i == nums[i]:
                return i
        return -1
```

- 时间复杂度： $O(n)$
- 空间复杂度：$O(1)$

---

#### 2. 二分剪枝(有序前提下)

```python

```

时间复杂度： $O(\log n)$