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

### 장고 설치

 Python 사용 가능 환경에서 pip install Django 로 설치.



