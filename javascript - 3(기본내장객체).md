## 기본 내장 객체

##### 기본 자료형과 객체의 차이점

- 기본 자료형 : 숫자, 문자열, bool



```js
var primitiveNumber = 273;
var objectNumber = new Number(273);

var output = '';
output += typeof primitiveNumber + ' : ' + primitiveNumber + '\n';
output += typeof objectNumber + ' : ' + objectNumber + '\n';
alert(output);
```



속성과 메서드는 객체가 가질 수 있는것

![image-20210118192038982](C:\Users\Gusangbuck\AppData\Roaming\Typora\typora-user-images\image-20210118192038982.png)

기본 자료형에도 속성과 메서드가 있다. 기본 자료형의 속성이나 메서드를 사용하면 기본 자료형이 자동으로 객체로 변환된다.

기본 자료형은 객체가 아니므로 속성과 메서드를 추가 할 수 없다.

```js
var primitiveNumber = 273;

primitiveNumber.method = function() {
	return 'Primitive Method';
}

var output = primitiveNumber.method() + '\n';
alert(output);
// 에러
```



기본 자료형은 속성이나 메서드를 추가 할 수 없다? 

```js
var primitiveNumber = 273;
var objectNumber = new Number(273);

Number.prototype.method = function() {
	return 'Method on Prototype';
}

var output = '';
output += primitiveNumber.method() + '\n';
output += objectNumber.method() + '\n';
alert(output);
```





##### Object 객체

- 자바스크립트의 최상위 객체



생성 방법

```js
var object = {};
var object = new Object();
```



| 메서드 이름                | 설명                                              |
| -------------------------- | ------------------------------------------------- |
| constructor()              | 객체의 생성자 함수를 나타낸다.                    |
| hasOwnProperty(name)       | 객체가 name 속성이 있는지 확인한다.               |
| isPrototypeof(object)      | 객체가 object의 프로토타입인지 검사한다.          |
| propertyIsEnumerable(name) | 반복문으로 열거할 수 있는지 확인한다.             |
| toLocaleString()           | 객체를 호스트 환경에 맞는 언어의 문자열로 바꾼다. |
| toString()                 | 객체를 문자열로 바꾼다.                           |
| valeuOf()                  | 객체의 값을 나타낸다.                             |



object 객체에 있는 constructor() 메서드는 객체의 생성자 함수를 의미하며, 자료형을 검사 할 때 유용하게 사용할 수 있다.

```js
var numberFromLiteral = 273;
var NumberFromObject = new Number(273);

alert(typeof numberFromLiteral);
alert(typeof NumberFromObject);
alert(numberFromLiteral.constructor == Number);
alert(NumberFromObject.constructor == Number);
```



##### String 객체의 메서드

| 메서드 이름                         | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| charAt(position)                    | position에 위치하는 문자를 리턴한다.                         |
| charCodeAt(position)                | position에 위치하는 문자의 유니코드 번호를 리턴한다.         |
| concat(args)                        | 매개변수로 입력한 문자열을 이어서 리턴한다.                  |
| indexOf(searchString, position)     | 앞에서부터 일치하는 문자열의 위치를 리턴한다.                |
| lastIndexOf(searchString, position) | 뒤에서부터 일치하는 문자열의 위치를 리턴한다.                |
| match(regExp)                       | 문자열 안에 regExp가 있는지 확인한다.                        |
| replace(regExp, replacement)        | regExp를 replacement로 바꾼 뒤 리턴한다.                     |
| search(regExp)                      | regExp와 일치하는 문자열의 위치를 리턴한다.                  |
| slice(start, end)                   | 특정 위치의 문자열을 추출해 리턴한다.                        |
| split(separator, limit)             | separator로 문자열을 잘라서 배열을 리턴한다. (limit: 분할 최대 개수) |
| substr(start, count)                | start부터 count만큼 문자열을 잘라서 리턴한다.                |
| subString(start, end)               | start부터 end까지 문자열을 잘라서 리턴한다.                  |
| toLowerCase()                       | 문자열을 소문자로 바꾸어 리턴한다.                           |
| toUpperCase()                       | 문자열을 대문자로 바꾸어 리턴한다.                           |



String 객체의 메서드는  자기 자신을 변화시키지 않고 리턴한다.

```js
var string = 'hello hello';

string.toUpperCase();
alert(string);

string = string.toUpperCase();
alert(string);
```





##### Array 객체

Array 객체 생성

```js
var array1 = [52, 273, 103, 57, 32];
var array2 = new Array();
var array3 = new Array(10);
var array4 = new Array(52,273, 103, 57l 32);
```



메서드

| 메서드 이름 | 설명                                                       |
| ----------- | ---------------------------------------------------------- |
| concat()    | 매개변수로 입력한 배열의 요소를 모두 합쳐 배열을 리턴한다. |
| join()      | 배열 안의 모든 요소를 문자열로 만들어 리턴한다.            |
| pop()*      | 배열의 마지막 요소를 제거하고 리턴한다.                    |
| push()*     | 배열의 마지막 부분에 새로운 요소를 추가한다.               |
| reverse()*  | 배열의 요소 순서를 뒤집는다.                               |
| slice()*    | 요서의 지정한 부분을 리턴한다.                             |
| sort()*     | 배열의 요소를 정렬한다.                                    |
| splice()*   | 요소의 지정한 부분을 삭제하고 삭제한 요소를 리턴한다.      |

```js
var array = [52, 273, 103, 32];
// sort 는 문자열 오름차순 정렬
array.sort();

alert(array);
```



오름차순, 내림차순 정렬

```js
var array = [52, 273, 103, 32];
array.sort(function(left, right) {
   return left - right; 
});

alert(array);

array.sort(function(left, right) {
   return right - left; 
});

alert(array);
```



요소제거

`배열.splice(start, deleteCount, item1, item2,....)`의 사용법 

```js
var array = [1,2,3,4,5,6,7,8,9];

// 1번째 요소 부터 이후 모든 요소 삭제
array.splice(1);

// 1번째 요소부터 1개 삭제
array.splice(1,1);

// 1번째 요소부터 2개 삭제 후 요소 추가
array.splice(1,2,11);

Array.prototype.remove = function(index) {
    this.splice(index,1);
}

array.remove(2);

alert(array);
```





##### ECMAScript 5 Array 객체

반복 메소드 - forEach()

```js
var array = [1,2,3,4,5,6,7,8,9,10];

var sum = 0;
var output = '';
array.forEach(function(element, index, array) {
	sum += element;
    output += index + ' : ' + element + ' -> ' + sum + '\n';
});

alert(output);
```



반복 메소드 - map() : 배열의 각 요소를 변경해 새로운 배열을 리턴하는 메소드

```js
var array = [1,2,3,4,5,6,7,8,9,10];

var output = array.map(function(element) {
    return element * element;
});

alert(output);
```



조건 메소드

| 메소드 이름 | 설명                                                       |
| ----------- | ---------------------------------------------------------- |
| filter()    | 특정 조건을 만족하는 요소를 추출해 새로운 배열을 만든다.   |
| every()     | 배열의 요소가 특정 조건을 모두 만족하는지 확인한다.        |
| some()      | 배열의 요소가 특정 조건을 적어도 하나 만족하는지 확인한다. |

```js
var array = [1,2,3,4,5,6,7,8,9,10];

array = array.filter(function(element, index, array) {
   return element <= 5; 
});

alert(array);
```



연산 메소드

| 메소드 이름   | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| reduce()      | 배열의 요소가 하나가 될 때까지 요소를 왼쪽부터 두 개씩 묶는 함수를 실행한다. |
| reduceRight() | 배열의 요소가 하나가 될 때까지 요소를 오른쪽부터 두 개씩 묶는 함수를 실행한다. |

```js
var array = [1,2,3,4,5];

var output = '';
array.reduce(function(previousValue, currentValue, index, array) {
    output += previousValue + ' : ' + currentValue + ' : ' + index + '\n';
});

alert(output);
```



```js
var array = [1,2,3,4,5];

var result = array.reduce(function(previousValue, currentValue) {
    console.log(previousValue + currentValue);
    return previousValue + currentValue;
});

alert(result);
```





JSON 객체

| 메소드 이름     | 설명                                        |
| --------------- | ------------------------------------------- |
| JSON.stringfy() | 자바스크립트 객체를 JSON 문자열로 변환한다. |
| JSON.parse()    | JSON 문자열을 자바스크립트 객체로 변환한다. |

```js
var object = {
    name: '박경수',
    region: '충주시'
}

var jsonToString = JSON.stringify(object);
alert(jsonToString);

var stringToJSON = JSON.parse(jsonToString);
console.log(stringToJSON);
```

