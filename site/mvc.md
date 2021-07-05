# MVC

* model: 数据的处理逻辑
* view: 数据的展示
* controller: 两者之间的粘合剂，传递者

```python
class Model:
    Services = {
        'email': {'number': 1000, 'price': 12},
        'sms': {'number': 1000, 'price': 10},
        'voice': {'number': 1000, 'price': 15},
        }


class View:
    def list_services(self, services):
        print(', '.join([service for service in services.keys()]))

    def list_prices(self, services):
        print(', '.join([str(value['price']) for value in services.values()]))


class Controller:
    def __init__(self):
        self.modoel = Model()
        self.views = View()

    def get_services(self):
        return self.views.list_services(self.modoel.Services)

    def get_prices(self):
        return self.views.list_prices(self.modoel.Services)


class Client:
    def main(self):
        c = Controller()
        c.get_services()
        c.get_prices()


if __name__ == '__main__':
    Client().main()
```
