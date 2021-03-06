# Javascript Study with Dream Coding
---

## 1강. 콘솔 출력, async vs defer, use strict


###  1-1. 콘솔 출력
<br>

#### 1-1-1. 터미널에서 node 로 출력

아래와 같이 자바스크립트를 작성한다.
``` Javascript
console.log('Hello World!');
```

이후 터미널에서 파일이 있는 위치로 이동 후 __`node (파일명).js`__ 로 실행
 (_단 node js 설치를 해야 한다._)

<br>

#### 1-1-2. 웹 콘솔로 출력 (Chorme)
<br>

아래와 같이 html 파일을 작성한다.
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="main.js"></script>
  </head>
  <body></body>
</html>
```

이후 html을 크롬으로 실행 시킨 후 __`ctrl + shift + i`__ 로 개발자 도구를 활성화 시킨다.

개발자 도구에서 Console창을 확인한다.

![개발자도구](./jsimages/1.png "콘솔창에서 Hello world가 출력된다. 또한 h의 값을 정해주고 h를 출력하면 지정 값이 도출된다.")


<br>

### 1-2. _async_ vs _defer_

___HTML에서 자바스크립트를 불러올 때 어떤 방식이 더 좋을까?___

* #### head 안에서 바로 블러오기

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <script src="main.js"><script>
  </head>
  <body></body>
<html>
```
![헤드에스크립트](./jsimages/2.png "Parsing을 멈추고 서버에서 js 를 받음")

 __위 방식의 단점은, 사용자가 웹사이트를 보기 위해 시간이 오래 걸린다.__

<br>

* #### body 마지막에 불러오기
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <div></div>
    <script src="main.js"></script>
  </body>
<html>
```

![바디에스크립트](./jsimages/3.png "parsing이 끝난 뒤 js를 받고 실행")

__위 방식의 단점은, 웹페이지가 js에 의존적이라면 정상적인 페이지를 보기까지 오래걸린다.__

<br>

* #### head에 async를 통해 불러오기

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <script asyn src="main.js"></script>
  </head>
  <body>
    <div></div>
  </body>
<html>
```

![헤드에에이싱크](./jsimages/4.png "parsing을 하다 동시에 병렬적으로 다운 후 실행")

__body끝에 fetching 하기 보다 다운로드 받는 시간을 절약할 수 있다. 그러나 js가 HTML이 Parsing되기 전에 정의되지 않을 수 있고 페이지를 보기 전에 시간이 더 걸릴 수 있다.__

<br>

* #### head에 defer을 통해 불러오기

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <script defer src="main.js"></script>
  </head>
  <body>
    <div></div>
  </body>
<html>
```

![헤드에디퍼](./jsimages/5.png "parsing 도중 병렬적 다운 후 parsing 이후 js 실행")

__HTML을 parsing 하는 동안 필요한 js를 받고, HTML을 모두 parsing 한 다음 js를 실행하여 사용자에게 더 빠른 컨텐츠를 제공한다.__

__만약 다수의 js들이 순서에 의존적이라면 `head + async` 보다는 `head + defer` 이 더 효율적인 방식이다.__

<br>

### 1-3. 'use strict';

자바스크립트는 특성상 유연한(flexible) 언어이기 때문에, 실수가 잦을 수 있다.
이러한 문제의 해결을 위해(?) use strict는 __ECMAscript 5__ 부터 추가되었다.


* #### use strict가 없을 시
```javascript
console.log("Hello World!");

a = 6;
```

![스트릭안해](./jsimages/6.png "문제 없이 진행")

* #### use strict가 있을 시
```javascript
"use strict";

console.log("Hello World!");

a = 6;
```

![스트릭해](./jsimages/7.png "a가 정의되지 않았다는 오류가 뜸")

use strict로 인해 a의 선언오류를 확인 할 수 있다.
이는 `let a;` 를 `a = 6;` 윗 줄에 추가하여 수정할 수 있다.

__use strict 모드를 이용하면 조금 더 상식적인 범위 내에서 js를 이용할 수 있고, js 엔진이 더욱 효율적으로 js를 분석 할 수 있다.__


---
