# TIL-20190805/Python: 메타클래스 이해하기

## Python `class`와  `type` 함수

대부분의 언어에서 클래스는 어떻게 객체를 생성할지 정의하는 코드, 하지만 Python에서의 클래스는 **객체**이기도 하다.

`class` 라는 키워드를 사용해서 선언한 클래스는 **객체**가 된다. 따라서 클래스는...

- 변수에 할당할 수 있다
- 복사할 수 있다
- 새로운 속성을 추가할 수 있다
- 함수의 인자로 넘길 수 있다

`type` 함수는 객체가 어떤 타입인지 알 수 있게 해주는 함수.

또 다른 기능은 **클래스를 만드는 데 사용할 수 있다.**

    # object의 타입을 알려준다
    class type(object)
    
    # 새로운 객체를 반환한다.
    class type(name, bases, dict)

`type`으로 메소드나 속성을 정의하기 위해 `dict`를 인자로 전달한다. 상속을 위해서는 `bases` 인자로 클래스를 전달한다.

    class Foo:
    		pass
    
    def greeting(self):
    		return self.bar
    
    FooChild = type('FooChild', (Foo,), {'bar': 'hello', 'greeting': greeting})
    
    obj = FooChild()
    obj.bar
    # 'hello'
    
    obj.greeting()
    # 'hello'

Python에서 클래스는 객체이고, 동적으로 생성할 수 있다. 이것은 `class` 키워드를 사용할 때 Python이 어떻게 작동 하는지를 의미한다. 그리고 이 방법은 metaclass를 사용할 때도 동일하다.

## Metaclass

메타클래스(Metaclasses)는 클래스를 만드는 '무언가'이며, 클래스는 곧 객체이다.

즉, 메타클래스는 객체를 만드는 '무언가'. '클래스'의 '클래스'

`type` 함수는 뒤에서 클래스를 생성하는 메타클래스라고 할 수 있다.

Python의 모든 것은 객체다. 그리고 이 모든 것들은 클래스로부터 생성된다.

    bar = 10
    bar.__class__
    # <class 'int'>
    
    foo = 'jonnung'
    foo.__class__
    # <class 'str'>
    
    def choo(): pass
    choo.__class__
    # <class 'function'>
    
    class Bar: pass
    Bar.__class__
    # <class 'type'>
    
    Bar().__class__
    # <class '__main__.Bar'>

### __metaclass__ 속성

클래스에 `__metaclass__`  속성을 설정하면, 해당 클래스를 생성하기 위해 이 메타클래스를 직적 사용하게 된다. 그리고 `__metaclass__` 에는 클래스는 만드는 '무언가'를 정의하게 된다.

    class Foo:
    		__mataclass__ = something...

Python은 클래스 정의에 `__metaclass__` 가 있는지 찾고, 있는 경우 그 클래스를 만들기 위해 해당 메타클래스를 사용한다. 발견하지 못한 경우 `type`을 사용한다. 그리고 `__metaclass__` 속성은 상속되지 않는다. 

메타클래스를 사용하는 코드는 복잡할 수 있지만, 다음과 같은 일을 할 수 있다.

- 클래스 생성 가로채기
- 클래스 수정하기
- 수정된 클래스 반환하기

## 참고한 내용

[https://tech.ssut.me/understanding-python-metaclasses/](https://tech.ssut.me/understanding-python-metaclasses/)