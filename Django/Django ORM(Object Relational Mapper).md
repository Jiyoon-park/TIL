# Django ORM(**O**bject **R**elational **M**apper)

> * 직접 SQL을 사용하지 않고도 ORM을 통해 파이썬 언어로 SQL 문을 생성/실행할 수 있다. -> 파이썬 언어와 DB SQL 사이의 통역사 역할 
>
> * 객체 지향적인 방법을 사용해서 DB의 데이터를 쉽게 조작할 수 있도록 한다.



### 터미널에서 shell 실행

> 일반 파이썬 쉘을 통해서는 프로젝트 환경에 접근할 수 없기 때문에, 프로젝트 내의 각종 모듈 패키지를 활용하기 위해서는 django shell 을 사용해야 한다.

```bash
$ python manage.py shell
```



> 추가 패키지 설치를 통해 편하게 활용해보자! 

#### 1. 설치
```bash
$ pip install django-extensions ipython
```

* [Django Extensions](https://django-extensions.readthedocs.io/en/latest/) include management commands, additional database fields, admin extensions and much more. 



#### 2. settings.py 에서 앱 추가

```python
INSTALLED_APPS = [
    'django_extensions',
    ...
]
```



#### 3. shell_plus 실행

```bash
$ python manage.py shell_plus
```





## 1. CRUD

> DB의 기본
* Create

  * ```python
    article = Article()
    article.title = '강아지'
    article.content = '멍멍'
    article.save()
    ```

  * ```python
    article = Article(title='강아지', content='멍멍')
    article.save()
    ```

  * ```python
    # .save() 안해줘도 되는 생성법
    Article.objects.create(title="강아지", content="멍멍")
    ```

  

* Read

  * ```python
    # 모든 데이터 조회 / for문을 돌려 하나씩 꺼내볼 수 있다.
    Article.objects.all() 
    ```

  * ```python
    # 고유한 식별번호로 단일 데이터 조회
    Article.objects.get(id=1)  # id 대신 pk(primary key) 써도 된다.
    ```

  

* Update

  * ```python
    a1 = Article.objects.get(id=1)
    a1.title = '고양이'
    a1.save()
    ```

  

* Delete

  * ```python
    article.delete()
    ```





목록페이지 이해 안감

redirect 도 모르겠음

django-extensions ipython 이 친구는 언제 사용...?