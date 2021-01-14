## CORS(Cross-Origin Resource Sharing: 교차 출처 리소스 공유)

웹 페이지 상의 제한된 리소스를 최초 자원이 서비스된 도메인 밖의 다른 도메인으로부터 요청할 수 있게 허용하는 구조

웹페이지는 교차 출처 이미지, 스타일시트, 스크립트, iframe, 동영상을 자유로이 임베디드 할 수 있다.

특정한 도메인 간(cross-domain) 요청, 특히 Ajax 요청은**SOP(Same-Origin Policy: 동일-출처 보안 정책)**에 의해 기본적으로 금지된다.



##### SOP(Same-Origin Policy)

- '같은 출처에서만 리소스를 공유할 수 있다.'라는 정책
- 'CORS 정책을 지킨 리소스 요청'은 예외적으로 허용이 된다.



##### 출처(Origin)

- `Scheme`, `Host`, `Port`
- `https://parkkyoungsoo.github.io/` -> Scheme : https / Host : parkkyoungsoo.github.io / Port : (생략)
- 포트번호가 생략되어있는 경우, 브라우저들의 독자적인 출처 비교 로직을 따라가게 된다.(익스플로러의 경우 포트번호를 완전히 무시)



HTTP 요청은 기본적으로 Cross-Site HTTP Requests가 가능하다. 다시말하면 `<img>`태그로 다른 도메인의 이미지 파일을 가져오거나, `<link>` 태그로 다른 도메인의 CSS를 가져오거나, `<script>`태그로 다른 도메인의 javascript 라이브러리를 가져오는것이 모두 가능하다. 하지만 `<script></script>`로 둘러쌓여 있는 **스크립트**에서 생성된 Cross-Site HTTP Requests는 **Same-Origin Policy**를 적용 받기 때문에 Cross-Site HTTP Requests가 불가능하다. 즉 **스킴, 호스트명, 포트**가 같아야 한다.



출처를 비교하는 로직이 서버에 구현된 스펙이 아니라 브라우저에 구현되어 있는 스펙이다.

CORS 정책을 위반하는 리소스 요청을 하더라도 해당 서버가 같은 출처에서 보낸 요청만 받겠다는 로직을 가지고 있는 경우가 아니라면 서버는 정상적으로 응답을 하고, 이후 브라우저가 이 응답을 분석해서 CORS 정책 위반이라고 판단되면 그 응답을 사용하지 않고 그냥 버린다.





## CORS 기본흐름

기본적으로 웹 클라이언트 어플리케이션이 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 보내게 되는데, 이때 브라우저 요청 헤더에 `Origin`이라는 필드에 요청을 보내는 출처를 함께 담아보낸다.

```http
Origin: https://parkkyoungsoo.github.io
```

 이후 서버가 이 요청에 대한 응답을 할 때 응답 헤더의 `Access-Control-Allow-Origin`이라는 값에 "이 리소스를 접근하는 것이 허용된 출처"를 내려주고, 이후 응답을 받은 브라우저는 자신이 보냈던 요청의 `Origin`과 서버가 보내준 응답의 `Access-Control-Allow-Origin`을 비교해본 후 응답이 유효한 응답인지 아닌지를 결정한다.



#### Preflight Request

- 요청을 한번에 보내지 않고 예비 요청과 본 요청으로 나누어서 서버로 전송
- 예비요청을 Preflight라고 함
- HTTP 메소드 중 OPTIONS<sup>*</sup> 메소드가 사용된다.

  

![cors-preflight](https://user-images.githubusercontent.com/44697835/104310994-f3edf880-5517-11eb-81e2-0ad529668eac.png)

<center>Preflight</center>

***** HTTP 메소드 종류

<table>
<tr>
    <th>HTTP Method
    </th>
    <th>전송형태
    </th>
    <th>설명
    </th>
</th>
<tr>
    <td>GET
	</td>
    <td>
        <pre>
GET [request-uri]?query_string HTTP/1.1
Host:[Hostname] 혹은 [IP]</pre>
	</td>
<td>요청받은 URI의 정보를 검색하여 응답한다.
</td>
</tr>
<tr>
    <td>HEAD
	</td>
    <td>
        <pre>
HEAD [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]</pre>
</td>
<td><pre>GET방식과 동일하지만, 응답에 BODY가 없고 응답코드와 HEAD만 응답한다.
웹서버 정보확인, 헬스체크, 버전확인, 최종 수정일자 확인등의 용도로 사용된다.</pre>
</td>
</tr>
<tr>
    <td>POST
	</td>
    <td>
        <pre>POST [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]
Content-Lenght:[Length in Bytes]
Content-Type:[Content Type]
[데이터]</pre>
	</td>
<td>요청된 자원을 생성(CREATE)한다. 새로 작성된 리로스인 경우 HTTP헤더 항목 Location: URI 주소를 포함하여 응답.
</td>
</tr>
<tr>
    <td>PUT
	</td>
    <td>
        <pre>
PUT [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]
Content-Lenght:[Length in Bytes]
Content-Type:[Content Type]
[데이터]</pre>
	</td>
<td>요청된 자원을 수정(UPDATE)한다. 내용 갱신을 위주로 Location: URI를 보내지 않아도 된다. 클라이언트측은 요청된 URI를 그대로 사용하는 것으로 간주함.
</td>
</tr>
<tr>
    <td>PATCH
	</td>
    <td>
        <pre>
PATCH [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]
Content-Lenght:[Length in Bytes]
Content-Type:[Content Type]
[데이터]</pre>
	</td>
<td>PUT과 유사하게 요청된 자원을 수정(UPDATE)할 때 사용한다. PUT의 경우 자원 전체를 갱신하는 의미지만, PATCH는 해당자원의 일부를 교체하는 의미로 사용.
</td>
</tr>
<tr>
    <td>DELETE
	</td>
    <td>
        <pre>
DELETE [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]</pre>
	</td>
<td>요청된 지원을 삭제할 것을 요청함.(안전성 문제로 대부분의 서버에서 비활성)
</td>
</tr>
<tr>
    <td>CONNECT
	</td>
    <td>
        <pre>
CONNECT [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]</pre>
	</td>
<td>동적으로 터널 모드를 교환, 프락시 기능을 요청시 사용.
</td>
</tr>
<tr>
    <td>TRACE
	</td>
    <td>
        <pre>
TRACE [request-uri] HTTP/ 1.1
Host: [Hostname] 혹은 [IP]</pre>
	</td>
<td>원격지 서버에 루프백 메시지 호출하기 위해 테스트용으로 사용.
</td>
</tr>
<tr>
    <td>OPTIONS
	</td>
    <td>
        <pre>
OPTIONS [request-uri] HTTP/ 1.1
Host: [Hostname] 혹은 [IP]</pre>
	</td>
<td>웹서섭에서 지원되는 메소드의 종류를 확인할 경우 사용.
</td>
</tr>
</table>







#### Simple Request

예비요청을 보내지 않고 바로 서버에게 본 요청을 보낸 후, 서버가 이에 대한 응답의 헤더에 `Access-Control-Allow-Origin`과 같은 값을 보내주면 그때 브라우저가 CORS 정책 위반 여부를 검사하는 방식. Preflight 와 예비요청의 존재 유무만 다르다.



![simple-request](https://user-images.githubusercontent.com/44697835/104311352-6bbc2300-5518-11eb-9c91-e71f8f258828.png)

<center>Simple Request</center>



특정 조건을 만족하는 경우에만 예비요청을 생략할 수 있다.

1. 요청의 메소드는 `GET`, `HEAD`, `POST`중 하나여야 한다.
2. `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, `DPR`, `Downlink`, `Save-Data`, `Viewport-Width`, `Width`를 제외한 헤더를 사용하면 안된다.
3. 만약 `Content-Type`를 사용하는 경우에는 `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain`만 허용된다.





#### Credentialed Request

- 인증된 요청을 사용하는 방법
- 다른 출처간 통신에서 좀 더 보안을 강화하고 싶을 때 사용하는 방법

기본적으로 브라우저가 제공하는 비동기 리소스 요청 API인 `XMLHttpRequest`객체나 `fetch` API는 별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 않는다. 이때 요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 바로`credentials`옵션이다.

| 옵션 값              | 설명                                           |
| -------------------- | ---------------------------------------------- |
| same-origin (기본값) | 같은 출처 간 요청에만 인증 정보를 담을 수 있다 |
| include              | 모든 요청에 인증 정보를 담을 수 있다           |
| omit                 | 모든 요청에 인증 정보를 담지 않는다            |





## CORS 해결 방법

#### Access-Control-Allow-Origin 세팅

가장 대표적인 방법은 서버에 `Access-Control-Allow-Origin`헤더에 알맞은 값을 세팅해주는것. 와일드카드인 `*`를 사용하여 세팅하면 모든 요청을 허락하는 것이므로 귀찮더라도 `Access-Control-Allow-Origin: 사이트 주소`를 하는것이 좋다.



#### Webpack Dev Server로 리버스 프록싱하기





출처 - [CORS는 왜 이렇게 우리를 힘들게 하는걸까?](https://evan-moon.github.io/2020/05/21/about-cors/#cors%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%82%B4%EC%9A%A9) , [CORS](https://brownbears.tistory.com/336)