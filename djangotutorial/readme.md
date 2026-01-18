### django網站建置 https://docs.djangoproject.com/en/6.0/intro/tutorial01/
## python版本:3.14.2 django:6.0
# 常用指令
python --version(檢查py版本)
python -m django --version(檢查Django版本)
python manage.py runserver(啟動伺服器)
python manage.py migrate(檢查INSTALLED_APP,以及其他新增的migration)
python manage.py shell(進入Django的shell)

# 一次性指令
pip install --upgrade Django(下載最新Django)
python -m django startproject mysite djangotutorial(網站專案生成)
python manage.py startapp polls(創建polls資料夾)

# Shell指令
exit()(退出shell)

- 到官網下載python(amd64)
記得勾選添加至環境變數
- 重開機
- 進入虛擬環境(Ctrl + \ )
- 初始化網站
python -m django startproject mysite djangotutorial
- 運行網站
python manage.py runserver

- 創建polls
python manage.py startapp polls
- 在polls/views.py添加
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
- 創建urls.py in polls
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
- 編輯urls.py in mysite
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("polls/", include("polls.urls")),
    path("admin/", admin.site.urls),
]
- 試著啟動server(https://localhost:8000/polls)
python manage.py runserver

# 資料庫設定 https://docs.djangoproject.com/en/6.0/intro/tutorial02/

- 建置Question, Choice模型 in polls/models.py
class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

- 在mysite/setting添加
"polls.apps.PollsConfig",

- python manage.py makemigrations polls
讓Django對你的models.py做儲存(migration)

- python manage.py sqlmigrate polls 0001

- python manage.py migrate
重複檢查,因為剛剛新增了polls 0001
(page2)