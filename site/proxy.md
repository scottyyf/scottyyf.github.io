# 代理模式 买东西用信用卡支付

代理模式包含3个类

* Subject类： 是proxy和realsubject的公共借口
* RealSubject类： subject的子类，提供真正的功能，由proxy实例并调用
* proxy类： subject的子类。负责处理客户端请求，实例化和调用realSubject

信用卡就是一个代理，对应实际的银行账户

```python
class Client:
    def __init__(self):
        print('用信用卡买一件衣服')
        self.debitcard = DebitCard()
    
    def buy(self):
        self.debitcard.do_pay()


class Payment(ABC):  # subject
    @abstractmethod
    def do_pay(self):
        pass


class Bank(Payment):  # realsubject
    def __init__(self):
        self.id = None
    
    def do_pay(self):
        print('Bank: paying the merchant')


class DebitCard(Payment):  # proxy
    def __init__(self):
        self.bank = Bank()

    def do_pay(self):
        self.bank.do_pay()
       

if __name__ == '__main__':
    Client().buy()
```
