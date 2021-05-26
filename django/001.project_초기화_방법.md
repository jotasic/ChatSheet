# Django 초기설정

## 가상환경 만들기
 - 특정 프로젝트만 쓸 패키지들을 분리하기 위해 사용함.
 - 프로젝트마다 필요한 패키지들이 달라서 환경을 분리하기 위한 용도

```bash
conda create -n [가상환경이름] python=[파이썬버전]
```

## 가상환경 들어가기
```bash
conda activate [가상환경이름]
```

## django에 필요한 패키지 설치
```bash
pip install django
pip install mysqlclient
```

# django 프로젝트 생성 및 설정
프로젝트 생성을 원하는 디렉토리로 이동 후, 폴더를 만들어 폴더안에서 아래 커맨드 입력
```bash
django-admin startproject [프로젝트명]
```

## git ignore 설정
gitignore는 git에 관리하기 싫은 파일들을 설정 하는 파일이다.

[gitignore](https://gitignore.io) 접속하여 `Python, VisualStudioCode, vim, macOS, zsh` 을 입력하여 .gitignore 파일에 필요한 정보를 만든다.
[생성 링크](https://www.toptal.com/developers/gitignore/api/python,visualstudiocode,vim,macos,linux,zsh,django)

## Database 생성
```sql
create database [DB명] character set utf8mb4 collate utf8mb4_general_ci;
```

##  설정파일 변경

### 설정파일 분리
- `[설정파일이름].py` 파일을 만들어서 민감한 설정값을 git에 올라가지 않도록 모은다.
- 설정파일은 `manage.py`와 같은 경로에 만든다.
> ex) my_setting.py


`[설정파일이름].py`로 `sttings.py`에 있는`DATABASES` 및 `SECRET_KEY` 정보를 옮긴다.

그 외 공개되서는 안되는 민감한 정보를 옮긴다.
```python
DATABASES = {
    'default' : {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'DATABASE 명',
        'USER': 'DB접속 계정명',
        'PASSWORD': 'DB접속용 비밀번호',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
SECRET_KEY = [settings.py에 있는 key]
```

### 분리한 설정 정보 settings.py에 import 시키기
`settings.py`에 `import`후  `DATABASES` 및 `SECRET_KEY` 정보 포함시키기

```python
from [설정파일이름] import SECRET_KEY, DATABASES
...
...
SECRET_KEY = SECRET_KEY
DATABASES = DATABASES
```

## 사용안하는 APP 주석 처리
`setttings.py`안에 있는 `INSTALLED_APPS`에 포함된 APP중에 안 쓰는것을 주석 처리한다.
```python
INSTALLED_APPS = [
    # 'django.contrib.admin',
    # 'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

```

`setttings.py`안에 있는 `MIDDLEWARE`에 아래 내용 주석 처리
```python
    # 'django.middleware.csrf.CsrfViewMiddleware',
    # 'django.contrib.auth.middleware.AuthenticationMiddleware',
```

## urls.py 에서 안쓰는 app에 대한 import 및 urlpatterns 삭제
```python
#from django.contrib import admin
from django.urls import path

urlpatterns = [
# path('admin/', admin.site.urls),
]
```

## APP 만들기
`manage.py`가 있는 경로에서 아래 명령어를 입력
```bash
python manage.py startapp [app이름]
```


`settings.py`안에 있는 `INSTALLED_APP`에 만든 app정보를 추가

```python
INSTALLED_APPS = [
    # 'django.contrib.admin',
    # 'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'products', #새로 만든 APP
]

```


