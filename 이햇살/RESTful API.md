# RESTful API

## 1. REST

> 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것
>
> → HTTP URL을 통해 자원을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것

### 1.1 REST의 구성

- 자원(Resource) - URI
- 행위(Verb) - HTTP Method
- 표현(Representations)

### 1.2 REST 란?

- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST,GET,PUT,DELETE)를 통해 해당 자원에 대한 CRUD 연산을 적용하는 것
- REST 기반으로 서비스를 구현한 것이 REST API!
- 즉, 어떤 자원에 대해 CRUD 연산을 수행하기 위해 URI(Resource)로 요청을 보내는 것
- REST의 기본 원칙을 성실히 지킨 서비스 디자인은 'RESTful'하다고 표현할 수 있다.

### 1.3 REST 6가지 원칙

- uniform Interface (유니폼 인터페이스)
  - URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 의미
- Stateless (무상태성)
- Cacheable (캐시 가능)
- Client-Server 구조
- Hierarchical system (계층형)
- Code on demand

### 1.4 REST API 디자인 가이드

REST API 설계 시 가장 중요한 항목 2가지

1. URI는 정보의 자원을 표현해야 한다.
2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

> GET : GET를 통해 해당 리소스를 조회합니다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다.
> POST : POST를 통해 해당 URI를 요청하면 리소스를 생성한다.
> PUT : PUT를 통해 해당 리소스를 수정한다.
> DELETE : DELETE를 통해 해당 리소스를 삭제한다.

`→ URI는 자원을 표현하는 데에 집중하고 행위에 대한 정의는 HTTP METHOD를 통해 하는 것이 REST한 API를 설계하는 중심 규칙`

## 2. RESTful API

> 월드 와이드 웹과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어의 한 형식으로 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반에 대한 패턴
>
> → REST한 방식으로 프로그램간 정보 교환 등의 상호작용을 가능하게 하는 것이 RESTful API
>
> *API : 데이터와 기능의 집합을 제공하여 **컴퓨터 프로그램간 상호작용을 촉진**하며, **서로 정보를 교환가능하도록** 하는 것

### 2.1 RESTful API의 의미

- 리소스와 행위를 명시적이고 직관적으로 분리한
  - 리소스는 URI로 표현되는데 리소스가 가리키는 것은 명사로 표현되어야 함
  - 행위는 HTTP Method로 표현 / POST,GET,PUT,DELETE를 분명한 목적으로 사용

- Message는 Header와 Body를 명확하게 분리해서 사용
  - Entity에 대한 내용은 body에 담음
  - 애플리케이션 서버가 행동할 판단의 근거가 되는 컨트롤 정보인 API 버전 정보, 응답받고자 하는 MIME 타입 등은 header에 담음
  - header와 body는 http header와 http body로 나눌 수도 있고, http body에 들어가는 json 구조로 분리 가능

- API 버전 관리
  - API의 signature가 변경될 수 있음에 유의
  - 특정 API를 변경할 때는 반드시 하위호환성을 보장해야 함

- 서버와 클라이언트가 같은 방식을 사용해서 요청하도록 함
  - URI가 플랫폼 중립적

### 2.2 RESTful api가 왜 필요할까?

최근 서버 프로그램은 다양한 브라우저와 모바일 디바이스에서도 통신을 할 수 있어야 함!

`→ 이러한 통신을 가능하게 해주는 것이 RESTful API`

### 2.3 장단점

- 장점
  - 쉬운 Open API 제공
  - 멀티플랫폼 지원 및 연동 용이
  - 원하는 타입으로 데이터를 주고받을 수 있음
  - 기존 웹 인프라(HTTP) 그대로 사용 가능

- 단점
  - 사용가능한 메소드가 4가지 밖에 없음
  - 분산환경에는 부적합
  - HTTP 통신 모델에 대해서만 지원함

## 3. HTTP 응답 상태 코드

### 3.1 200 상태코드 (Success)

- 200 : OK. 클라이언트의 요청을 정상적으로 수행함
- 201 : Created. 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨 (POST를 통한 리소스 생성 작업 시, 또는 PUT)
- 202 : Accepted. 클라이언트의 요청은 정상적이나, 서버가 아직 요청을 완료하지 못함
- 204 : No Content. 클라이언트의 요청은 정상적이나 컨텐츠를 제공하지 않음

### 3.2 300 상태코드

- 301 : 클라이언트가 요청한 리소스에 대한 URI가 변경되었을 때 사용하는 응답코드
  (응답 시 Location header에 변경된 URI를 적어줘야 함)

### 3.3 400 상태코드 (Clients errors)

- 400 : Bad Request. 클라이언트의 요청이 부적절 할 경우 사용하는 응답 코드
- 401 : Unauthorized. 비인증. 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때 사용하는 응답 코드
- 403 : Forbidden. 비인가. 유저의 인증상태와 관계없이 클라이언트가 권한이 없기 때문에 작업을 진행할 수 없는 경우
- 404 : Not Found. 클라이언트가 요청한 자원이 존재하지 않음
- 405 : Method Not Allowed. 클라이언트의 요청이 허용되지 않는 메소드(HTTP Method)인 경우. 즉, 자원(URI)는 존재하지만 해당 자원이 지원하지 않는 메소드일 때 응답하는 상태 코드.
- 409 : Conflict. 클라이언트의 요청이 서버의 상태와 충돌이 발생한 경우

### 3.4 500 상태코드 (Server errors)

- 서버에 문제가 있을 경우 사용하는 응답 코드

---

참고

[[기술 면접 대비 CS] RESTful API](https://velog.io/@jsw7000/%EA%B8%B0%EC%88%A0-%EB%A9%B4%EC%A0%91-%EB%8C%80%EB%B9%84-CS-RESTful-API)

[[개발자 면접] RESTful API이란?](https://jinsangjin.tistory.com/75)