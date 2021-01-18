## 객체

##### 객체 개요

객체와 배열의 차이

- 객체 : key값을 이용해 value 접근
- 배열 : index를 이용해 value 접근

```js
var product = {
	제품명 : '7D 건조 바나나',
	유형 : '당절임',
	성분 : '바나나, 설탕, 메타중아황산나트륨, 치자황색소',
	원산지 : '필리핀'
};

product['제품평']
product.제품명
```



객체의 key는 식별자 또는 문자열을 모두 사용할 수 있다. 식별자가 아닌 문자를 키로 사용했을 때는 무조건 대괄호를 사용해야 객체의 요소에 접근할 수 있다.

```js
var object = {
	'with space': 23,
	'with ~!@#$%^&*()_+': 52,
};

object['with space']
```



##### 속성과 메서드

메서드 내에서 자기 자신이 가진 속성을 출력하고 싶을 때는 자신이 가진 속성임을 분명하게 표시해야 한다.

```js
var person = { 
	name: '박경수',
    eat: function (food) {
		alert(this.name + '가 ' + food + '을/를 먹습니다.');
	}
};

person.eat('바나나');
```



##### 객체의 반복문

객체는 단순  for 반복문으로 객체의 속성을 살펴보는것은 불가능하다. `for in`을 사용한다.

```js
var product = {
	name: 'Micorsoft Visual Studio 2015 Ultimate',
    price: '15,000,000원',
    language: '한국어',
    supportOS: 'win 32/64',
    subscription: true,
}

var output = '';
for(var key in product){
    output += '- ' + key + ' : ' + product[key] + '\n';
}
alert(output);
```



##### 객체 관련 키워드

```js
var Student = {
	이름: '구상벽',
    국어: '15',
    수학: '2',
    영어: '17',
    과학: '5',
}
```

1. in 키워드

   해당 키가 객체 안에 있는지 확인 할 수 있다.

   ```js
   var output = '';
   var student = {
   	이름: '구상벽',
       국어: '15',
       수학: '2',
       영어: '17',
       과학: '5',
   }
   
   output += "'이름' in student: " + ('이름' in student) + '\n';
   output += "'성별' in student: " + ('성별' in student) + '\n';
   
   alert(output);
   ```

   



2. with 키워드

   복잡하게 사용해야 하는 코드를 짧게 줄여주는 키워드

   ```js
   var student = {
   	이름: '구상벽',
       국어: 15,
       수학: 2,
       영어: 17,
       과학: 5,
   }
   
   var output = '';
   output += '이름 : ' + student.이름 + '\n';
   output += '국어 : ' + student.국어 + '\n';
   output += '수학 : ' + student.수학 + '\n';
   output += '영어 : ' + student.영어 + '\n';
   output += '과학 : ' + student.과학 + '\n';
   output += '총점 : ' + (student.국어 + student.수학 + student.영어 + student.과학) + '\n';
   alert(output);
   ```

   ```js
   var student = {
   	이름: '구상벽',
       국어: 15,
       수학: 2,
       영어: 17,
       과학: 5,
   }
   
   var output = '';
   with(student) {
   	output += '이름: ' + 이름 + '\n'; 
       output += '국어: ' + 국어 + '\n';
       output += '수학: ' + 수학 + '\n';
       output += '영어: ' + 영어 + '\n';
       output += '과학: ' + 과학 + '\n';
       output += '총점: ' + (국어 + 수학 + 영어 + 과학) + '\n';
   }
   alert(output);
   ```



##### 객체의 속성 추가와 제거

```js
var student = {};

student.이름 = "구상벽";
student.나이 = 28;

student.toString = function() {
	var output = '';
    for(var key in student) {
		if(key != 'toString') {
			output += key + '\t' + this[key] + '\n';
		}
	}
    return output;
}

alert(student.toString());

delete(student.나이);

alert(student.toString());
```



##### 얕은 복사와 깊은 복사

```js
var originValue = 10;
var newValue = originValue;

originValue = 222;

alert(originValue);
alert(newValue);
```







## 생성자 함수

##### 생성자 함수 개요

```js
// 생성자 함수 생성
function Student(name, korean, math, english, science) {
    this.name = name;
    this.korean = korean;
    this.math = math;
    this.english = english;
    this.science = science;
    
    this.getSum = function() {
		return this.korean + this.math + this.english + this.science;
	}
    
    this.getAvg = function() {
		return this.getSum() / 4;
	}
    
    this.toString = function() {
		return this.name + '\t' + this.getSum() + '\t' + this.getAvg();
	}
}

var students = [];
students.push(new Student('박경수',14,15,21,22));
students.push(new Student('구상벽',43,2,56,89));

var output = '이름\t총점\t평균\n';
for(var i in students) {
	output += students[i].toString() + '\n';
}

var student = new Student('이름',98,98,98,100);

alert(output);
alert(student instanceof Student);
```



##### 프로토타입

생성자 함수로 생성된 객체가 공통으로 가지는 공간

```js
/// 생성자 함수 생성
function Student(name, korean, math, english, science) {
    this.name = name;
    this.korean = korean;
    this.math = math;
    this.english = english;
    this.science = science;
}
Student.prototype.getSum = function() {
    return this.korean + this.math + this.english + this.science;
};
Student.prototype.getAvg = function() {
    return this.getSum() / 4;
};
Student.prototype.toString = function() {
    return this.name + '\t' + this.getSum() + '\t' + this.getAvg();
};

var students = [];
students.push(new Student('박경수',14,15,21,22));
students.push(new Student('구상벽',43,2,56,89));

var output = '이름\t총점\t평균\n';
for(var i in students) {
	output += students[i].toString() + '\n';
}

var student = new Student('이름',98,98,98,100);

alert(output);
```



##### 캡슐화

특정 속성이나 메서드를 사용자가 사용할 수 없게 숨겨놓는 것

```js
// 사각형을 의미하는 Rectangle 객체를 만들어보자
function Rectangle(width, height) {
    
    var w = width;
    var h = height;
    
    this.getWidth = function() {
		return w;
    }
    this.getHeight = function() {
		return h;
	}
    this.setWidth = function(width) {
		if(width < 0) {
			throw '길이는 음수일 수 없습니다.';
        } else {
            w = width;
        }
	}
    this.setHeight = function(height) {
		if(height < 0) {
			throw '길이는 음수일 수 없습니다.';
        } else {
            h = height;
        }
	}
}

Rectangle.prototype.getArea = function() {
	return this.getWidth() * this.getHeight();
}

var rectangle = new Rectangle(5,7);
rectangle.setWidth(-3);

alert('Area: ' + rectangle.getArea());
```



##### 상속

```js
// Square를 만들자
function Rectangle(width, height) {
    
    var w = width;
    var h = height;
    
    this.getWidth = function() {
		return w;
    }
    this.getHeight = function() {
		return h;
	}
    this.setWidth = function(width) {
		if(width < 0) {
			throw '길이는 음수일 수 없습니다.';
        } else {
            w = width;
        }
	}
    this.setHeight = function(height) {
		if(height < 0) {
			throw '길이는 음수일 수 없습니다.';
        } else {
            h = height;
        }
	}
}

Rectangle.prototype.getArea = function() {
	return this.getWidth() * this.getHeight();
}

//////////////////////////////////////
function Square(length) {
	this.base = Rectangle;					// .......1
    this.base(length, length);				// .......2
}

Square.prototype = Rectangle.prototype;		// .......3
Square.prototype.constructor = Square;		// .......4

var rectangle = new Rectangle(5,7);
var square = new Square(5);

alert(rectangle.getArea() + ' : ' + square.getArea());
alert(square instanceof Rectangle);
```

1,2번을 사용해 Rectangle 객체의 속성을 Square 객체에 추가

3,4번을 사용해 Rectangle 객체의 프로토타입이 가진 속성 또는 메소드를 Square객체의 프로토타입에 복사