### 门面模式 婚礼筹备

如何理解门面模式： 去商店买东西，只需要告诉店员你需要什么，店员就会把对应东西给你

* 门面模式为子系统中的一组接口提供一个统一的接口(店员)
* 实现与多个客户端的解耦

```python
class EventManager:
    def __init__(self):
        print('talk to the event manager...\n')

    def manage(self):
        self.hotelier = Hotelier()
        self.hotelier.book_hotel()

        self.florist = Florist()
        self.florist.set_flower()

        self.caterer = Caterer()
        self.caterer.set_cuisine()


class You:
    def __init__(self):
    
    def book(self):
        em = EventManager()
        em.manage()


class Caterer:
    def __init__(self):

    def set_cuisine(self):


class Florist:
    def __init__(self):
    
    def set_flower():

class Hotelier:
    def __init__(self):
        
    def book_hotel(self):


if __name__ == '__main__':
    you = You()
    you.book()
```
