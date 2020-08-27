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

  >  값을 그대로 할당

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

  >  값이 저장된 주소값을 할당(참조) => 키와 값으로 구성된 기본형 데이터의 집합

  * Object

    > `let obj = { 키:값, 키:값, ..., }` ( `키:값` = `프로퍼티`)

    * Function
    * Array
    * RegExp



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

  

  