# 模板方法模式

多个相同或类似的逻辑在一起需要实现的时候，定义好一个模板，包括执行顺序等。子类实现对应的具体操作，达到少代码

模板： 

```python
class AbstractClass(ABC):
    @abstractmethod
    def operation1(self):
        pass

    @abstractmethod
    def oparation2(self):
        pass

    def template_method(self):
        self.operation1()
        self.operation2()

 
class ConcreteClass(AbstractClass):
    def operation1(self):
        print('operation1')

    def operation2(self):
        print('operation2')


class client:
    def main(self):
        ConcreteClass().template_method()


client().main()
```


旅行社：旅行社定义了一共几天的行程，用户定义每天做什么

```python
class Trip(ABC):
    @abstractmethod
    def set_transport(self):  # 设置交通工具
        pass

    @abstractmethod
    def day1(self):
        pass

    @abstractmethod
    def day2(self):
        pass

    @abstractmethod
    def return_home(self):
        pass

    def itinerary(self):
        self.set_transport()
        self.day1()
        self.day2()
        self.return_home()

 
class VeniceTrip(Trip):
    def set_transport(self):
        # buy airport

    def day1(self):
        # 吃

    def day2(self):
        # 喝

    def return_home(self):
        # 睡

 
class MaldivesTrip(Trip):
    ...


class Client:
    def arrange_trip(self):
        VeniceTrip().itinerary()
        MaldivesTrip().itinerary()


Client().arrange_trip()
```
