## SPA(Single Page Application)

- 서버로부터 새로운 페이지를 불러오지 않고 현재의 페이지를 동적으로 다시 작성함으로써 사용자와 소통하는 웹 애플리케이션이나 웹사이트를 지칭

- **네이티브 앱**<sup>*</sup> 과 유사한 사용자 경험을 제공할 수 있다
- 기본적으로 단일 페이지로 구성

<span style="font-size:12px">네이티브 앱 : 흔히 말하는 어플리케이션, 모바일에 최적화 되어있는 어플리케이션</span>



<center>전통적인 웹 어플리케이션 방식과 SPA 방식 비교</center>

![m blog naver com 643 spa1](https://user-images.githubusercontent.com/44697835/102209526-3b329a80-3f14-11eb-9381-aa25b30bc2a4.png)



![m blog naver com 619 spa2](https://user-images.githubusercontent.com/44697835/102209523-3a016d80-3f14-11eb-8b68-642214a21a62.png)





## SPA 특징

#### 라우팅(Routing)

- 출발지에서 목적지까지 경로를 결정하는 기능
- 어플리케이션의 라우팅은 사용자가 테스크를 수행하기 위해 어떤 화면(view)에서 다른 화면으로 화면을 전환하는 네비게이션을 관리하기 위한 기능을 의미
- 사용자가 요청한 URL 또는 이벤트를 해석하고 새로운 페이지로 전환하기 위한 데이터를 취득하기 위해 서버에 필요한 데이터를 요청하고 화면을 전환하는 일련의 행위를 말한다.



라우팅을 백단 서버가 아닌 브라우저 단에서 구현해야 하는것이 SPA개발의 핵심  ->  요청 URL에 따라 브라우저에서 돔(DOM)을 변경하는 방식





## CSR(Client Side Rendering)



![1_c955FMt4om-cyNU9d11OiQ](https://user-images.githubusercontent.com/44697835/102214622-e561f080-3f1b-11eb-80f2-64dbbb0af312.png)

<center> CSR은 웹 서버에 요청할떈 데이터가 없는 문서를 반환한다. </center>





![1_nmfJo2FUGSF9aL45JwG-Lg](https://user-images.githubusercontent.com/44697835/102214624-e5fa8700-3f1b-11eb-89ab-16b1c1e5e8aa.png)

<center>HTML 및 Static 파일들이 로드 되면서, 데이터 또한 서버에 요청하고 그것이 화면상에 나타나게 된다.</center>



데이터가 없는 빈 깡통인 HTML(이외에 static 파일들)만 받아오고, 데이터는 깡통인 문서와 여러 static 파일들이 로드된 이후에 요청해서 받아오는 방식으로 진행된다.

브라우저가 자바스크립트를 받아와 동적으로 렌더링한다. 첫 로딩시에 필요한 파일크기는 더 크지만(HTML, CSS, javascript, 그외 리소스 모두 포함) 다 받기만 하면 동적으로 빠르게 렌더링 하기 때문에 사용자가 느끼는 UX에 유리하다. SSR과 다르게 하나의 HTML 파일로 모든 페이지를 구성하기 때문에 meta 태그 정의에 약점이 있다.





## SSR(Server Side Rendering)



![1_fuDcEQEaNQXEg4S78n-lUQ](https://user-images.githubusercontent.com/44697835/102214871-3e318900-3f1c-11eb-8ec4-82965a1a1471.png)

<center>데이터가 포함된 HTML을 받아온다.</center>



데이터까지 전부 삽입하여 완성된 HTML을 받아온다.

서버에서 정적인 페이지로 렌더링 되어 사용자아게 내려오는 것을의미한다. 따라서 초기 로딩속도가 빠르고(js 파일을 다운로드하고 적용하기 전에 이미 브라우저에서 보여지기 떄문) SEO에 사용되는 meta 태그들이 미리 정의되어 SEO에 유리하다.





## SPA와 CSR은 같다?

SPA는 서버로부터 처음에만 페이지를 받아오고 이후에는 동적으로 DOM을 구성하여 렌더링 되는 화면이 바뀌게 한다. 

여기서 ''동적으로 DOM을 구성하여 렌더링 되는 화면이 바뀌게 한다." 부분이 CSR이다. 

SPA는 처음에만 페이지를 받아오고 이후에는 받아오지 않는데 이럼에도 데이터가 수정되고 조회되게 하고 싶어서 CSR이란 '**"방식"**을 채택





## SEO(Search Engine Optimization)

#### 검색엔진 최적화 

- 검색엔진이 자료를 수집하고 순위를 매기는 방식에 맞게 웹 페이지를 구성하여 검색 결과의 상위에 나올 수 있도록 하는 작업을의미



#### SPA에서 SEO

일반적으로 검색 엔진의 크롤러들은 데이터를 긁어올 떄 웹 페이지의 javascript를 해석해 노출시키기 떄문에 크롤링을 할 수 없는 시점에서는 검색 엔진이 데이터를 노출시키지 않는 것이고, 이는 상대적으로 우리의 서비스가 검색 엔진 서비스에 노출되는 것이 줄어듦을 의미한다.

따라서 CSR을 사용하면 View를 생성하기 위해서  javascript가 필요하고(그 전까지는 빈 페이지이기 때문에 View가 완성되지 않아서), View를 생성하기 전까지는 검색 엔진 크롤러의 데이터 수집이 제한적이기 때문에 상대적으로 검색 엔진이 이해하는 정보가 부족해 SEO에 유리하지 않게 된다.

반대로 전통적인 SSR은 View 를 서버에서 렌더링해 제공하기 때문에(View를 먼저 그리기 때문에) 상대적으로 SEO에 유리해져 사용자 유입이 많을 것이다.



SSR과 CSR 두가지 렌더링 방법을 적절하게 사용하여 첫 번째 페이지 로딩에서는  SSR을 사용하고, 그 후 모든 페이지 로드에는 CSR 렌더링을 활용하는 방법이 많이 사용된다.



```
<html>
<head>
  <title>Single Page Application</title>
  <link rel="stylesheet" href="app.css" type="text/css">
</head>
<body>
  <div id="app"></div>
  <script src="app.js"></script>
</body>
</html>
```







출처 
- [아하 프론트 개발기(1) — SPA와 SSR의 장단점 그리고 Nuxt.js](https://medium.com/aha-official/%EC%95%84%ED%95%98-%ED%94%84%EB%A1%A0%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EA%B8%B0-1-spa%EC%99%80-ssr%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90-%EA%B7%B8%EB%A6%AC%EA%B3%A0-nuxt-js-cafdc3ac2053)
- [MPA와 SPA, SSR과 CSR, 그리고 SEO](https://devowen.com/309)
- [CSR, SSR, SPA, MPA?](https://medium.com/%EC%95%84%EB%AA%BD%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4/csr-ssr-spa-mpa-ede7b55c5f6f)


