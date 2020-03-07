# Web Basic

## BASIC for Web

웹 프로그래밍 : HTTP\(S\) 프로토콜로 통신하는 클라이언트와 서버 개발

**웹 클라이언트 종류**

* 웹 브라우저를 사용하여 요청
* 리눅스 curl 명령어와 같이
* Telnet 이용
* 직접 만든 클라이언트

HTTP  Protocol : Hypertext + multimedia와 같이 모든 종류의 데이터 전송 가능 프로토콜

* HTTP 메시지 구조 : Start Line\(Request/Status\) \| Header \| Blank Line \| Body
* URI\(Uniform Resource Identifier\) : URL\(Uniform Resource Locator\) + URN\(Uniform Resource Name\)을 포함하는 넓은 의미

| Method | Meaning | CRUD mapping |
| :--- | :--- | :--- |
| GET | 리소스 취득 | Read\(조회\) |
| POST | 리소스 생성, 리소스 데이터 추가 | Create\(생성\) |
| PUT | 리소스 변경 | Update\(변경\) |
| DELETE | 리소스 삭제 | Delete\(삭제\) |
| HEAD | 리소스의 헤더\(메타데이터\) 취득 |  |
| OPTIONS | 리소스가 서포트하는 메소드 취득 |  |
| TRACE | 루프백 시험에 사용 |  |
| CONNECT | 프록시 동작의 터널 접속으로 변경 |  |

GET과 POST의 경우 데이터를 전송하는 방식이 차이가 있음. GET은 주소창에도 보여 공개적이며, 주소길이가 한정적이어서 데이터 전송 길이에도 한계가 있음. 그래서 POST를 통해 파라미터를 전달함.

**상태코드 분류**

| 메소드 | 의미 | CRUD |
| :--- | :--- | :--- |
| 1xx | 정보 제공 | 임시적인 응답. 현재 클라이언트의 요청까지 처리되었으니 계속 진행하라는 의미. HTTP 1.1버전부터 추가 |
| 2xx | 성공 | 클라이언트의 요청이 서버에서 성공적으로 처리됨. |
| 3xx | 리다이렉션 | 완전한 처리를 위해 추가 동작 필요. 주로 서버의 주소 또는 요청한 URI의 웹 문서가 이동되어 다시 시도하라는 의미. |
| 4xx | 클라이언트 에러 | 없는 페이지를 요청하는 것처럼 잘못된 요청 메시지가 온 경우. |
| 5xx | 서버 에 | 서버 측 무제로 메시지 처리가 잘못된 경우. |

**URL 설계**

{% embed url="http://www.example.com:80/services?category=2&kind-patents\#n10" %}

* http:// : URL 스킴. URL에 사용된 프로토콜을 의미
* www~.com : 호스트명. 웹 서버의 호스트명. 도메인명 또는 IP주소
* :80 : 포트번호. 웹 서버 내의 서비스 포트번호. 생략하면 디폴트로 http는 80, https는 443을 사용.
* service : 경로. 파일이나 애플리케이션 경로.
* ?~patents : 쿼리스트링. &로 구분된 이름=값의 쌍으로 표현.
* \#n10 : 프라그먼트. 문서 내의 앵커 등 조각을 지정.

**RPC\(Remote Procedure Call\)** : URL 설계와 API 설계를 동일하게 고려하여 URL 경로를 API 함수로, 쿼리 파라미터를 함수의 인자로 사용하는 방법.

**REST\(Representational State Transfer\)** : URL을 통해 웹 서버의 특정 리소스를 표현한다음 개념. GET, POST, PUT, DELETE 등의 명령어로 이용함.

Search Engine Friendly or User Friendly URL : 기존 URL에서 &, ?, = 과 같이 프로그래밍에 사용되는 부분을 제거하여 보기 편하게 변경한 방식.

**웹 서버** : 웹 클라이언트의 요청을 받아서 요청을 처리하고, 그 결과를 웹 클라이언트에 응답. 주로 정적 페이지 HTML, 이미지, CSS 등을 웹 클라이언트에게 제공할 때 사용. \(Apache httpd, Nginx, etc\)

**웹 애플리케이션 서버** : 웹 서버로부터 동적 페이지 요청을 받아 요청을 처리하고 그 결과를 웹 서버로 반환. \(Apache Tomcat, JBoss, etc\)

