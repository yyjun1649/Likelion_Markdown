# Django

---

### MTV 패턴

---

python -m venv [가상환경명]

source [가상환경명]/Script/activate

pip install django

django-admin startproject [프로젝트이름]

python manage.py runserver



MTV

Model , Template , View

- Template
  - 프론트엔드
  - 템플릿언어
- Model
  - DB
-  View
  - 데이터를 처리하는곳
  - MTV중 핵심



실습



1. Django 실행, myvenv 실행

2. 폴더를 만들면

firstproject에 있는 setting에 INSTALLED_APPS에
'[폴더이름].apps.[폴더이름Config(폴더이름 첫글자는 대문자)]'



3. 이후 templates 폴더 생성 후 html을 만들면

firstproject에 있는 urls에 

- form [폴더이름] import views as [원하는이름]
- path('[주소]/', [원하는이름].[html], name = "[이름]")



4. 이후 각자의 폴더에 views에

def html(request):

​	return render(request,"[html파일이름]") 

입력

-> [html파일이름] 실행





-----

Class 생성

> class Blog(models.Model):
> title = models.CharField(max_length=200)
> writer = models.CharField(max_length=100)
> pub_date = models.DateTimeField()
> body = models.TextField()
> def __str__(self):
> 		return self.title



![image-20210608170050013](C:\Users\YOON YOUNGJUN\AppData\Roaming\Typora\typora-user-images\image-20210608170050013.png)![image-20210608170111536](C:\Users\YOON YOUNGJUN\AppData\Roaming\Typora\typora-user-images\image-20210608170111536.png)

makemigrations ( python manage.py makemigrations)

- 앱 내의 migration 폴더를 만들어서 models.py 변경사항 저장

migrate ( python manage.py migrate )

- Migration폴더를 실행시켜 데이터베이스에 적용



# CRUD

### Read

> path('\<str:id\>', detail, name"detail")  : 사용자 id마다 다른 주소
>
> detail함수
>
> - def detail(request, id):
>   	blog = get_object_or_404(Blog,pk=id)
>   	return render(request,'detail.html',{'blog':blog})



### Create

> new 함수
>
> - def new(request):
>   return render(request,'new.html')
>
> 
>
> #### Get
>
> > - 데이터를 얻기 위한 요청
> > - 데이터가 url에 보임
> > - 보안 안좋음
>
> #### Post
>
> > - 데이터 생성하기 위한 요청
> > - 데이터 url 안보임
> > - Crsf 공격방지 (사이트 간 요청 위조)
> >
> > ~~~~
> > ex)
> > <form action ="" method ="post">
> > 	{%csrf_token}
> > 	~~~
> > </form>
> > ~~~~
> >
> > 과 같은 방식으로 post 방식 이용시 {%csrf_token} 반드시 입력
>
> ~~~
> from django.shortcuts from render,redirect,get_object_or_404
> def Create(request):
> 	new_blog = Blog()
> 	new_blog.title = request.POST['title']
> 	new_blog.pub_date = timezone.now
> 	new_blog.save()
> 	return redirect('detail',new_blog.id)
> ~~~
>
> 이후 html 에서
>
> ~~~
> <from action="{%url 'create'%}" method="post">
> ~~~
>
> 

### Update

>~~~
>views:
>def edit(request,id):
>	edit_blog = Blog.objects.get(id=id)
>	return render(request,'edit.html',{'blog':edit_blog})
>	
>def update(request,id):
>	update_blog = Blog.objects.get(id=id)
>	update_blog.title = request.POST['title']
>	~~
>	update_blog.save()
>	return redirect('detail',new_blog_id)
>
>urls:
>urlparttern = [
>path('edit/<str:id>',edit,name="edit")
>path('update/<str:id>',update,name="update")
>]
>
>
>html:
><a herf = "{%url 'edit' blog_id %}">수정하기</a>
>~~~
>
>
>
>### Delete
>
>>~~~
>>views:
>>def delete(request,id):
>>	delete_blog = Blog.objects.get(id=id)
>>	delete_blog.delete()
>>	return redirect('home')
>>	
>>urls:
>>path('delete/<str:id>',delete,name="delete")
>>
>>html:
>><a herf = "{%url 'delete' blog_id %}">삭제하기</a>
>>~~~
>>
>>
>>
>>
>>
>>
>
>

