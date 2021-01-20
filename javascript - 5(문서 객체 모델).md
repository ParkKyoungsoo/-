

## 문서 객체 모델

```html
<!DOCTYPE html>
<html>
    <head>
        <title>index</title>
        <script></script>
    </head>
    <body>
        <h1 id="header">
            HEADER
        </h1>
    </body>
</html>
```

- 문서 객체 : 태그(`<body></body>`)를 자바스크립트에서 이용할 수 있는 객체로 만든것



```js
window.onload = function() {
    var header = document.getElementById('header');	
}
```

`header`가 문서 객체가 된다.



- 요소 노드 : HTML 태그
- 텍스트 노드 : 요소 노드 안에 들어 있는 글자



웹 페이지가 처음 HTML 페이지에 적혀 있는 태그들을 읽으며 생성하는 것을 "정적으로 문서 객체를 생성한다."

자바스크립트로 원래 HTML 페이지에는 없던 문서 객체를 생성하는 것을 "동적으로 문서 객체를 생성한다."



##### 문서 객체 만들기

document 객체의 노드 생성 메소드

| 메소드 이름            | 설명                    |
| ---------------------- | ----------------------- |
| createElement(tagName) | 요소 노드를 생성한다.   |
| createTextNode(text)   | 텍스트 노드를 생성한다. |

문서 객체의 연결 메소드
| 메소드 이름       | 설명                    |
| ----------------- | ----------------------- |
| appendChild(node) | 객체에 노드를 연결한다. |

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var header = document.createElement('h1');
            var textNode = document.createTextNode('Hello DOM');

            header.appendChild(textNode);
            document.body.appendChild(header);
        }
    </script>
</head>
<body>
</body>
</html>
```



텍스트 노드를 갖지 않는 노드

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var img = document.createElement('img');
            img.src = 'https://w.namu.la/s/090992c37cc12fb97cdce72e7275e27244bbfb3bdfc7a7347d4543d496e466cea8b5bcb9f25bf365b59a223cc2b17768b6c9631e96d7d16e1ef101c207040e2a457ad8bd54f0c1c0936209f273c76e816b4fdee35493319df6dd418bca2e6fe76112536b605e5b536d33b2cb79a711ea';
            img.width = 1000;
            img.height = 700;

            document.body.appendChild(img);
        }
    </script>
</head>

<body>

</body>

</html>
```



웹 브라우저가 지원하지 않는 속성은 아래 메소드를 사용해야 속성을 넣을 수 있다.

| 메소드 이름               | 설명                    |
| ------------------------- | ----------------------- |
| setAttribute(name, value) | 객체의 속성을 지정한다. |
| getAttribute(name)        | 객체의 속성을 가져온다. |

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var img = document.createElement('img');
            img.setAttribute('src', 'https://w.namu.la/s/090992c37cc12fb97cdce72e7275e27244bbfb3bdfc7a7347d4543d496e466cea8b5bcb9f25bf365b59a223cc2b17768b6c9631e96d7d16e1ef101c207040e2a457ad8bd54f0c1c0936209f273c76e816b4fdee35493319df6dd418bca2e6fe76112536b605e5b536d33b2cb79a711ea');
            img.setAttribute('width', 700);
            img.setAttribute('height', 500);

            img.setAttribute('data-property', 350);

            document.body.appendChild(img);
        }
    </script>
</head>
<body>

</body>
</html>
```



innerHTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var output = '';
            output += '<ul>';
            output += ' <li>JavaScript</li>';
            output += ' <li>Vue</li>';
            output += ' <li>React</li>';
            output += '</ul>';

            document.body.innerHTML = output;

            // document.body.innerHTML += '<h1>Document Object Model</h1>';
        }
    </script>
</head>
<body>
</body>
</html>
```



##### 문서 객체 가져오기

| 메소드 이름                   | 설명                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| getElementById(id)            | 태그의 속성이 id 매개변수와 일치하는 문서의 객체를 가져온다. |
| getElementByName(name)        | 태그의 name 속성이 name 매개변수와 일치하는 문서 객체를 배열로 가져온다. |
| getElementsByTagName(tagName) | tagName 매개변수와 일치하는 문서 객체를 배열로 가져온다.     |

HTML5 부터 document 객체에 메소드가 추가 되었다.

| 메소드 이름              | 설명                                                |
| ------------------------ | --------------------------------------------------- |
| querySelector(선택자)    | 선택자로 가장 처음 선택되는 문서 객체를 가져온다.   |
| querySelectorAll(선택자) | 선택자를 통해 선택되는 문서 객체를 배열로 가져온다. |



##### 문서의 객체 스타일 조작

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var header = document.getElementById('header');

            header.style.border = '2px solid black';
            header.style.color = 'orange';
            header.style.fontFamily = 'helvetica';
        }
    </script>
</head>

<body>
    <h1 id="header">안녕</h1>
</body>

</html>
```



##### 문서 객체 제거

| 메소드 이름        | 설명                              |
| ------------------ | --------------------------------- |
| removeChild(child) | 문서 객체의 자식 노드를 제거한다. |

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        window.onload = function () {
            var willRemove = document.getElementById('will-remove');

            // document.body.removeChild(willRemove);
            willRemove.parentNode.removeChild(willRemove);
        }
    </script>
</head>

<body>
    <h1 id="will-remove">Header</h1>
</body>

</html>
```

`document.body.removeChild(willRemove);`는 body 문서 객체 바로 아래에 제거하고자 하는 문서 객체가 있으므로 사용 가능

일반적으로 문서 객체를 제거할때는 `willRemove.parentNode.removeChild(willRemove);`처럼 h1태그에서 부모 노드로 이동하고 부모 노드에서 자식 노드를 삭제한다.

