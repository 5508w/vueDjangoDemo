
搭建流程：

    安装django后段api插件：

        pip install django-rest-framework
    创建一个新的名为books的应用:

        python manage.py startapp books 
        cd books
        touch urls.py
    进入setting配置books应用

        # book_demo/settings.py
        INSTALLED_APPS = [
            'django.contrib.admin',
            'django.contrib.auth',
            'django.contrib.contenttypes',
            'django.contrib.sessions',
            'django.contrib.messages',
            'django.contrib.staticfiles',

            # demo add
            'rest_framework',
            'books',
        ]
    在命令行中执行
        python manage.py makemigrations # 让 Django 知道我们在我们的模型有一些变更
        python manage.py migrate  # 创建表结构
    对整个项目的路由进行配置，让访问api/路径时候转到books应用中的urls.py文件配置进行处理。
        # book_demo/urls.py
        from django.contrib import admin
        from django.urls import path, include

        urlpatterns = [
            path('admin/', admin.site.urls),
            path('api/', include('books.urls')), # demo add
        ] 
    在models.py文件中写简单数据类Books
    在books文件夹中创建serializer.py文件，并写对应序列化器BooksSerializer
    在views.py文件中写对应的视图集BooksViewSet来处理请求
    在urls.py文件中写对应的路由映射

搭建原理：
    DRF通过视图集ViewSet的方式让我们对某一个数据类Model可以进行增删改查，而且不同的操作对应于不同的请求方式，比如查看所有books用get方法，添加一本book用post方法等，让整个后端服务是restful的。这样做之后就可以通过不同的网络请求对后端数据库的Books数据进行操作
