# DTL( Django Template Language )

> django 의 html 안에서는 DTL을 사용함으로써 파이썬 변수와 문법을 사용할 수 있다.



### 1. Variables

```html
{{ variable }}
```

* 변수의 속성에 접근하기 위해서는 `[]` 가 아닌 `.` 을 사용한다.

```html
{{ variable.attribute }}

<!-- example -->
{{ section.title }}
{{ fruits.0 }}
```





### 2. Tags

```html
<!-- 몇개는 닫는 태그가 꼭 필요한 태그들도 있다-->
{% tag %} ... tag contents ... {% endtag %}
```



#### *- for*

```html
<!-- 시퀀스에서 하나씩 뽑아 -->
{% for article in articles %}
	<!-- 원하는 동작 실행 -->
	{{ article }} 
{% endfor %}
```



#### *- if, elif, else*

```html
{% if students|length > 2 %}
	many students.
{% elif students|length == 1 %}
	I'm the only one left.
{% else %}
	Nobody here.
{% endif %}
```

you can learn more tags here: [built-in tag reference](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#ref-templates-builtins-tags)



### 3. filter

* length 

```html
<!-- value='name' -->
{{ value|length }}
<!-- output: 4 -->
```

* add


```html
<!-- value = 4 -->
{{ value|add:"3" }}
<!-- output: 7 -->
```

```html
<!-- first = [1, 2, 3], second = [4, 5, 6] -->
{{ first|add:second }}
<!-- output: [1, 2, 3, 4, 5, 6] -->
```

* capfirst

```html
<!-- value='python' -->
{{ value|capfirst }}
<!-- output: 'Python' -->
```

* cut

```html
<!-- value='Life is short, you need python.' -->
{{ value|cut:" " }}
<!-- output: 'Lifeisshort,youneedpython.' -->
```

you can learn more filters here: [built-in filter reference](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#built-in-filter-reference) ( join, get_digit, date, dictsort, make_list, last, first, random, slice, title, truncatechars, upper ... )



### 4. comments

```html
{# comments #}

<!-- example -->
{# greeting #} 
Good morning
```





### 5. template inheritance

> 'base.html' 의 템플릿 상속을 통해 자식 템플릿에 공통적인 *__뼈대__* 를 제공해 줄 수 있다.
>
> `base.html` defines an HTML skeleton document

```html
<!-- project/templates/base.html -->

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>django basic</title>
    {% block css %}
    {% endblock %}
</head>
<body>
    <h1>이 템플릿 뼈대를 상속할거야</h1>
    {% block body %}
    {% endblock %}
</body>
</html>
```



> 자식 템플릿은 {% block %} 을 통해 overide 가 가능하다.
>
> `child.html` fills the empty blocks with content.

```html
<!-- app/templates/child.html -->

{% extends 'base.html' %}

{% block css %}
	p {
		color : green;
}
{% endblock %}

{% block body %}
	<p>나는 상속받은 자식이고 여기는 내가 보여주고 싶은거 보여줄거야</p>
{% endblock %}
```

💡  *__extends__*  태그가 상속의 KEY 💡 

 

#### 상속하고 바꾸어야 할 project/settings.py

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # 여기 아래 'DIRS' 부분 추가해주기
        # APP 내에 있는 폴더 아닌 추가적으로 활용하고 싶은 템플릿의 경로 / BASE_dIR는 root.
        'DIRS': [os.path.join(BASE_DIR, 'djanog-intro', 'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```



