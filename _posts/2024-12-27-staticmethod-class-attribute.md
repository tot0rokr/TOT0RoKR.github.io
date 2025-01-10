---
title: "How to create class attribute in staticmethod in Python"
last_modified_at: 2025-01-10T00:00:00-09:00
categories:
- Python
tags:
- class
excerpt: "Python에서 __init_subclass__ 매직 메소드를 사용해 staticmethod에서 class attribute를 정의하고 접근하는 방법에 대해 기술한다."
---

## 그런 일이 왜 필요한가?

Base class를 상속받는 클래스에서 메소드가 정의 될 때, class attribute에 해당 메소드를 추가하여
Base class에서 특정 Key값을 이용하여 해당 메소드를 호출하는 방법을 사용하고 싶었다. 그러니까, 자식
클래스의 구현체 모르면서 메소드는 호출하고 싶은 상황이었다.

이런 디자인 자체가 부모클래스에서 자식클래스에 의존성을 갖게되는 문제가 있다고 생각이 들 수도
있지만, 특정 메소드를 지정해서 호출하는 것이 아니고, class method에서 class attribute에 등록된
메소드를 호출하므로
의존성 관계 자체를 맺는 구조는 아니다. 게다가, 자식 클래스와 그의 메소드가 무한히 확장 가능하면서도
Base class에서 호출되어야 하므로 이러한 구조가 필요했다.

이를 해결하기 위해, Base class의 staticmethod를 decorator로 자식 클래스의 메소드를 정의하는 방법을
사용한다. Base class의 staticmethod에서는 자식 클래스의 attribute를 할당한다. 하지만 일반적인
방법으로는 접근 자체가 불가능하다. 어떻게 해결했는지 알아보자.

## 문제점

### 부모 클래스의 staticmethod에서 자식 클래스의 attribute를 접근하는 것은 원칙적으로 불가능

애초에 명시적인 지정을 하지 않으면 접근할 방법이 없다. 만약 평범하게 class attribute로 접근하면
아래와 같은 방법이 최선이다. 하지만 이렇게 접근하면 어떠한 클래스의 메소드인지 알 방법이 없고, 모든
클래스가 모든 메소드를 공유하게 된다는 설계상의 문제가 있다.

```python
class Base:
    _method = None

    @staticmethod
    def register(method):
        Base._method = method
        return method

    def method(self):
        self._method()

class Child(Base):
    # _method = None 이렇게 할 수 없다. self._method가 None이 되기 때문

    @Base.register
    def hello(self):
        print("Hello")

print(Base._method) # <function Child.hello at 0x7f4c7fbb7d00>
print(Child._method)  # <function Child.hello at 0x7f4c7fbb7d00>
Child().method() # Hello
```

### staticmethod 대신 classmethod를 사용하면?

부모 클래스의 class method를 호출하는데, 자식 클래스의 class attribute에 접근할 수 있를 턱이 없다.
결국 staticmethod로 구현한 위의 사례와 동일한 문제가 발생한다.

```python
class Base:
    _method = None

    @classmethod
    def register(cls, method):
        cls._method = method
        return method

    def method(self):
        self._method()

class Child(Base):
    # _method = None 역시 이렇게 할 수 없다. self._method가 None이 되기 때문

    @Base.register
    def hello(self):
        print("Hello")

print(Base._method) # <function Child.hello at 0x7f4c7fbb7d00>
print(Child._method)  # <function Child.hello at 0x7f4c7fbb7d00>
Child().method() # Hello
```

## 해결책

### `__init_subclass__` 매직 메소드와 method attribute를 사용

그렇다면 이 문제를 어떻게 해결할 수 있을까? 결론은 staticmethod에서 일종의 flag를 사용해 lazy 처리를
통해 이 문제를 해결할 수 있다.

```python
class Base:
    _method = None

    def __init_subclass__(cls, **kwargs):
        super().__init_subclass__(**kwargs)

        for _, method in cls.__dict__.copy().items():
            if hasattr(method, "_flag"):
                cls._method = method
                delattr(method, "_flag")

    @staticmethod
    def register(method):
        method._flag = True
        return method

    def method(self):
        self._method()

class Child(Base):
    @Base.register
    def hello(self):
        print("Hello")

print(Base._method) # None
print(Child._method) # <function Child.hello at 0x7f8b1c1b7d30>
Child().method() # Hello
```

method에 attribute를 추가한다는 점이 마음에 들지는 않지만, 이렇게 하면, Base와 Child가 모두 정의된
이후에 할당하여 요구사항을 모두 만족할 수 있다.
