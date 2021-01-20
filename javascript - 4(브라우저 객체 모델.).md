## 브라우저 객체 모델

브라우저 객체 모델(Browser Object Model)

- 웹 브라우저와 관련된 객체의 집합

- 대표 객체 : `window`, `location`, `navigator`, `history`, `screen`, `document`



| 객체명    | 역할                      |
| --------- | ------------------------- |
| screen    | 화면 전체와 관련된 객체   |
| navigator | 웹 브라우저와 관련된 객체 |
| location  | 주소와 관련된 객체        |
| history   | 기록과 관련된 객체        |
| documents | HTML 문서와 관련된 객체   |



##### window 객체

- 자바스크립트의 브라우저 기반 최상위 객체



##### 새로운 window  객체 생성

- `open(URL, name, feature, replace);` : 새로운 window 객체를 생성한다.

feature

| 옵션 이름 | 설명                     | 입력할 수 있는 값 |
| --------- | ------------------------ | ----------------- |
| height    | 새 윈도우의 높이         | 픽셀 값           |
| width     | 새 윈도우의 너비         | 픽셀 값           |
| location  | 주소 입력창의 유무       | yes, no, 1, 0     |
| menubar   | 메뉴의 유무              | yes, no, 1, 0     |
| resizable | 화면 크기 조절 가능 유무 | yes, no, 1, 0     |
| status    | 상태 표시줄의 유무       | yes, no, 1, 0     |
| toolbar   |                          | yes, no, 1, 0     |

![image-20210119191104510](C:\Users\Gusangbuck\AppData\Roaming\Typora\typora-user-images\image-20210119191104510.png)

```js
var child = window.open('','','width=300, height=200');

if(child) {
    child.document.write('<h1>From Parent Window</h1>');
} else {
    alert('팝업 차단을 해제해주세요.');
}
```



##### window 객체의 기본 메소드

| 메소드 이름   | 설명                                        |
| ------------- | ------------------------------------------- |
| moveBy(x,y)   | 윈도우의 위치를 상대적으로 이동한다.        |
| moveTo(x,y)   | 윈도우의 위치를 절대적으로 이동한다.        |
| resizeBy(x,y) | 윈도우의 크기를 상대적으로 지정한다.        |
| resizeTo(x,y) | 윈도우의 크기를 절대적으로 지정한다.        |
| scrollBy(x,y) | 윈도우 스크롤의 위치를 상대적으로 이동한다. |
| scrollTo(x,y) | 윈도우 스크롤의 위치를 절대적으로 이동한다. |
| focus()       | 윈도우에 초첨을 맞춘다.                     |
| blur()        | 윈도우에 맞춘 초점을 제거한다.              |
| close()       | 윈도우를 닫는다.                            |

```js
var child = window.open('','','width=300, height=200');

child.moveTo(0,0);

setInterval(() => {
	child.moveBy(10,10);
},1000);
```

```js
var child = window.open('', '', 'width=300, height=200');

if(child) {
    child.document.write('<div id="myPage" onmouseover="moveTo(Math.floor(Math.random() * 1920) + 1,Math.floor(Math.random() * 1080) + 1);">안녕</div>');
} else {
    alert('팝업 차단을 해제해주세요.');
}
```



##### screen 객체

- 브라우저의 화면이 아니라 운영체제 화면의 속성을 갖는 객체

| 속성 이름   | 설명                           |
| ----------- | ------------------------------ |
| width       | 화면의 너비                    |
| height      | 화면의 높이                    |
| avaliWidth  | 실제 화면에서 사용 가능한 너비 |
| availHeight | 실제 화면에서 사용 가능한 높이 |
| colorDepth  | 사용 가능한 색상 수            |
| pixeDepth   | 한 픽셀당 비트 수              |



```js
var child = window.open('','','width=300, height=200');
var width = screen.width;
var height = screen.height;

child.moveTo(0,0);
child.resizeTo(width, height);

setInterval(() => {
	child.resizeBy(-20,-20);
    child.moveBy(10,10);
},1000);
```



##### location 객체

- 웹 브라우저의 주소 표시줄과 관련된 객체
- 프로토콜의 종류, 호스트 이름, 문서 위치 등의 정보가 있다.

location 객체의 속성

| 속성 이름 | 설명                      | 예                     |
| --------- | ------------------------- | ---------------------- |
| href      | 문서의 URL 주소           |                        |
| host      | 호스트 이름과 포트 번호   | localhost:8080         |
| hostname  | 호스트 이름               | localhost              |
| port      | 포트 번호                 | 8080                   |
| pathname  | 디렉토리 경로             | /Project/Location.html |
| hash      | 앵커 이름(#~)<sup>*</sup> | #beta                  |
| search    | 요청 매개변수             | ?param=10              |
| protocol  | 프로토콜 종류             | http:                  |

* 앵커(Anchor) : 현재 웹 페이지 안의 위치를 id값으로 표시. 페이지 내 해당 위치로 이동하는데 사용



location 객체

| 속성 이름     | 설명                  |
| ------------- | --------------------- |
| assign(link)  | 현재 위치를 이동한다. |
| reload()      | 새로고침              |
| replace(link) | 현재 위치를 이동한다. |

replace() 메소드는 뒤로가기 버튼을 사용할 수 없다.



##### navigator 객체

- navigator 객체는 웹 페이지를 실행하고 있는 브라우저에 대한 정보가 있다.

| 속성 이름   | 설명                             |
| ----------- | -------------------------------- |
| appCodeName | 브라우저의 코드 이름             |
| appName     | 브라우저의 이름                  |
| appVersion  | 브라우저의 버전                  |
| platform    | 사용 중인 운영체제의 시스템 환경 |
| userAgent   | 웹 브라우저의 전체 정보          |



##### window 객체의 onload 이벤트 속성

```js
window.onload = function() {

};
```

- 문서 객체의 속성 중 `on`으로 시작하는 속성을 이벤트 속성이라 부른다.
- 함수를 할당해야 한다.
- 위 코드는 <u>window 객체 로드가 완료</u><sup>?</sup>되고 자동으로 할당한 함수를 실행한다.

**?** window 객체 로드가 완료될 때 : HTML 페이지에 존재하는 모든 태그가 화면에 올라가는 순간

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        window.onload = () => {
            alert('Process - 0');
        }
    </script>
    <h1>Process - 1</h1>
    <script>alert('Process - 1');</script>
    <h2>Porcess - 2</h2>
    <script>alert('Process - 2');</script>
    <h3>Process - 3</h3>
    <script>alert('Process - 3');</script>
</body>

</html>
```



