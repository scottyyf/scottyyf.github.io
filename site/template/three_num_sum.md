下面是3数之和，如果是4数之和，5数之和，那么直接在外面加对应的for循环

```python
class Solution:
    def threeSum(self, nums: list) -> List[List[int]]:
        ret = []
        if len(nums) < 3:
            return ret

        nums.sort()
        for pivot in range(len(nums) - 2):
            if nums[pivot] > 0:
                break

            # 相同数字已经计算过了
            if pivot > 0 and nums[pivot] == nums[pivot - 1]:
                continue

            left, right = pivot + 1, len(nums) - 1  # 赋初始值出过错
            while left < right:
                _sum = nums[pivot] + nums[left] + nums[right]
                if _sum > 0:
                    right -= 1

                elif _sum < 0:
                    left += 1

                else:
                    ret.append((nums[pivot], nums[left], nums[right]))
                    while left < right and nums[left] == nums[left + 1]:  # 这个地方错了很多次了
                        left += 1

                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1

                    left += 1
                    right -= 1

        return ret
```
