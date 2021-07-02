## 简单工厂模式

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


## 工厂方法模式

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
