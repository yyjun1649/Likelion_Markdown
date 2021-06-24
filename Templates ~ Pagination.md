

## Templates

공통된 것을 만들고 싶을때 Templates 상속을 이용

~~~
<div class = "container">
	{% block content %}
	{% endblock %}
</div>
~~~

를 templates 파일 내에 base.html을 만들어 입력



~~~
{% extends 'base.html' %}

{% block content %}
~
~
~
~
~
~
{% endblock %}
~~~

다른 html 파일에 head, body를 제거후 사용하면 block content와 endblock 사이의 내용이 base.html을 포함하여 출력



setting.py 에서

TEMPLATES 에 'DIRS' : ['프로젝트이름/템플릿주소'] 로 입력



---

# URLS 각각 관리하기

blog 파일 내에 urls.py 만든 후 기존 urls.py 복붙

1. admin, 메인페이지 제거
2. from .views import *



기존 urls.py

1. from blog.views import home
2. 어드민 홈을 제외하고 제거
3. path('blog/', include('blog.urls'))
4. from django.urls import path,include



---

# Static

정적 파일
	lmg, js, css



static 폴더 만들기

1. img 파일

2. setting.py 폴더  ->

     STATIFCFIES_DIRS = [

   ​				os.path.join(BASE_DIR, 'blog', 'static')]

   -> 현재 스태틱 파일은 어디?

   STATIC_ROOT = os.path.join(BASE_DIR, 'static')

   -> 스태틱 파일을 어디에 모을건지?

3. 터미널에 python manage.py collectstatic

4. base.html에  Navbar 삭제하고

   ~~~
   <a class ="navbar-brand" href="{%url 'home'%}">
   <img src="{% static 'likelion.png'%}" alt="" width ="50" height ="25">
   ~~~

   입력



---

# Media

사진의 url

1. static.py

   ~~~
   MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
   # 이용자가 업로드한 파일을 모으는 곳
   MEDIA_URL = '/media/'
   # MEDIA 파일의 URL 설정
   ~~~

2. url.py

   ~~~ 
   from django.conf import setting
   from django.conf.urls.static import static
   
   urlpatterns = [
   ~
   ] + static (settings.MEDIA_RUL,documnet_root=settings.MEDIA_ROOT)
   ~~~

3. models.py

   ~~~
   img = models.ImageField(upload_to = "blog/", blank = True, null = True)
   ~~~

4. migration 삭제

5. pillow 다운

   1. pip install pillow
   2. python mange.py makemigrations
   3. python mange.py runserver
   4. admin 이동

이미지 파일 받아오기 ( 이미지 업로드 )

~~~
html
<form action = {%url 'create' method = "post" enctype = "multipart/form-data"}
사진 : <input type ="file" name = "image">

views.py
def create(request):
	new_blog.image = request.FILES['image']
	
detail.html
{% if blog.image %}
<img src = "{{blog.image.url}}" alt ="">
{% endif %}
~~~



---

# Form

1. blog 폴더 내 forms.py 생성

   ~~~
   from django import forms
   from .models import Blog
   
   class BlogForm(forms.ModelForm):
   	class Meta:
   		model = Blog
   		fields = ['title','writer','body','image']
   ~~~

~~~
views.py

from .forms import BlogForm

def new(request):
	form = BlogForm()
	return render(request,'new.gtml',{'form':form})
	
def create(request):
	form = BlogForm(request.POST,request.FILES)
	if form.is_vaild():
		new_blog = form.save(commit = False) 
		new_blog.pub_date = timezone.now()
		new_blog.save()
		return redirect('detail',new_blog.id)
	return redirect('home')
	
new.py

{%csrf_token%}
{{form.as_p}} # <table>as_table</table> 도 가능

~~~

---

# User 확장과 인증

models.py 에 컬럼들 저장되어있음.

f11 로 확인



1. python manage.py startapp account

2. settings.py 에 INSTALLED_APPS 에 account 등록

3. views.py에

4. 
   ~~~
   from django.shortcuts import render,redirect
   from django.contrib.auth.forms import AuthenticationForm, UserCreationForm
   
   from django.contrib.auth import authenticate,login,logout
   
   def login_view(request):
   	if request.method == 'POST':
   		form = AuthenticationForm(request=request,data=request.POST)
   		if form.isvalid(): # 유효성 검사
   			username = form.cleaned_data.get("username")
   			password = form.cleaned_data.get("password")
   			user = authenticate(request = request,username=username,
   									password = password)
   			if user is not None:
               	login(request, user)
               return redirect("home")
   			
   	else:
   		form = AuthenticationForm()
   		return render(request, 'login.html',{'form':form})
   		
   
   def logout_view(request):
   	logout(request)
   	return redirect("home")
   ~~~

   추가

5. urls.py 생성 -> blogs에 url import 복붙.

   ~~~
   urlpatterns = [
   	path('login/',login_view,name="login"),
   	path('logout/',logout_view,name="logout")
   ]
   ~~~

6. blog에 url.py

   ~~~
   urlpatterns = [
   path('account/',include(account.urls)),
   ]
   ~~~

   추가

7. templates 폴더 생성 , login.html 생성

   ~~~
   # login.html
   
   {% extends 'base.html' %}
   
   {% block content %}
   <h1>Login</h1>
   
   <form action = "{%url 'login'%} method="post">
   	{%csrf_token%}
   	{{form.as_p}}
   	<button type="submit"> submit</button>
   </form>
   {% endblock %}
   ~~~

   

8. base.html

   ~~~
   <li>
   <a class = "nav-link" herf="{% url 'login' %}">Login</a>
   </li>
   <li>
   <a class = "nav-link" herf="{% url 'logout' %}">Logout</a>
   </li>
   ~~~

   링크부분 수정

9. home.html

   ~~~
   {% block content %}
   	{% if user.is authenticated %}
   		{{user.username}}
   	{% endif %}
   ~~~



### 회원가입

---

~~~
# views.py

def register_view(request):
	if request.method == "POST":
		form = UserCreationForm(request.POST)
		if form.isvaild(): # 유효성검사
			user = form.save()
			login(request,user)
		return redirect("home")
		
	else:
		form = UserCreationForm()
		return render(request,'signup.html',{'form':form})
		
		
		
		
from .forms import RegisterForm 생성 후 CreationForm 제거 -> 수정
~~~

~~~
# urls.py

urlpatterns=[
	path('register',reigster_view,name="signup")
]
~~~

~~~
# signup.html

{% extends 'base.html' %}

{% block content %}
<h1>Sign up</h1>

<form action = "{% url 'signup' %}" method="post">
	{%csrf_token%}
	{{form.as_p}}
	<button type="submit"> submit</button>
</form>
{% endblock %}

~~~

~~~
# base.html

{% if not user.is authenticated %} # 로그아웃 상태
<li>
<a class = "nav-link" herf="{% url 'login' %}">Login</a>
</li>
{%endif%}

{% if user.is authenticated %}	   # 로그인 상태
<li>
<a class = "nav-link" herf="{% url 'logout' %}">logout</a>
</li>
{%endif%}

{% if not user.is authenticated %}
<li>
<a class = "nav-link" herf="{% url 'Signup' %}">Signup</a>
</li>
{%endif%}
~~~

~~~
# account.py

from django db import models
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
	nickname = models.CharField(max_Length=100)
	university = models.CharField(max_Length=50)
	location = models.CharField(max_Length=200)
~~~

~~~
# setting.py

AUTH_USER_MODEL = 'account.CustomUser'
~~~

이후 명령어 python mange.py makemigrations

~~~
# forms.py

from django.contrib.auth.forms import UserCreationForm
from .models import CustomUser

class RegisterForm(UserCreationForm):
	class Meta:
		model = CustomUser
		fileds = ['username','password1','password2','nickname','location',...]
~~~

~~~
# admin.py

from django.contrib import admin
from .models import CustomUser

admin.site.register(CustomUser)
~~~





---

# Pagination

분리해서 전송

~~~
# views.py

from django.core.paginator import Pageinator

def home(request):
	blogs = Blog.objects.all()
	paginator = Paginator(blogs,3)
	page = request.GET.get
	blogs = paginator.get_page(page)
~~~

~~~
# home.html

{%if blogs.has_previous%}
<a href ="?page = 1">처음</a>
<a href ="?page = {{blogs.previous_page_number}}">이전</a>
{%endif%}
<span>{{blogs.number}}</span>
<span>of</span>
<span>{{blogs.paginator.num_pages}}</span>
{%if blogs.has_next%}
<a href ="?page={{blogs.next_page_number}}">다음글</a>
<a href ="?page={{blogs.paginator.num_pages}}">이전</a>
{%endif%}
~~~

---

# QureySet 가져오기

~~~
# views.py

def home(request):
	blogs = Blog.objects.order_by('-pub_date') # 최신글이 위로 올라옴. (-를 빼면 오래된 글부터)
	search = request.GET.get('search')
	if search == 'true':
		author = request.GET.get('writer')
		blogs = Blog.objects.filter(writer=author)
		return render(request,'home.html',{'blogs':blogs})
	
	paginator = Paginator(blogs,3)
	page = request.GET.get
	blogs = paginator.get_page(page)
~~~

~~~
# home.html

<a herf ="?search=true&writer={{user.nickname}}">내가 쓴 글</a> # a태그를 눌렀을 때 filter을 통해 조건에 맞는 것만 보임.

filter와 반대된 것
exclude(filter에 제외된 것들을 출력)
~~~





