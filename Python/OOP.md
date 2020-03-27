# OOP

> 객체 지향 프로그래밍  ( **O**bject **O**riented **P**rogramming )



### 기본적으로 기억해야 할 것

An `Object` has two characteristic.

​	1) `attributes` 

​	2) `behavior` ( =method)

```
if an Object == red panda :
attributes = [ age, name, gender, ... ]
behavior = [ eating, dancing, hunting, ... ]
```



### 용어 정리

* class 

  * it's a blueprint for the object. 
  * 같은 종류의 집단에 속하는 속성과 행위를 정의한 것
  * we use `class` keyword to define an empty class. 

* object(or instance)
  
  * An individual object of a certain class.
* 보통 객체만 지칭할 땐 object 라고 부르고, 클래스와 연관지어 말할 땐 instance 라 부른다.
  
* attribute

  * data

* method

  * behavior
  * A special kind of function that is defined in a class definition.



예시 1)

 `vehicle` 이라는 `class` 안에는 `car`, `bus`, `plane` 등등의 `instance` 가 있다.  그리고 `vehicle` 은 바퀴 개수, 브랜드, 수용 인원 과 같은 `attribute`를 가지고 있고, 가속하고 감속하고 멈추고 소리내고 등등의 `method`를 가지고 있다.  



예시 2)

`person` 이라는 `class` 안에는 `p1`, `p2` 등등의 `instance` 가 있다. `person` 은 `age`, `name`, `gender`등등의 `attribute` 를 가지고 있고, 먹고 마시고 잠자고 등등의 `method`를 가지고 있다. 



### 클래스와 인스턴스 생성

* `class` 생성

```python
class Person:
    # 클래스 변수 정의 (모든 인스턴스가 공유)
    hobby = 'reading books'
    
    def __init__(self, name, age):
        # 인스턴스 변수 정의
        self.name = name
        self.age = age
        
    def eating(self):
        return '얌얌'
    
    def whatdo(self):
        return f'I like {self.hobby}.'
```

* `instance` 생성

```python
p1 = Person('박짹짹', 21)
print(p1.name, p1.age)  # 결과값 박짹짹, 21

print(p1.eating()) 		# 결과값 '얌얌'

print(p1.whatdo()) 		# 결과값 'I like reading books'
```



#### 💬 기억하세요 !

* 클래스와 인스턴스는 각자 다른 `namespace` 를 가지고 있다. 
* 인스턴스의 `attribute` 가 변경되면, 변경된 데이터는 인스턴스 객체 내의 `namespace`에 저장된다.
* 인스턴스의 attribute에 접근하면, **인스턴스 -> 클래스** 순으로 탐색한다.
  * p1 instance 에는 hobby 값이 없기 때문에 class 의 hobby 값을 찾아 `reading books`를 반환했다.





### 클래스의 생성자와 소멸자

* `__init__()`

  `init` method is a special method, which is called class constructor or initialization method that Python calls when we create a new instance of this class.  

* `__del__()`

  `del` method is a destructor method, which is called when an object gets destroyed.

```python
class Student:
    def __init__(self):
        print('Good morning, teacher!')
        
    def __del__(self):
        print('Thank you, bye!')
```

```python
s1 = Student() 	# Good morning, teacher!
del s1			# Thank you, bye!
```



