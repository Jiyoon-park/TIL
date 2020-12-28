## CSS

화면에 HTML 각 요소의 styling을 어떻게 할 것인지를 정의하기 위한 언어이다. 각 요소에 style을 적용시키기 위해서는 `selector` 로 각 요소를 선택한다. 

html와 css는 각자의 문법을 갖는 다른 언어이며, html에 css가 포함될 수는 있지만, html이 없는 css는 의미가 없다. html에 css를 포함하는 방법으로 `1. link style`, `2.embedding style`, `3.inline style` 이 있다.

* link style

  ```html
  <html>
    <head>
      <link rel="stylesheet" href="css/style.css">
    </head>
    <body>
      ...
    </body>
  </html>
  ```

* embedding style

  ```html
  <html>
    <head>
      <style>
        h1 { color: red; }
        p  { background: aqua; }
      </style>
    </head>
    <body>
      ...
    </body>
  </html>
  ```

* inline style

  ```html
  <html>
    <body>
      <h1 style="color: blue">Hello</h1>
    </body>
  </html>
  ```



CSS에는 기본적으로 defalt값이 지정되어 있기 때문에, 개발자가 예상하지 못한 결과가 나올 때가 있다. 이런 상황을 방지하기 위해, `reset CSS`를 사용하기도 한다. 아래는 자주 사용되는 reset CSS이다.

* [Eric Meyer’s reset](http://meyerweb.com/eric/tools/css/reset/)



* 새로 학습한 셀렉터
  * 어트리뷰트 셀렉터
    * 셀렉터[어트리뷰트]
    * 셀렉터[어트리뷰트="값"]
    * 셀렉터[어트리뷰트~=”값”]
    * 셀렉터[어트리뷰트|=”값”]
    * 셀렉터[어트리뷰트^=”값”]
    * 셀렉터[어트리뷰트$=”값”]
    * 셀렉터[어트리뷰트*=”값”]
  * 후손 셀렉터, 자식 셀렉터
  * 인접 형제 셀렉터, 일반 형제 셀렉터
  * 링크 셀렉터, 동적 셀렉터
  * UI 요소 상태 셀렉터
  * 구조 가상 클래스 셀렉터(`:first-child`, `:last-child`, `:nth-child(n)`, `:nth-last-child(n)`)
  * 정합성 체크 셀렉터(`:valid`, `:invalid`)
  * **가상요소 셀렉터**



* margin, padding
  * 4개의 값 (위, 오, 아,  왼)
  * 3개의 값 (위, 오아, 왼)
  * 2개의 값 (위아, 오아)
  * 1개의 값 (위오아왼)