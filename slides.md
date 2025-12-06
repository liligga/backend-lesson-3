---
theme: seriph
background: https://cover.sli.dev
title: Урок 3 Python backend
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Добро пожаловать

---

### Принципы ООП

1. Наследование
2. Полиморфизм
3. Инкапсуляция
4. Абстракция

---

### Инкапсуляция в Python

**Инкапсуляция** — это механизм, который объединяет данные (атрибуты) и методы, работающие с этими данными, в единый объект и скрывает детали реализации от пользователя.

В Python инкапсуляция достигается с помощью соглашения об именовании. Атрибуты, которые не предназначены для прямого доступа извне, именуются с одним или двумя подчеркиваниями в начале.

- `_одно_подчеркивание`: атрибут считается **защищенным** (protected) и не должен изменяться вне класса.
- `__два_подчеркивания`: атрибут считается **приватным** (private), и его имя искажается, чтобы избежать случайного переопределения в дочерних классах.

---

### Инкапсуляция в Python

> Доступ к <span v-mark.highlight.green>защищенным и приватным</span> атрибутам **внутри** класса возможен.

> Доступ к <span v-mark.highlight.orange>защищенным</span> атрибутам извне возможен, но не рекомендуется.

> Доступ к <span v-mark.highlight.red>приватным</span> атрибутам **извне** класса возможен при помощи искажения имени. Но тоже не рекомендуется.


```python
class Car:
    def __init__(self):
        self.__speed = 60

car = Car()
car.__speed = 10 # будет ошибка
print(car.__speed) # будет ошибка
print(car._Car__speed)  # будет 60, так делают в крайнем случае
```

> Это называется искажением имени (name mangling).

---
layout: two-cols
---

### Инкапсуляция в Python

Для нормального доступа к приватным атрибутам используются методы (getter и setter) или `@property`

`@property` - это декоратор, который позволяет сделать метод доступным как атрибут

Инкапсуляция полезна для защиты данных от неправильного доступа и изменения, а также для проверок данных

::right::

```python
class Car:
    def __init__(self, max_speed):
        self.max_speed = max_speed
        self.__speed = 0  # Приватный атрибут

    def accelerate(self, acc):
        # setter
        if self.__speed + acc > self.max_speed:
            raise ValueError("Скорость не может быть больше максимальной")
        else:
            self.__speed += acc

    def get_speed(self):
        # getter
        return self.__speed

```

При попытке присвоить неправильное значение выше будет выброшено исключение(`ValueError`)

---

### Инкапсуляция в Python

Пример с `@property`:

```python
class Car:
    def __init__(self, max_speed):
        self.max_speed = max_speed
        self.__speed = 0  # Приватный атрибут

    @property
    def speed(self):
        # getter
        return self.__speed

    @speed.setter
    def speed(self, value):
        # setter
        if value > self.max_speed:
            raise ValueError("Скорость не может быть больше максимальной")
        else:
            self.__speed = value
```

При попытке присвоить неправильное значение выше будет выброшено исключение(`ValueError`)

---
layout: two-cols
---

### Абстракция в Python

**Абстракция** — это принцип, который позволяет скрывать сложные детали реализации, предоставляя пользователю только необходимый функционал. Она помогает сосредоточиться на том, ***что*** объект делает, а не на том, ***как*** он это делает.

В Python абстракция осуществляется с помощью абстрактных классов и методов из модуля `abc` (Abstract Base Classes).

<v-clicks>

- **Абстрактный класс** не может иметь экземпляров и служит шаблоном для других классов.

- **Абстрактный метод** объявляется, но не реализуется в абстрактном классе. Дочерние классы обязаны его реализовать.

</v-clicks>

::right::

<v-click>

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        # Реализация абстрактного метода
        print("Собака лает")

class Cat(Animal):
    def make_sound(self):
        # Реализация абстрактного метода
        print("Кошка мяукает")

dog = Dog()
cat = Cat()

dog.make_sound()
cat.make_sound()
```

</v-click>

---

### Абстракция в Python

> В примере выше Animal - это абстрактный класс, его нельзя ининциализировать.

<br>

> Dog и Cat - это дочерние классы, которые наследуются от Animal, они называются конкретными классами.

<br>

> Каждый конкретный класс обязан переопределить абстрактный метод make_sound. Это называется реализацией абстрактного метода. То есть конкретные классы реализуют методы абстрактного класса.

---
layout: two-cols-header
---

### Общее

Все принципы ООП помогают сделать код более понятным и поддерживаемым.
Также есть более сложные принципы дизайна программного обеспечения - принципы SOLID.
Также есть паттерны программирования, связанные с ООП, которые помогают решать определенные задачи.

Полезные ссылки:

::left::

- [Принципы SOLID](https://solidbook.vercel.app/)
- [Про SOLID с примерами](https://habr.com/ru/companies/otus/articles/651753/)
- [Паттерны программирования](https://refactoring.guru/ru/design-patterns/catalog)
- [Паттерны с примерами](https://habr.com/ru/articles/930094/)

Штуки со знаком @ - это декораторы. Они используются для добавления дополнительной функциональности к функции или классу.

::right::

Более продвинутые статья про атрибуты в Python:
- [Статья #1](https://habr.com/ru/companies/otus/articles/896190/)
- [Статья #2](https://habr.com/ru/companies/otus/articles/889754/)
- [Статья #3](https://habr.com/ru/companies/otus/articles/801595/)
- [Статья #4](https://konstantinklepikov.github.io/myknowlegebase/notes/python-descriptors.html)

Про протоколы в Python:
- [Статья #1](https://habr.com/ru/companies/wunderfund/articles/751424/)

---

<Questions />