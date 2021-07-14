# 有效的括号

* 当解决最近相关性的问题时，使用栈解决 （洋葱一样的题）
* 当解决先来后到的问题时，用队列
* 用栈实现队列，用队列实现栈，那么就用两个栈或两个队列实现对应的队列或栈

暴力方法：替换队列中符合要求的括号对

栈方法：如果是左括号，那么加入栈，如果是右括号，那么就和栈顶元素比较并进行抵消

```python
class Solution:
    def isValid(self, s: str) ->bool :
        kh_dict = {'[': ']', '(': ')', '{': '}'}
        stack = ['pre']
        for data in s:
            if data in kh_dict:
                stack.append(data)
            elif kh_dict.get(stack.pop()) != data:
                return False

        return stack == ['pre']
```
