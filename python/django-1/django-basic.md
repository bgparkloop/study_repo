# Django Basic

## Django 특징들

Django는 MVC 패턴 기반 MVT로 동작

* MVC : Model - View - Controller
  * Model : 데이터베이스에 엑세스하는 컴포넌트
  * View : 데이터를 사용자에게 보여주는 컴포넌트
  * Controller : 데이터를 가져오고 변형하는 컴포넌트
* MVT in django : Model - View - Template
  * Model은 동일
  * View는 MVC의 Controller와 동일
  * Template은 MVC의 View와 동일

### 기본 특징들

| ORM\(Object Relational Mapping\) | 데이터베이스 시스템과 데이터 모델 클래스를 연결시키는 다리역할. 다양한 데이터베이스 시스템을 지원하며, SQL을 사용하지 않고도 테이블 조작이 가능. |
| :--- | :--- |
| 관리자 화면 시스템 | 콘텐츠 및 데이터베이스 관리 등을 위한 관리자화면을 제공함. |
| 자체 템플릿 시스템 | 확장과 디자인이 쉬운 강력한 템플릿 시스템을 갖춤. |
| 캐시 시스템 | 동적 페이지 관리를 위한 캐시 시스템을 지원함. 메모리, 데이터베이스 내부, 파일 시스템 중 어느 곳에나 저장 가능. |
| 언어 지원 | 다국어 지원. |
| 개발 환경 | 테스트용 웹 서버 등 개발에 도움되는 다양한 기능 제공. 또한, 소스 파일의 변경사항을 바로바로 반영하여 웹 서버를 다시 시작하지 않아도 됨. |

### 장고 기본 세

1. Python 사용 가능 환경에서 pip install Django 로 설치.

2. 프로젝트 생성을 위해 다음과 같은 명령어 실행 \(project\_name 부분에 프로젝트 이름을 넣으면 생성\)

```text
django-admin startproject project_name
```

3. 웹 애플리케이션에서 동작할 애플리케이션 생성을 위해 다음과 같은 명령어 실행. 실행 전 프로젝트 폴더로 이동.\(위의 project\_name 폴더\)

```text
python manage.py startapp app_name
```

4. settings.py를 적절하게 조정 후, 아래와 같은 명령어로 데이터베이스 기본 설정 진행. \(기본 테이블 생성을 진행함\)

```text
python manage.py migrate
```

5. 웹 서버를 실행하여 잘 동작하는지 확인

```text
python manage.py runserver [IP][PORT]
IP : 지정하지 않으면 기본 주소 127.0.0.1
PORT : 지정하지 않으면 기본 포트 8888
PORT만 할 경우 runserver 8888
IP만 할 경우 runserver 127.0.0.1
둘다 할 경우, IP:PORT
```

6. 테이블이 정상적으로 생성됬는지 Admin 페이지에서 확인하기

* 관리자\(슈퍼유저\) 생성하기

```text
python manage.py createsuperuser
```

* username, email, password 등록 후 아래의 사이트에서 확인 가능 
* http://IP:PORT/admin으로 접속
* 기존 미리 정의된 user와 groups 테이블이 보

