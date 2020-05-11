# DRF: Django REST framework

## basic process

* rest-framework 설치

```bash
$ pip install djangorestframework
```



* settings.py 앱 등록

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```



* url 분리

```python
# api/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('board/', include('board.urls')),
]
```

```python
# board/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('article/', views.artist_list, name='article_list'),
    path('article/<int:article_pk>', views.artist_detail, name='article_detail'),
    path('article/<int:article_pk>/comments/', views.comments_create, name='comments_create'),
]
```





* board/models.py 작성

```python
from django.db import models
# 'django-extensions' 설치 후 앱등록 'django_extensions'
from faker import Faker

f = Faker()

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.title
	
    # 데이터 더미 생성 방법
    @classmethod
    def dummy(cls, n):
        for _ in range(n):
            cls.objects.create(
                title=f.name(),
                content=f.text()
            )
            
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.TextField()

    def __str__(self):
        return f'{self.content} ({self.article})'
```



* board/serilaizers.py 생성

```python
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):
    class Meta:
        model = Article
        fields = ['title', 'created_at']

class ArticleDetailSerializer(serializers.ModelSerializer):
    comments = CommentSerializer(source='comment_set', many=True)
    comments_count = serializers.IntegerField(source='comment_set.count')
    class Meta:
        model = Article
        fields = ['id', 'content', 'comments_count', 'comments']
        
class CommentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Comment
        fields = ['id', 'content', 'article_id']   
```



* boards/views.py

```python
from django.shortcuts import render, get_object_or_404

from rest_framework.response import Response
from rest_framework.decorators import api_view

from .models import Article
from .serializers import ArticleSerializer

# rest framework
@api_view(['GET'])
def article_list(request):
    articles = Article.objects.all()
    serializer = ArticleSerializer(articles, many=True)
    # rest_framework.response.Reponse
    return Response(serializer.data)

@api_view(['GET'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    serializer = ArticleDetailSerializer(article)
    return Response(serializer.data)

@api_view(['POST'])
def comments_create(request, article_pk):
    serializer = ArticleSerializer(data=request.data)
    if serializer.is_valid():
        serializer.save(article_id=article_pk)
    return Response(serializer.data)
```





## drf-yasg - Yet another Swagger generator

https://github.com/axnsan12/drf-yasg

* 설치

```bash
$ pip install -U drf-yasg
```



* 앱등록

```python
INSTALLED_APPS = [
   ...
   'drf_yasg',
   ...
]
```



* board/urls.py

```python
# from rest_framework import permissions
...

from drf_yasg.views import get_schema_view
from drf_yasg import openapi

...

schema_view = get_schema_view(
   openapi.Info(
      title="Snippets API",
      default_version='v1',
      description="Test description",
      terms_of_service="https://www.google.com/policies/terms/",
      contact=openapi.Contact(email="contact@snippets.local"),
      license=openapi.License(name="BSD License"),
   ),
   public=True,
   permission_classes=(permissions.AllowAny,),
)

urlpatterns = [
    ...
    path('swagger/', schema_view.with_ui('swagger')),
    # path('redoc/', schema_view.with_ui('redoc')),
]
```

