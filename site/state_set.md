# 状态设计模式

收音机有AM、FM两个模式，还有一个自动搜索按钮。切换到对应AM或FM再自动搜索，这个可用状态设计模式

* state: 封装对象的父类借口
* concreteState: state的子类，包含具体状态的处理逻辑方法
* context: 接受客户端请求，并维护一个state的实例，包含客户调用接口

模板：

```python
class State(ABC):
    @abstractmethod
    def handle(self):  # 搜索台的功能
        pass


class ConcreteStateA(State):
    def handle(self):
        print('this is a')


class ConcreteStateB(State):
    def handle(self):
        print('this is b')


class Context:
    def __init__(self):
        self.state = None

    def set_state(self, state):
        self.state = state

    def get_state(self):
        return self.state

    def handle(self):
        self.state.handle()


c = Context()
state = ConcreteStateA()
c.set_state(state)
c.handle()
```


电脑的开机，关机，挂起和休眠

```python
class ComputerState(ABC):
    name = ''
    allowed = []

    def switch(self, state):
        if state.name not in self.allowed:
            print('not allowed')
        else:
            print(f'set state to {state.name}')
            self.__class__ = state


class On(ComputerState):
    name = 'on'
    allowed = ['off', 'suspend']


class Off(ComputerState):
    name = 'off'
    allowed = ['on']


class Suspend(ComputerState):
    name = 'suspend'
    allowed = ['on', 'off']


class Computer:
    def __init__(self):
        self.state = Off()

    def change(self, state):
        self.state.switch(state)

cmpt = Computer()
cmpt.change(On)
cmpt.change(Suspend)
```
