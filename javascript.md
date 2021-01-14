## javascript

##### 문자열 자료형 입력

- `prompt()`

  

##### 식별자에 값을 넣을 때 사용하는 키워드

| 키워드 | 구분 | 선언위치    | 재선언 |
| ------ | ---- | ----------- | ------ |
| var    | 변수 | 전역 스코프 | 가능   |
| let    | 변수 | 해당 스코프 | 불가능 |
| const  | 상수 | 해당 스코프 | 불가능 |



```js
for(var i = 0; i < 4; i++) {
	setTimeout(function() {
		alert(i);
	},1000 * i);
}
//////////////////////////////////////////////////////
for(var i = 0; i < 4; i++) {
	setTimeout(() => {
		alert(i);
	},1000 * i);
}
```



```js
for(var i = 0; i < 4; i++) {
	(function(i) {
    	setTimeout(function() {
			alert(i);
		},1000 * i)
	})(i);
}
/////////////////////////////////////////////////////
for(var i = 0; i < 4; i++) {
	((i)=> {
		setTimeout(() => {
			alert(i);
		},1000 * i);
    })(i);
}
```





```js
for(let i = 0; i < 4; i++) {
	setTimeout(function() {
		alert(i);
	},1000 * i);
}

for(let i = 0; i < 4; i++) {
	setTimeout(() => {
		alert(i);
	},1000 * i);
}
```





##### 짧은 조건문

다음 논리합 연산자를 사용한 표현식은 뒤에 어떠한 값이 들어가도 항상 참이다.

```js
true || value
```

js는 이처럼 참이 확실할 때 추가 연산을 진행하지 않는다. 즉, 논리할 연산자의 좌변이 참이면 우변을 실행하지 않는다.

`(<bool 표현식>) || (<bool 표현식이 거짓일 때 실행할 문장>)`

`(<bool 표현식>) && (<bool 표현식이 참일 때 실행할 문장>)`

```js
var input = Number(prompt('숫자를 입력하세요'));

input % 2 == 0 || alert('홀수입니다.');
input % 2 == 0 && alert('짝수입니다.'); 
```



##### for of 반복문

for in 반복분

```js
var array = [1,2,3,4,5];
for(var i in array) {
	alert(i + '번째 요소는 ' + array[i] + '입니다.');
}
```



for of 반복분

```js
for(const element of [1,2,3,4,5]) {
	alert(`요소는 ${element}입니다.`);
}
```

```js
{
    let i = 0;
    for(const element of [1,2,3,4,5]) {
        alert(`${i}번째 요소는 ${element}입니다.`);
        i++;
    }
}
```





##### 익명함수와 선언적 함수

```js
// 익명함수
var func1 = function() {
	alert('hello');
}

// 선언적 함수
function func2() {
	alert('hi');
}
```



```js
var hello = function() {
	alert('hello!');
}

function hello() {
	alert('Hi!!');
}

hello();
```



##### 가변 인자 함수

```js
function sumAll() {
	alert(typeof arguments + ' : ' + arguments.length);
    
    var output = 0;
    for(var i = 0; i < arguments.length; i++) {
		output += arguments[i];
	}
    return output;
}

alert(sumAll(1,2,3,4,5,6,7,8,9));
```





#### 클로저

```js
function test(name) {
	var output = 'Hello ' + name + '..!!';
	return function() {
		alert(output);
	}
}

test('javascript')();
```

변수 output은 지역 변수이므로 함수가 종료될 때 사라져야 한다. 그러나 해당 변수가 이후에도 활용될 가능성이 있으므로 자바스크립트는 변수를 제거하지 않고 남겨둔다. 따라서 위 코드는 실행된다.



클로저의 정의들

- 위 처럼 지역변수를 남겨두는 현상
- test() 내부의 변수들이 살아있으는 것이므로 test() 함수로 생성된 공간 자체
- 리턴한 함수 자체
- 살아남은 지역 변수 output



추가로 지역 변수 output을 남겨둔다고 외부에서 마음대로 사용할 수 있는것은 아니다. 반드시 리턴된 클로저 함수를 사용해야 지역 변수 output을 사용할 수 있다. 클로저 함수로 인해 남은 지역변수는 클로저 함수 각각의 고유한 변수이다.

```js
function test(name) {
	var output = 'Hello ' + name + '..!!';
	return function() {
		alert(output);
	}
}

var test_1 = test('Web');
var test_2 = test('javascript');

test_1();
test_2();
```





##### 코드실행 함수

| 함수 이름    | 설명                          |
| ------------ | ----------------------------- |
| eval(string) | string을 자바스크립트 코드로 실행한다. |

```js
var willEval = '';
willEval += 'var number = 10;';
willEval += 'alert(number);';

eval(willEval);

alert(number);
```



##### 자바스크립트의 실행 순서

```javascript
alert('A');
setTimeout(() => {
    alert('B');
},0);
alert('C');
```

A -> C -> B 순으로 실행

자바스크립트의 함수 중에는 웹 브라우저에 처리를 부탁하는 함수가 있다. 대표적으로 Timeout 함수와 웹 요청 관련 함수가 있으며, 웹 브라우저가 처리하고 처리가 완료되었다는 것을 자바스크립트에서 알려준다.

이러한 함수는 현재 실행 중인 다른 코드의 실행이 끝나기 전에는 실행되지 않는다. 

```javascript
setTimeout(() => {
	alert('Time out...');
},0);
while(true) { }
```




##### 기본 매개변수

매개변수를 입력하지 않았을 때, 매개변수를 강제로 초기화 하는것

```js
function test(a,b,c) {
	if(!b) { b = 52;}
    if(!c) { c = 273;}
    
    alert(a + ' : ' + b + ' : ' + c);
}

test(1,2);
```

```js
function test(a,b,c) {
	b = b||52;
    c = c||273;
    
    alert(a + ' : ' + b + ' : ' + c);
}

test(1,2);
```



ECMAScript 6

```js
function test(a,b = 52,c = 273) {
    alert(a + ' : ' + b + ' : ' + c);
}

test(1,2);
```



##### 화살표 함수 - ECMAScript 6 

기존함수와 차이가 아예 없는건 아니다.

내부에서 사용하는 this 키워드의 의미가 다르다.

- 익명함수 : 함수 자체에 바인딩되어 있는 객체(window 객체 또는 프로토타입 객체가 될 수도 있다.)
- 화살표 함수 : 전역 객체(웹 브라우저 환경에서는 window 객체)