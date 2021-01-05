## RESTfui API

### API

- Application Programming Interface : 어플리케이션 소프트웨어를 구축하고 통합하는 정의 및 프로토콜 세트

- 응용프로그램에서 사용할 수 있도록, 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스

- 때때로 정보 제공자와 정보 사용자 간의 계약으로 지칭되기도 함

- 소비자에게 필요한 콘텐츠(호출)와 생산자에게 필요한 콘텐츠(응답)을 구성한다.

  

### REST란?

- REpresentational State Transfer" 의 약자

  - 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든것을 의미

  - 자원(resource)의 표현(representation)에 의한 상태 전달

    - 자원 : 해당 소프트웨어가 관리하는 모든것

      ​	Ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등

    - 자원의 표현 : 그 자원을 표현하기 위한 이름

      ​	Ex) DB의 학생 정보가 자원일 때, 'Students'를 자원의 표현으로 정함

    - 상태 전달 : 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달하는 것을 뜻함

      ​	Ex) 프로그램이 학생 데이터를 요청하면 요청받은 시점의 상태(데이터)를 전달

      

- 일반적으로 REST 라고 하면 좁은 의미로 HTTP를 통해 CRUD를 실행하는 API

- 웹이 존재하는 자원(이미지, 동영상, DB)에 대해서 고유한 URI를 부여하고 활용하는 방법론을 의미

  (참고 URI : Uniform Resource Identifier / URL : Uniform Resource Locator / Uniform Resource Name)





### REST의 특징

- Uniform(유니폼 인터페이스)
  - 리소스에 상관없이 동일한 API 메소드를 갖는다. 즉, 이미지 리소스에 대한 처리와 문서 리소스에 대한 처리가 일관된 형태로 요청되어진다.
- Stateless(무상태성)
  - 서버는 각각의 요청을 완전히 별개의 것으로 인식하고 처리해야 하며, 이전 요청이 다음 요청의 처리에 연관 되어서는 안된다.
- Cacheable(캐시 가능)
  - HTTP 프로토콜을 사용하기 때문에 기존 웹 인프라를 그대로 사용가능하다. 즉 웹 브라우저에서 HTTP 캐시를 이용하는 등의 동작이 그대로 이용가능하다.
- Self-descriptiveness(자체 표현 구조)
  - REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다.

- Client-Server 구조
  - 클라이언트와 서버가 분리되어야 한다. ->  개발자가 클라이언트단을 수정할 때 서버 단의 DB디자인에 영향을 끼치지 않고 수정할 수 있어야 한다.
- 계층형 구조



### REST의 구조



Rest API는 다음과 같은 구성으로 이루어져 있다.

- Resource : URI는 정보의 자원을 표현해야 한다.
- 행위(Verb) : HTTP Method(GET, POST, DELETE, UPDATE)
- 표현 : 자원에 대한 행위는 HTTP Method로 표현한다.

  -> 이름이 상벽인 사용자를 생성한다  

​	Resource : 사용자

​	Method : 생성한다 

​	Representation : 이름이 상벽인 사용자

====================================

POST /member

{

​	"users" : {

​		"name" : "상벽"

​	}

}



ex) 

- 회원 정보 삭제 : DELETE /member/1
- 회원정보 조회 : GET /member/1
- 회원정보 추가 : POST /member





## RESTful API

REST API의 설계 의도를 정확하게 지켜주는 API들을  RESTful API라고 부른다.