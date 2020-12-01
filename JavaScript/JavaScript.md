# JavaScript

## 데이터 타입

* 동적 언어(dynamically typed)

  * 변수에 데이터 타입을 지정해 저장하지 않는다. 변수에 저장되는 값은 언제든지 데이터 타입을 바꿔 저장할 수 있다.

    ```javascript
    let apples = "sweet";
    apples = 3
    console.log(apples) // 3
    ```



* Primitive Type 

  >  값을 그대로 할당한다. 문자열이면 문자열, 숫자면 숫자 오직 하나의 데이터 타입만을 나타낼 수 있다.

  * Number
    * 정수(`+2**53` < x < `-2**53`)
    * 부동소수점 숫자
    * 특수 숫자 값( Infinity, -Infinity, NaN)
  * BigInt
    * 정수 끝 `+` n
  * String
    * 백틱으로 감싼 `${...}` 로 변수나 표현식을 문자열에 넣을 수 있다. 
  * Boolean
  * null
    * 비어 있는 값
  * undefined
    * 변수는 선언되었으나 값이 할당되지 않은 상태
  * Symbol



* Reference Type 

  >  값이 저장된 주소값을 할당(참조)한다. 키와 값으로 구성된 기본형 데이터의 집합이나 복잡한 객체와 같은 다양한 데이터를 담을 수 있다.

  * Object

    >  `let obj = { 키:값, 키:값, ..., }` ( `키:값` = `프로퍼티`)
>
    > 객체는 중괄호(`{}`) 안에 키와 값, 쌍으로 구성된 프로퍼티를 여러개 넣을 수 있다. 키엔 문자형, 값엔 모든 자료형이 허용된다. 키를 이용해서 해당하는 프로퍼티를 쉽게 찾아 읽거나 수정, 삭제가 가능하다. 추가도 마찬가지이다.

    ```javascript
    let dog = {
        name: 'hope',
        age: 2,
    };
    // 객체 dog에는 'name' 과 'age' 이름을 가진 두 개의 프로퍼티가 존재한다. 
    
    console.log(dog.name) // 'hope'
    console.log(dog[age]) // 2
    
    dog.color = 'grey';
    console.log(dog) // { name: 'hope', age: 2, color: 'grey'}
    
    dog["like swimming"] = true;
    console.log(dog) // { name: 'hope', age: 2, color: 'grey', like swimming: true}
    
    dog.age = 10;
    console.log(dog) // { name: 'hope', age: 2, color: 'grey'}
    
    delete user.age
    console.log(dog) // { name: 'hope', color: 'grey'}
    ```

- 객체 : function, array, regexp, error, date --- 

 


* typeof  ( 타입 연산자)

  ```javascript
  // 하위 호환성을 위해 고치지 않는 에러
  
  typeof null // object 		=> null은 null 타입
  typeof alert // function	=> function이란 타입은 없다. function은 object이다.
  ```

  

## 형변환

* 문자형으로 변환

  * String(value)

  ```javascript
  alert(String(123)); 	// "123"
  alert(String(true)); 	// "true"
  alert(String(false)); 	// "false"
  ```

  

* 숫자형으로 변환

  * Number(value)
  * `undefined`의 숫자형 변환은 `NaN` 
  * `null`의 숫자형 변환은 `0`

  ```javascript
  let a;		// a = undefined
  Number(a); 	// NaN 
  ```

  ```java
  alert(Number("     12   ")); 	// 12
  alert(Number("       "));		// 0
  alert(Number("12z"));			// NaN
  alert(Number(true));			// 1
  alert(Number(false));			// 0
  alert(Number(null));			// 0
  ```

  

* 불린형으로 변환

  * `""`(빈문자열)은 `false` 이나 `" "`(공백이 있는 문자열)이나 `"0"` 은 `true`

  ```javascript
  alert(Boolean(""));			// false
  alert(Boolean(" "));		// true
  alert(Boolean("0"));		// true
  alert(Boolean(0));			// false
  alert(Boolean(NaN));		// false
  alert(Boolean(undefined));	// false
  alert(Boolean(null));		// false
  alert(Boolean(1));			// true
  ```

  

  

## this

자바스크립트에서 `this`는 런타임에 결정됩니다. 메서드가 어디서 정의되었는지에 상관없이 `this`는 ‘점 앞의’ 객체가 무엇인가에 따라 ‘자유롭게’ 결정됩니다. 함수(메서드)를 하나만 만들어 여러 객체에서 재사용할 수 있다는 것은 장점이지만, 이런 유연함이 실수로 이어질 수 있다는 것은 단점입니다.