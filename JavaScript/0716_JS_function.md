# 0716

## JavaScript의 함수

* 함수

  * JS 내장 객체인 function 생성자로 생성된 객체

  * 함수는 객체이므로 프로퍼티와 메소드를 가질 수 있다.

    * 메소드 : 함수가 객체의 프로퍼티

    

* 함수와 다른 객체와의 차이점

  * 함수는 호출이 가능하다.
  * 함수는 프로토타입 프로퍼티를 가진다.



* 함수 생성 방법

  * 1) 함수 선언식 => 실행 컨텍스트에 영향을 끼친다.

    ```javascript
    function User () {};
    var user = new User();
    ```

  * 2) 함수 표현식

    ```javascript
    var workout = funtion () {};
    ```



* 객체 생성 방법

  * Object() 생성자

    ```javascript
    var user = new Object();
    user.name = 'sun';
    user.interests = ['swimming'];
    ```

  * 객체 리터럴

    ```javascript
    var user = {
        name: 'sun',
        interests: ['swimming']
    };
    ```

    ```javascript
    var user = {
      get role() {
          return 'Engineer';
      }  
    };
    ```

  * 생성자 함수

    ```javascript
    function User(name, interests) {
        this.name = name;
        this.interests = interests;
    }
    
    var user = new User('sun', ['swimming']);
    ```

  * Object.create()

    ```javascript
    // 위에서 생성한 User 생성자 함수의 프로토타입과 Object.create() 메소드 활용
    var user = Object.create(User.prototype, {
        name: { value: 'sun'},
        interests: { value: ['swimming']}
    });
    ```

  * 생성 함수

    ```javascript
    function createUser(name, interests) {
        var user = {};
        user.name = name;
        user.interests = interests;
        return user;
    }
    var user = createUser('sun', ['swimming']);
    ```

  * ES6의 클래스

    ```javascript
    class User {
        constructor(name, interests) {
            this.name = name;
            this.interests = interests;
        }
    }
    
    let user = new User('sun', ['swimming']);
    ```

    

