# Javascript 핵심 개념

## 1. 기본형과 참조형의 종류 및 차이점

* 기본형(primitive Type) : 값을 그대로 할당
  * Number
  * String
  * Boolean
  * null
  * undefined
* 참조형(Reference Type) : 값이 저장된 주소값을 할당(참조)
  * Object
    * Array
    * Function
    * RegExp

- 중첩 객체 : 참조형 데이터 안에 또 다시 참조형 데이터가 있는 경우.

```js
var obj = {
    a: [1,2,3]
};
```



## 2. 함수

### 1) 호이스팅

> hoist 끌어올리다 => 변수 선언과 함수 선언을 끌어올린다. ( 식별자 정보를 끌어올린다 )

```js
// 호이스팅 때문에 아래 코드는 오류가 생기지 않는다.
console.log(a());
console.log(b());
console.log(c());

function a() {
    return 'a';
}
var b = function bb( {
    return 'bb';
})
var c = function() {
    return 'c';
}
```

```javascript
// 위의 코드는 아래 코드로 전환되어 실행된다.
function a() {
    return 'a';
}

var b;
var c;
console.log(a());
console.log(b());
console.log(c());

b = function bb() {
    return 'bb';
}
c= function c() {
    return 'c';
}
```



### 2) 함수 선언문과 함수 표현식

> 함수 선언문과 함수 표현식은`할당 여부`에서 차이가 있다. 할당을 하지 않는 경우(함수선언문) 전체가 호이스팅의 대상이 되고, 할당을 한다면(함수 표현식) 함수는 그 자리에 남아있고 변수만 호이스팅의 대상이 된다.
>
> `함수 표현식을 쓰자` => 안전하고 예측가능한 코드를 만들기 위해서.

* 함수 선언문(function declaration)

```javascript
function a() {
    return 'a';
}
```



* 함수 표현식(named function expression) => 선언한 함수를 변수에 할당한다.

```javascript
var b = function bb() {
    return 'bb';
}
```



* (익명)함수 표현식(unnamed(anonymous) function expression)

```javascript
var c = function() {
    return 'c';
}
```



### 3) 함수스코프, 실행컨텍스트

> 스코프와 실행 컨텍스트는 `발생 시점`에 있다. 스코프는 함수가 정의될 때 결정되고/ 실행 컨텍스트는 함수가 실행될 때 결정된다.

* 스코프(scope) : 유효범위(변수) => 안에서 밖으로는 접근 가능하나, 밖에서 안에서는 접근 불가능.( 자기 자신으로부터 없다면 밖으로 또 없다면 밖으로 )

* 실행 컨텍스트(execution context) : 실행되는 코드 덩어리(추상적 개념)/ 동일한 조건(환경)을 지니는 코드 뭉치를 실행할 때 필요한 조건(환경정보) 
  * => 함수(or 전역공간)을 실행할 때 필요한 환경정보를 담은 객체

```javascript
var a = 1;
function outer() {
    console.log(a);
    
    function inner() {
        console.log(a);
        var a = 3;
    }
    
    inner();
    console.log(a);
}
outer();
console.log(a);

// 결과 => 1 undefined 1 1 
```



* call stack : 현재 어떤 함수가 동작하고 있는지, 다음에 어떤 함수가 호출되어야 하는지 등을 제어하는 자료구조
* Lexical Environment : 어휘적/사전적 환경
  * environmentRecord : 현재 문맥의 식별자 정보 => hoisting
  * outerEnvironmentReference : 현재 문맥에 관련 있는 외부 식별자 정보 => scope chain을 만듬 

### 4) 메소드

> 함수와 메소드의 차이는 `this에 바인딩을 하느냐 하지 않느냐`. 메소드는 this에 바인딩을 한다.



### 5) 콜백함수

> 호출해서 돌려줄 함수
>
> call / back => something will `call` this function `back` sometime somehow.
>
> * 특징
>
>   1) 다른 함수(A)의 매개변수로 콜백 함수(B)를 전달하면, A가 B의 제어권을 갖게된다.
>
>   2) 특별한 요청(bind)이 없는 한, A에 미리 정해진 방식에 따라 B를 호출한다. 

```javascript
// setInterval(callback, milliseconds)
setInterval(function() {	// 인자1. 콜백함수
    console.log('1초마다 실행');
}, 1000);	// 인자2. 실행주기
```



## 3. this

> 실행 콘텍스트가 활성화 될 때 this가 바인딩 된다. / 호출 방식에 따라 this가 동적으로 바인딩 => 호출 형태를 잘 보기!



### 1) 전역공간에서

> window / global



### 2) 함수 호출시

> window / global



### 3) 메소드 호출시

>메소드 호출 주체 ( 메소드명 앞)



```javascript
var a = 10;
var obj = {
    a: 20,
    b: function() {
        console.log(this.a); // 20 => this는 obj
        
        function c() {
            console.log(this.a); // 10 => this는 window
        }
        c();
    }
}
obj.b();
```

```javascript
var a = 10;
var obj = {
    a: 20,
    b: function() {
        var self = this;
        console.log(this.a); // 20 => this는 obj
        
        function c() {
            console.log(self.a); // 20 => self는 obj
        }
        c();
    }
}
obj.b();
```

=> 지금은 arrow function을 사용.



### 4) callback 호출시

> 기본적으로 함수내부에서와 동일 => 전역객체를 본다.
>
> but, 제어권을 가진 함수가 callback의 this를 명시한 경우에는 그에 따른다.
>
> but, 개발자가 this를 바인딩한 채로 callback을 넘기면 그에 따른다.

* call => 두번째 매개변수는 무한대로 나열가능 => 즉시호출
* apply => 두번째 매개변수는 배열 => 즉시호출
* bind => 두번째 매개변수는 무한대로 나열가능 => 새로운 함수 생성 => this 설정 가능.



```javascript
var callback = function() {
    console.dir(this);
};

var obj = {
    a: 1,
    b: function(cb) {
        cb(); // window
    }
};
obj.b(callback);
```

```javascript
var callback = function() {
    console.dir(this);
};

var obj = {
    a: 1,
    b: function(cb) {
        cb.call(this); // obj
    }
};
obj.b(callback);
```



```javascript
var callback = function() {
    console.dir(this);
};

var obj = {
    a: 1
};
setTimeout(callback, 100); // window
```

```javascript
var callback = function() {
    console.dir(this);
};

var obj = {
    a: 1
};
setTimeout(callback.bind(obj), 100); // obj
```



```javascript
document.getElementById('a').addEventListener('click', function() {
    console.dir(this);	// #a
});
```

```javascript
document.getElementById('a').addEventListener('click', function() {
    console.dir(this);	// obj
}.bind(obj));
```



### 5) 생성자함수 호출시

> 인스턴스

```javascript
function Person(n, a) {
    this.name = n;
    this.age = a;
};
var gomugom = new Person('고무곰', 30);
console.log(gomugom);
```



## 4. closure

> 클로저는 함수와 함수가 선언된 lexical environment의 조합이다.