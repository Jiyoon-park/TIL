# Form을 이용한 요청 처리

> 사용자에게 값을 받고(`input/`), 이를 출력하는 페이지 만들기(`output/`)

####  💡 기억하세요

1. urls.py
2. views.py
3. templates



> **1. urls.py**


```python
# /app/urls.py
from django.urls import path
from . import views

urlpatterns = [
    # 사용자에게 값 받기
    path('input/', views.input), 	# /app/input/
    # 요청 받은 값 출력하기
    path('output/', views.output),	# /app/output/
]
```



> **2. views.py**

```python
from django.shortcuts import render
import requests

# 사용자에게 값을 받는 함수
def input(request):
    return render(request, 'input.html')

# 요청받은 값을 출력하는 함수
def output(request):
    # 사용자 입력값 받기_form 태그를 이용해서 받은 변수 이름 wanted
    wanted = request.GET.get('wanted')

    # api 요청 보내기 -> api url(사진요청 api), key(클라이언트 키), 검색대상(query)
    key = client-key값
    urls = f'https://api.unsplash.com/search/photos?client_id={key}&query={wanted}'

    response = requests.get(urls).json()


    # 응답값 확인 및 사진 추출
    photo_list = []
    for photo in response.get('results'):
        photo_list.append(photo.get('urls').get('regular'))

    context = {
        'wanted' : wanted,
        'photo_list' : photo_list
    }

    return render(request, 'output.html', context)

```



> **3. templates**

```html
<!-- input.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>원하시는 사진을 찾아드려요!</h1>
    <h2>무엇을 찾고 계신가요?</h2>
    <form action='/app/output/'>
        <!-- 요청하는 정보를 담는 변수 name 설정/여기선 wanted-->
        <input type="text" name="wanted">
        <input type="submit" value="submit">
    </form>

</body>
</html>
```

```html
<!-- output.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1> 안녕, 나를 찾고 있니? </h1>
    {% for photo in photo_list %}
        <h3>나는 너가 찾는 {{ forloop.counter }}번 {{ wanted }}야!</h3>
        <img src="{{ photo }}">
    {% empty %}
        <h1>Sorry! 너가 원하는 건 찾지 못했어. </h1>
    {% endfor %}

</body>
</html>
```



