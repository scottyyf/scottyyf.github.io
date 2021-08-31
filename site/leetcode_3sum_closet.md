# 最接近的三数之和

和求3数之和类似

```python
class Solution:
    def test(self, nums, target):
        nums.sort()
        result = nums[0] + nums[1] + nums[2]
        for pivot in range(len(nums)-2):
            left, right = pivot+1, len(nums)-1
            while left < right:
                total = nums[pivot] + nums[left] + nums[right]
                if total == target:
                    return total

                if abs(total - target) < (result - target):
                    result = total

                if total < target:
                    left +=1
                else:
                    right -= 1

        return result
```
