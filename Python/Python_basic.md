# Python_basic

`Life is too short, you need python.`



### 자료형

#### 1. number `immutable`

> integer : 정수형 / float : 실수형

* 연산자

  * 사칙연산 ( `+`, `-`, `*`, `/` )

  * 제곱 ( `**` )

  * 나머지 ( `%` )

  * 몫 (`//` )

    

#### 2. string `immutable`

> 큰따옴표(`"`)나 작은따옴표(`'`) 로 문자를 둘러싸면 문자열이 된다.
>
> multiline일 경우, 큰따옴표 세개(`"""`), 작은따옴표 세개(`'''`) 로 문자열을 둘러싼다.

* 이스케이프 코드

  * `\n` : 줄 바꾸기
  * `\t` : 탭 간격 주기
  * `\\` : 백슬래쉬(`\`) 그대로 사용하기
  * `\'` : 작은따옴표(`'`) 그대로 사용하기
  * `\"` : 큰따옴표(`"`) 그대로 사용하기

* 문자열 연산자

  * `+` 

    ```python
    a = 'hello'
    b = ' world'
    print(a+b) # 결과값 'hello world'
    
    # 숫자가 문자열이 되었을 때 주의할 것
    c = '12'
    d = '345'
    print(c+d) # 결과값 '12345'
    ```

  * `*`

    ```python
    a = 'hi'
    print(a*2) # 결과값 'hihi'
    ```

* 문자열 포맷팅

  1) `%` 

  * `%s` : 문자열
  
	* `%d` : 정수
  
      ```python
      num = 3
      print('I have %s apples' % num) # 결과값 I have 3 apples
      print('I have %d apples' % num) # 결과값 I have 3 apples
	    ```
      
  * `%f` : 부동소수
  
      ```python
      print("%0.3f" % 1.24541254) # 결과값 1.245 
      print("%0.4f" % 1.24541254) # 결과값 1.2454 
      print("%0.5f" % 1.24541254) # 결과값 1.24541
      ```
  
  * `%%` : %
  
  2) `format()`

  ```python
    print("{} {}".format('I', 'did')) # 결과값 'I did'
    print("{1} {0}?".format('I', 'did')) # 결과값 'did I?'
  ```

  * `%f` : 소수점 표현

    ```python
    number = 1.24541254
    print("{0:0.3f}".format(number)) # 결과값 1.245
    ```

  3) `f` 문자열
  ```python
num = 3
print(f'i have {num} apples.') # 결과값 i have 3 apples.
  ```



#### 3. list 

#### 4. tuple `immutable`

#### 5. dictionary

#### 6. set

#### 7. bool `immutable`

