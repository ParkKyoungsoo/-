## Window 객체와 BOM

#### Window 객체

- **브라우저**의 요소들과 자바스크립트 엔진, 그리고 모든 변수를 담고 있는 객체



#### Window

인터넷 브라우저를 보면 **탭, 주소창, 즐겨찾기**가 있다. 그 다음부터는 웹사이트가 표시가 된다. 여기서 브라우저 **전체**를 담당하는게 **Window** 객체이고, **웹사이트만** 담당하는게 **Document** 객체라고 이해하면 된다. Document도 Window 객체 안에 들어있다. 



window 아래에는 대표적으로 **screen, location, history, document** 같은 객체들이 있다. 메소드는 **parseInt, isNaN** 등이 존재한다. 



일반적으로 만드는 변수(함수 안에서 선언한 변수 제외)도 모두 window 객체 안에 등록이 된다.

```js
var really = 'Really';
window.really;
```



실행결과

![image-20210104201915351](C:\Users\Gusangbuck\AppData\Roaming\Typora\typora-user-images\image-20210104201915351.png)





### window 객체의 대표적인 메소드와 속성

#### window.close()

현재의 창을 닫는다. window는 생략이 가능하기 때문에 `close();` 해도 된다. 하지만 다른 함수와 헷갈릴 수 있기 때문에 window를 붙여주는것도 괜찮다.



#### window.open()

새 창을 연다. 팝업 창의 형태로도 열 수 있고 새 탑으로도 열 수 있다. 첫 번째 인자로 주소를 받고, 두 번째 인자로 새탭으로 열지, 현재 탭에 열지를 설정할 수 있다. 세 번째 인자로 새 창에 대한 각종 설정을 전달 할 수 있다.

```js
window.open('https://www.naver.com'); // 새탭
window.open('https://www.naver.com','_self'); // 현재 탭
window.open('','','width=200, height=200') // 가로, 세로 200px의 팝업창
```

 

open 메소드는 더 많은 설정이 가능하다. 새로 연 창을 변수에 저장 할 수도 있다. 그리고 **변수.document.write**로 새창의 내용을 변경 할 수 있다.

```js
var popup = window.open('','','width=200, height=200');
popup.document.write('안녕하세요')
```

나중에 프로그래밍적으로 팝업 창을 닫으려면 저장해둔 변수에 `popup.close();`하면 된다. 



#### window.setTimeout(함수, 밀리초), window.setInterval(함수, 밀리초)

setTimeout은 지정한 초 뒤에 함수가 실행이 되고, setInterval 은 지정한 초 마다 반복된다.

```js
setTimeout(function() {
	alert('1초 뒤');
},1000);

setInterval(function() {
	console.log('1초 마다');
},1000); // 실행하지 말것
```



Timeout과 Interval을 중지하고 싶을때는 `clearTimeout`과 `clearInterval`을 사용하면 된다. 먼저 setTimeout, setInterval을 변수에 저장해놓고, 그 변수를 사용해 중지한다.

```js
var timer = setTimeout(function() {
	alert('5초 뒤');
},5000);

clearTimeout(timer);

var intervalTimer = setInterval(function() {
	console.log('1초 마다');
},1000);

clearInterval(intervalTimer);
```



#### window.getComputedStyle(태그)

태그의 스타일을 찾는 메소드이다. 현재 적용된 CSS속성 값을 알 수 있다.

```js
console.log(getComputedStyle(document.getElementById('태그명')));
```





다음은 **전역 객체** 중에 자주 쓰이는 것들이다. documents는 따로 **DOM**이라고 불리고 나머지는 브라우저에 대한 정보를 가지고 있어서 **BOM** 이라고 불린다.

### BOM(Browser Object Model)

#### navigator

브라우저나, 운영체제(OS)에 대한 정보가 있다(`navigator.userAgent`). userAgent 정보를 바탕으로 분석 사이트에서는 고객에 대한 정보를 분석한다. 만약 브라우저에 따라 다른 동작을 해야하거나 특정 브라우저인지를 체크할 때 navigator 객체를 쓰게 될 것이다.

```js
navigator.userAgent; 
// "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:84.0) Gecko/20100101 Firefox/84.0"
```

![image-20210104204451447](C:\Users\Gusangbuck\AppData\Roaming\Typora\typora-user-images\image-20210104204451447.png)





#### screen

화면에 대한 정보를 알려준다. 너비(width), 높이(height), 픽셀(pixelDepth), 컬러(colorDepth), 화면 방향(orientation), 작업표시줄을 제외한 너비와 높이(availWidth, availHeight) 등이 있다. 화면 크기에 따라 다른 동작을 하고 싶을 때 사용한다.

```js
screen.availHeight;
screen.availWidth;
screen.colorDepth;
```



#### location 

**location** 객체는 주소에 대한 정보를 알려주고(protocol, host, hostname, pathname, href, post, search, hash 속성을 이용), `location.reload()`로 새로고침도 가능하다. `location.replace()`는 현재 주소를 다른 주소로 교체한다.(다른 페이지로 이동하지만 이전 페이지 기록이 남지 않는다.)

```
location.host;
location.hostname; 
location.protocol;
location.href; 
location.pathname; 
```

[테스트 블로그](https://blog.naver.com/hapkiyusul/222190388022)

![image-20210104205308350](C:\Users\Gusangbuck\AppData\Roaming\Typora\typora-user-images\image-20210104205308350.png)



#### history

**history**는 앞으로 가기(`history.forward()`) 또는 `history.go(1)`), 뒤로가기(`history.back()` 또는 `history.go(-1)`) 같은 것을 관장한다. 히스토리간에 이동(`history.go(페이지수)`)할 수도 있다. `history.length`는 뒤로가기 할 수 있는 페이지의 개수를 의미한다.



`history.pushState(객체, 제목, 주소)` 와 `history.replaceState(객체, 제목, 주소)`는 **HTML5**에서 추가되었다. 페이지를 이동하지 않고 단순히 주소만 바꿔준다. 대신 **객체** 부분에 페이지에 대한 정보를 추가 할 수 있다. 이것은 SPA 를 만들 때 자주 이용된다.

```js
var state = { 'page_id': 1, 'user_id': 5 }; 
var title = 'Hello World'; 
var url = 'hello-world.html'; 
history.pushState(state, title, url);
```





출처 - [Window 객체와 BOM](https://www.zerocho.com/category/Javascript/post/573b321aa54b5e8427432946)

