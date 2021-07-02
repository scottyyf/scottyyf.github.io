1. 通过\_\_new方法实现单列。new方法是在init方法前被自动调用
```python
class SingleTon:
    _instance = None
    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super().__new__(cls, *args, **kwargs)

        return cls._instance
```

2. 元类。元类是类的类，如type(int)返回的是type，这说明type是元类。实际上是通过int = type(name, base, dict)来实现类的初始化
。这里可通过控制元类实现单例化。一般由元类来覆盖init和new
```python
class MyInt(type):
    _instance = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instance:
            cls._instance[cls] = super().__call__(*args, **kwargs)

        return cls._instance[cls]


class Int(metaclass=MyInt):
    def connect(self):
        print(f'Int id {self}')


a = Int().connect()  ## Int()实例化将调用MyInt的__call__函数
```

3. 可在类定义的地方，直接实例化。其他地方调用时，直接使用这个实例化的对象、
```python
class SingleTon:
    pass

single_ton = SingleTon()
```
