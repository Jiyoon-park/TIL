# Django Framework

> `Python` 으로 만들어진 오픈소스 웹 어플리케이션 프레임 워크 

* MTV 패턴 ( **M**odel **T**emplate **V**iew )
* URL 형태를 개발자가 직접 결정가능/ URL 형태를 파이썬 함수에 연결
* 관리자 웹 인터페이스 제공

---



### 설치하기

```bash
$ pip install django==2.1.15
```



### django 프로젝트 시작

---

#### 프로젝트 생성

```bash
$ django-admin startproject blahblah
```

* `blahblah` 부분에 원하는 project 이름을 넣는다.
* project 생성 후 `ls` 명령어를 통해  `manage.py` 파일을 확인할 것



#### 서버실행

* blahblah 폴더의 settings.py 파일 수정하기

    ```bash
    # 28번째 줄_호스트 설정
    ALLOWED_HOST = ['*']
    
    # 106번째 줄_언어 설정 
    LANGUAGE_CODE = 'ko-KR'
    
    # 그 아래_시간 설정
    TIME_ZONE = 'Asia/Seoul'
    ```

* `manage.py` 파일이 있는 공간에서 `$ python manage.py runserver 8080` 로 서버 실행 가능

    ```bash
    ~/ $ cd blahblah
    ~/blahblah/ $ python manage.py runserver 8080 
    ```



####  앱 생성

* project 생성 후 `ls` 명령어를 통해 `manage.py` 를 확인 후, 앱 생성하기

	```bash
	$ python manage.py startapp blahblah
	```
	
* `blahblah` 부분에 원하는 app 이름을 넣는다



### ✨기억하세요 순서✨

1. `urls.py`

   * `from ~ import ~` 
   * `path` 추가
     * ex) path('idex/', views.index)

2. `views.py` 

   ```python
   def func(request):
       context = {
           'result' = result,
       }
       return render(request, 'a.html', context)
   ```

   * `request`  반드시 기억할 것
   * `context` 는 dictionary 로, 여러가지의 정보를 하나로 묶어 `a.html` 로 넘겨줄 수 있다. 

3. `templates`

   * templates 에 `views.py` 에 작성한 다양한 `html` 파일 작성 



### 리눅스 명령어

* `cd` : change directory
  * `$ cd ../` : 상위 directory로 이동
  * `$ cd` : root 로 이동
* `mkdir` : make directory
* `ls` : list
* `touch` : make file



### 리눅스 단축키

* `ctrl` + `l` : clear
* `ctrl` + `c` : 서버 종료


