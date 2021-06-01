# [三数之和](https://leetcode-cn.com/problems/3sum/)

悟： 这道题的target可以传入指定，也可以不一定是求和。非常的可扩展

要求： 和两数之和类似

附： 那么四数之和，五数之和，n数之和怎么求？

解法：

暴力法：时间复杂度O(n^3)。由于这里是返回值，不是下标，且不允许有重复值，所以前面先sort并在后面进行了continue的操作
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        ret = []
        nums.sort()
        for left in range(len(nums) - 2):
            for mid in range(left + 1, len(nums) - 1):
                for right in range(mid + 1, len(nums)):
                    if nums[left] + nums[mid] + nums[right] == 0:
                        if [nums[left], nums[mid], nums[right]] in ret:
                            continue

                        ret.append([nums[left], nums[mid], nums[right]])

        return ret
```

两重循环加hash map，hashmap中存储第三个值
```python
TODO
```

双指针法：快慢指针，左右两边，以及快指针先走k步的多种情况。
枚举k， 然后i,j进行双指针操作
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        ret = []
        if len(nums) < 3:
            return ret

        nums.sort()
        for pivot in range(len(nums) - 2):
            if nums[pivot] > 0:
                break

            if pivot > 0 and nums[pivot] == nums[pivot - 1]:
                continue

            left, right = pivot + 1, len(nums) - 1
            while left < right:
                to_sum = nums[pivot] + nums[left] + nums[right]
                if to_sum > 0:
                    right -= 1

                elif to_sum < 0:
                    left += 1

                else:
                    ret.append([nums[pivot], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1

                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1

                    left, right = left + 1, right - 1

        return ret
```
