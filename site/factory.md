## 简单工厂模式 动物叫

定义：允许接口创建对象，但不会暴露对象的创建逻辑

factory类是一个带有make_sound方法的工厂，根据客户端传递的参数类型，就可以创建出对应的Animal实例

```python
from abc import ABC, abstractmethod


class Animal(ABC):
    @abstractmethod
    def do_say(self):
        pass


class Dog(Animal):
    def do_say(self):
        print('Bhow Bhow!!')


class Cat(Animal):
    def do_say(self):
        print('Meow Meow!!')


class Factory:
    def make_sound(self, object_type):
        return eval(object_type)().do_say()

 
if __name__ == '__main__':
    ff = Factory()
    animal = input('input an animal type, Dog or Cat...')
    ff.make_sound(animal)
```


## 工厂方法模式 脸书、领英上跟人简介

```
product                     creator
  |                             |
  |                             |
  |                             |
concrete_product ------- concrete_creator
```

* creator, product 是抽象类
* concrete_product, concrete_creator是对应的子类
* concrete_creator经过对应的传入参数后，会调用方法创建对应的product实例

实现一个facebook, linkedin上个人简介。简介中都包含个人信息，另外，linkedin中还包含个人专利等；facebook包含相册等

```python
from abc import ABC, abstractmethod
class Section(ABC):
    @abstractmethod
    def describe(self):
        pass


class PersonalSection(Section):
    def describe(self):
        print('Personal Section')


class AlbumSection(Section):
    def describe(self):
        print('Album Section')


class PatentSection(Section):
    def describe(self):
        print('Patent Section')


class PublicationSection(Section):
    def describe(self):
        print('Publication Section')


class Profile(ABC):
    def __init__(self):
        self.sections = []
        self.create_profile()

    @abstractmethod
    def create_profile(self):
        pass

    def add_section(self, section):
        self.sections.append(section)


class Linkedin(Profile):
    def create_profile(self):
        self.add_section(PersonalSeciton())
        self.add_section(PatentSection())
        self.add_section(PublicationSection())


class FaceBook(Profile):
    def create_profile(self):
        self.add_section(PersonalSection())
        self.add_section(AlbumSection())


if __name__ == '__main__':
    ff = input('your input, facebook or linkedin?')
    profile = eval(ff)()
```


## 抽象工厂模式 pizza商店供货

一个接口创建一系列对象

一个pizza店，有美式和印式两种，每种又有蔬菜和肉两类，分别是美式（Mexican,Ham）印式(Delux,Chicken)。现在来了一个顾客要了肉类的所有pizza

```
factory(creator)---us_factory --- concrete_product1 --- product1
|                    |
|                    |
|               concrete_product2 -- product2
|
india_factory ....
```

```python
class PizzaFactory(ABC):
    @abstractmethod
    def create_veg_pizza(self):
        pass

    @abstractmethod
    def create_non_veg_pizza(self):
        pass


class UsPizzaFactory(PizzaFactory):
    def create_veg_pizza(self):
        return MexicanPizza()

    def create_non_veg_pizza(self):
        reutrn HamPizza()


class IndiaFactory(PizzaFactory):
    def create_veg_pizza(self):
        return DeluxPizza()

    def create_non_veg_pizza(self):
        return ChickenPizza()


class VegPizza(ABC):
    @abstractmethod
    def prepare(self):
        pass


class NonVegPizza(ABC):
    @abstractmethod
    def serve(self, veg_pizza):
        pass


class MexicanPizza(VegPizza):
    def prepare(self):
        print(f'prepare {type(self).__name__}')


class HamPizza(NonVegPizza):
    def serve(self, veg_pizza):
        print(f'{type(self).__name__} served with {type(veg_pizza).__name__} on')


class DeluxPizza(Vegpizza):
    def prepare(self):
        print(f'prepare {type(self).__name__}')


class ChickenPizza(NonVegPizza):
    def serve(self, veg_pizza):
        print(f'{type(self).__name__} served with {type(veg_pizza).__name__} on')


class PizzaStore:
    def make_pizza(self):
        for factory in [UsFactory(), IndiaFactory()]:
            veg = fatory.create_veg_pizza()
            non_veg = factory.create_non_veg_pizza()
            non_veg.prepare()
            veg.serve(non_veg)
```
