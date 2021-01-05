# JSON Schema

> JSON 데이터가 정해진 규칙에 따라 구성되어 있는지 유효성을 검사할 수 있는 방법.

## 메타데이터

>  스키마의 기본 정보를 나타내어 다른 사용자의 기본적인 이해에 도움이 될 수 있다.

* title : 스키마에 대한 이름
* description : 스키마에 대한 설명
* example : 스키마 검증에 통과하는 예시
* $comment : 주석



## 검증 조건 키워드

> 데이터의 유효성을 검사하기 위한 여러 가지 검증용 키워드

* type : 필드에 유효한 데이터 타입
* required : 반드시 포함되어야 하는 속성
* properties : 객체 타입인 경우 속성 표기



### 문자열 검증 방법

* minLength : 문자열 최소길이
* maxLength : 문자열 최대길이

* pattern : 해당 문자열이 명시한 정규 표현식과 일치하는지

  ```json
  {
    "type": "string",
    "pattern" : "(naver|google)\\.com"
  }
  ```

  -> "naver.com" 또는 "google.com" 경우만 허용

  

* format : 해당 문자열이 지정한 포맷을 갖는지

  - `date-time`, `time`, `date`, `email`, `hostname`, `ipv4`, `ipv6`

  ```json
  {
    "type": "string",
    "format": "date"
  }
  ```




### 배열 검증 방법

* minItems : 배열 요소의 최소 개수
* maxItems : 배열 요소의 최대 개수

* items : 배열의 요소 검증

  ```json
  {
    "type": "array",
    "items": {
      "type": "integer"
    }
  }
  ```

  -> 배열의 요소가 모두 정수이거나 비어있는 경우만 허용

  ```json
  {
    "type": "array",
    "items": [
      {
      	"type": "integer"
    	},
      {
        "type": "string",
        "format": "email"
      }
    ]
  }
  ```

  -> 타입이 혼합일 경우에도 검증 가능하다. 첫번째 요소는 정수형 타입이고 두번째 요소는 문자열이나 이메일 포맷을 가져야한다.

* uniqueItems : 배열 내에 중복 요소 검사. true 일 경우, 중복값이 허용되지 않는다.



### 객체 검증 방법

* properties : 객체 속성 검사

  ```json
  {
    "type": "object",
    "properties": {
    	"id": {
    		"type": "integer"
    	},
  		"username": {
        "type": "string"
      },
      "email": {
        "type": "string",
        "format": "email"
      },
      "birth": {
        "type": "string",
        "format": "date"
      }
    },
    "required": ["id", "username", "email"]
  }
  ```

* required : 필수 속성 값

* propertyNames : 속성의 이름 검증
* dependencies : 속성 간의 의존성 설정





참고자료 

https://madplay.github.io/post/json-schema-validation-examples