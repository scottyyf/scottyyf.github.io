# 命令模式 买卖股票

可用于命令行重做和回滚，异步执行

* client： 用户发出的买卖指令
* receiver: 交易系统，有buy和sell等交易的接口
* concreteCommand: command的子类，他将一个receiver实例包含到自己内部，实现对应的买或卖
* command: 定义对应订单接口
* invoker: 中介，实际执行的地方。可将所有的concrete实例都存储下来，做对应的回退等操作

模板

```python
class Command(ABC):
    def __init__(self, recv):
        self.recv = recv

    @abstractmethod
    def excute(self):
        pass


class ConcreteCommand(Command):
    def excute(self):
        self.recv.action()


class Receiver:
    def action(self):
        print('receiver action')


class Invoker:
    def __init__(self, cmd):
        self.cmd = cmd

    def excute(self):
        self.cmd.excute()

cmd = ConcreteCommand(Recevier())
invoker = invoker(cmd)
invoker.excute()
```


证券交易

```python
class Order(ABC):  # Command
    @abstractmethod
    def excute(self):
        pass


class BuyStockOrder(Order):  # concreteCommand
    def __init__(self, receiver):
        self.recv = receiver

    def excute(self):
        self.recv.buy()


class SellStockOrder(Order):
    def __init__(self, receiver):
        self.recv = receiver

    def excute(self):
        self.recv.sell()


class StockTrade:
    def __init__(self):
        pass

    def buy(self):
        print('buy')

    def sell(self):
        print('sell')


class Agent:
    def __init__(self):
        self.order_list = []

    def place_order(self, order):  # order是concreteOrder
        self.order_list.append(order)
        order.excute()


if __name__ == '__main__':
    cmd = BuyStockOrder(StockTrade())
    agent = Agent()
    agent.place_order(cmd)
```
