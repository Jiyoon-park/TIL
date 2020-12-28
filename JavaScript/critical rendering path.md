## Critical Rendering Path

> 브라우저가 서버로부터 HTML 응답을 받아 화면을 그리기 위해 실행하는 과정

1. DOM tree 
2. CSSOM tree
3. JS 실행



## json

> 서버 통신의 시작



client와 serve 와의 통신 == http(typertext transfer protocol) 

클라이언트의 request, 서버의 response

문서나, 이미지 파일, 링크 다 요청.

http를 사용해서 서버에게 데이터를 요청해서 받아오는 방법. 

1) ajax(asynchronous JS and xml) / 



fetch() API

XMLHttpRequest 



what is XML => html과 같은 markup language 중 하나.

서버와 데이터를 주고 받을 때에는 xml 과 json 등등을 사용. 

* 요즘에는 XML보단 가독성적인 부분에서 더 좋고 크기도 적은 JSON(JS Object Notation)사용

* 키와 밸류로 이어져있음.

* 가벼운 텍스트 기반 구조

* 프로그래밍 랭귀지나 플랫폼 상관 없이 사용이 가능하다.

* 서버와 데이터를 주고 받을 수 있는 가장 간단한 포맷



serialize 직렬화 <--> deserialize 

* object to JSON

  ```javascript
  let json = JSON.stringify(['apple', 'banana']); // ["apple", "banana"]
  ```

  

* JSON to object

  ```javascript
  let object = JSON.parse()
  ```

  

hoisting 이란? var, function 선언이 자동적으로 맨 위로 올라가는 것





