# 观察者模式 新闻发布

* subject: 新闻发布者newpublisher，他包括新增，删除观察者方法，以及发布消息，增加消息接口
* SmsSubscriber和EmailSubscriber是两个观察者，提供一个被subject发布消息时调用的接口

```python
class NewPublisher:
    def __init__(self):
        self._subscriber = set()
        self._last_news = None

    def attach(self, subscriber):
        self._subscriber.add(subscriber)

    def detach(self, subscriber):
        self._subscriber.discard(subsciber)

    def notify_all(self):
        for sub in self._subscriber:
            sub.notify()

    def add_news(self, news):
        self._last_news = news

    @property
    def last_news(self):
        reutrn self._last_news


class Subscriber(ABC):
    @abstractmethod
    def notify(self):
        pass


class EmsSubscriber(Subscriber):
    def __init__(self, publisher):
        self.publisher = publisher
        self.publisher.attach(self)

    def notify(self):
        print(f'{type(self)} {self.publisher.last_news}')


class EmalSubscriber(Subscriber):
    def __init__(self, publisher):
        self.publisher = publisher
        self.publisher.attach(self)

    def notify(self):
        print(f'{type(self)} {self.publisher.last_news}')


if __name__ == '__main__':
    publisher = NewPublisher()
    for sub in [EmsSubscriber, EmalSubscriber]:
        sub(publisher)

    publisher.notify_all()
```
