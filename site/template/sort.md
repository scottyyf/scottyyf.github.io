# 时间复杂度

O(n^2)

### 选择排序
从头到尾，找到最小的那个值，并将这个值和当前头进行交换。重复该操作n次即可
```python
def select_sort(s: list):
    for left in range(len(s)-1):
        min_index= left
        for right in range(left+1, len(s)): # 从已排好序的下一个开始
            if s[right] < s[min_index]: # 找到最小index
                min_index = right

        s[min_index], s[left] = s[left], s[min_index]

    return s
```


### 插入排序
将已排好序的部分和之后的一个值进行比较，如果这个值比排好序的最后一个小，那么需要将这个值插入到已排好序的合适位置
```python
def insert_sort(s: list) -> list:
    for outer in range(1, len(s)): # 从1 开始
        pre_index = outer - 1
        current = s[outer]
        while pre_index >= 0 and current < s[pre_index]: # 将outer对应的值插入已排好序的列表中
            s[pre_index], s[pre_index + 1] = s[pre_index + 1], s[pre_index]
            pre_index -= 1

    return s
```


### 冒泡排序
将当前位置和下一个位置的值进行比较，把较大值放到右侧，同时从这里的右侧位置进行往下一位进行比较。知道最后一个位置，这样就完成了一遍冒泡
后续重复该动作，完成n遍冒泡

```python
def bubble_sort(s: list) -> list:
    for left in range(len(s)):
        for right in range(0, len(s) - 1 - left):
            if s[right] > s[right+1]:
                s[right], s[right+1] = s[right+1], s[right]

    return s
```


# 时间复杂度
O(nlogn)

### 快速排序

通过pivot将列表分成左边小于pivot，右边大于pivot，然后递归调用这个逻辑。完成排序

> **_NOTE:_** 以行首为标杆，将大小分为右左两边。这样一直执行，当只有两个元素的时候，开始有序，并在归的时候慢慢向上有序操作

```python
class QuickSort:
    def sort(self, nums: list) -> list:
        self.quick_sort(nums, 0, len(nums)-1) # 0 to n-1
        return nums

    def quick_sort(self, nums, begin, end): # end 这里是正确的index
        if begin >= end:
            return

        pivot = self.partition(nums, begin, end)
        self.quick_sort(nums, begin, pivot-1)
        self.quick_sort(nums, pivot+1, end)

    def partition(self, nums, begin, end) -> int:
        pivot = nums[begin]
        mark = begin
        for i in range(begin+1, end+1): # i需要到end这个数，所以range中需要end+1
            if nums[i] < pivot:
                mark += 1
                nums[mark], nums[i] = nums[i], nums[mark]

        nums[begin], nums[mark] = nums[mark], nums[begin]
        return mark
```

### 归并排序

> **_NOTE:_** 先一分为二，这样一直分，一直分，分到只有两个值的时候，开始合并，这个合并操作会一直向上重复刚刚一分为二的路径

```python
class MergeSort:
    def merge(self, nums:list):
        self.merge_sort(nums, 0, len(nums)-1)
        return nums

    def merge_sort(self, nums: list, left: int, right: int):
        mid = (left + right) >> 1
        self.merge_sort(nums, left, mid)
        self.merge_sort(nums, mid+1, right)
        self.merge(nums, left, mid, right)

    def merge(self, nums, left, mid, right):
        temp = []
        i = left
        j = mid + 1

        while i <= mid and j <= right:
            if nums[i] < nums[j]:
                temp.append(nums[i])
                i += 1
            else:
                temp.append(nums[j])
                j += 1

        while i <= mid:
            temp.append(nums[i])
            i += 1

        while j <= right:
            temp.append(nums[j])
            j += 1

        nums[left: right+1] = temp
```

### 堆排序

这里先用heapq自带的小顶堆
```python
class HeadqSort:
    def sort(self, nums: list) -> list:
        headq.heapify(nums)
        
        temp = []
        length = len(nums)
        for i in range(length):
            temp.append(headq.heappop(nums)

        return temp
```


# 特殊排序
O(n)


