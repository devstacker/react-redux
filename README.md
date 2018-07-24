# modern react-redux



## Section 1. 리액트소개



### Boiler Plate

- 보일러 플레이트 프로젝트로 먼저 시작해라
    -  boiler plate : 재사용 가능하고 적은 수정만으로 여러곳에 활용 가능한 소스코드
    -  banilla javascript: 라이브러리나 프레임워크 없이 순수 자바스크립트만 사용하는것

### Modern Javascipt Tooling

[사진01]

- tooling(or transpile)은 코드를 같은 수준의 다른 언어로 바꿔주는 과정이다.

- webpack과 babel의 목적은 ES6 코드가 바로 브라우저에서 실행하지 못하는 문제를 해결하기 위해 이를 트랜스파일해서 브라우저에서 돌아가는 코드로 변형하기 위함이다.

- 툴링을 거치면 application.js, main.js, app.js 와 같은 하나의 js 파일로 빌드되어 이를 브라우저에서 제대로 실행할 수 있도록 해준다.

   

### 개발환경 및 프로젝트 설정

##### 보일러 플레이트 어플리케이션을 설치해 보자

아래 사진처럼 실제 유투브API를 사용해 화면을 만들것이다.

[사진02]

```shell
git clone https://github.com/StephenGrider/ReduxSimpleStarter.git
cd ReduxSimpleStarter
npm install
npm start      #localhost:8080
```



##### index.html

```js
<script src="bundle.js"></script>
//bundle.js는 전체 어플리케이션의 컴파일된 자바스크립트 파일
```

> 웹팩과 바벨이 기존에 있는 여러 js파일들을 하나의 bundle.js 파일로 합쳐 이 파일 하나로 이용할 수 있게 만든것

웹서버 localhost:8080을 방문할 때마다 index.html이 작동하게 된다.



##### 우리는 이제 다운받은 보일러 프로젝트(ReduxSimpleStarter)의 src 폴더를 모두 지우고 새로 다시 만들어볼 것이다.

src폴더를 다시 만들고 index.js 생성



### JSX와의 첫만남

- React는 자바스크립트 라이브러리

> 웹브라우저에 보여지는 HTML을 만드는 라이브러리

- Component는 HTML을 만드는 자바스크립트 함수의 모음집  



#### 첫번째 컴포넌트 만들기

컴포넌트를 생성한 후, 이는 DOM 형태로 만들어져야 한다.

여러개의 컴포넌트를 작성할 것인데, 이 컴포넌트는 자동으로 HTML문서에 삽입되는게 아니다.

그래서 우리는 구체적으로 명시해줘야 한다.

> 리액트야 내가 만든 컴포넌트를 DOM으로 넣어줘! - Take this component's generated HTML and put it on the page. (in the DOM) 라고

결론은 먼저 컴포넌트를 만든다음 이것을 페이지에 보이게 하기 위한 코드도 작성해야한다.



```javascript
// index.js
// create a new component.
const App = function() {
    return <div>Hi!</div>;
}
```

어떤게 ES6 코드이고 React인지 구별해보자!

일단 `const` 로 선언한 변수는 무조건 최종값을 가진다. 그래서 변수라 부르지 않고 상수라고 부른다.   그리고 이 App이라는 상수는 선언된 이후 재할당 되지 않을것이다.

function()은 const로 선언된 App에 해당 함수를 할당한 것이고, function() 안에 HTML처럼 보이는 코드는 **JSX** (변형된 자바스크립트)이다. 

원래 자바스크립트 안에 HTML코드는 들어갈 수 없는데, JSX는 자바스크립트 안에 HTML처럼 보이는 소스코드를 사용할 수 있게 한다.



#### 그래서 JSX의 목적은 무엇인가?

JSX의 목적은 자바스크립트 코드를 궁극적으로 HTML으로 만들기 위한 것이다.

ES6 구문같은 JSX의 const는 브라우저에 의해 해석될 수 없는데, 기억해야 할 점은 웹팩과 바벨같은 보일러플레이트 패키지의 목적이 JSX를 바닐라 자바스크립트로 변환해 브라우저가 이해할 수 있도록 만든다는 것이다.

이런식으로 JSX를 사용하는 이유는 컴포넌트를 렌더링할때, DOM에 삽입되기도하고 실제 HTML로 변환되어 제공되기 때문이다.

> 렌더링 한다는 의미는 컴포넌트를 HTML에 올린다는 뜻이다. 

그럼, 왜 처음부터 평범한 자바스크립트 기능을 이용하지 않고 HTML 형태로 보이게 작성하는 것인지 궁금할 것이다. (원하지 않는다면 JSX를 사용할 필요는 없다. 하지만 JSX를 사용하고 싶어질것이다.)

JSX는 바닐라 자바스크립트같은 평범한 자바스크립트로 변경된다는 것을 기억해라.

ES6 REPL(https://babeljs.io/repl/)이라 불리는 도구를 사용해 Index.js 코드를 붙여 넣어보자.

[사진03]

오른쪽 화면에는 바닐라 자바스크립트로 변환된 코드 결과를 보여주는데, 무엇을 의미하는지 한눈에 파악하기 어렵다.

그래서 컴포넌트를 더욱 깔끔하고 보기좋게 만드는것이 JSX를 사용하는 목적이다.

### ES6 import

컴포넌트로부터 반환되는 JSX와 사용자가 보게 되는 DOM안에 넣어지는 과정을 확인해보자.

일단, 처음 말했던 것처럼 오류가 나도록 코드를 작성할 것이다. (오류 고치는 법을 알기위해)

```javascript
React.render(App); //App이라는 컴포넌트를 렌더링하라
```

리액트가 요소를 DOM에 렌더링한다.

코드를 저장하고 웹브라우저 개발자 도구에서 확인해보면, 아래와 같은 오류메시지가 콘솔창에 뜰것이다.

[사진4]

리액트 라이브러리를 불러오지 않아서 그렇다.

어디에다 리액트를 정의하면 될까?

ES6 코드를 작성할때, 우리는 여기서 자바스크립트 모듈에 접근할 수 있다. 자바스크립트 모듈은 서로 분리된 코드 파일들을 또 다른 파일들 혹은 다른 곳에 설치한 라이브러리와 분리할 수 있다.

분리한다는 의미는 다른 파일에 어떠한 변수도 참조될 수 없다는 뜻이다.

따라서 다른 파일에 선언된 코드들은 현재 우리가 보는 코드 와는 아무런 소통을 할 수 없다.

> "저 다른 파일에 따로 접근할 수 있게 권한을 줘!" 라고 만들어놔야만 그게 가능하다.

그래서 React를 이 파일에서 접근할 수 있도록 별도록 선언해야한다.

코드 맨위에 한문장만 적으면 된다.

```js
import React fom 'react';
```

> 리액트를 우리가 설치한 모듈(node_modules 폴더에 설치된 모듈 중)에서 가져와! 

트랜스파일러 같은 라이브러리도 JSX를 표준 자바스크립트로 변환하면서, 이 파일 안의 리액트를 필요로 한다.

그래서 결론적으로 이 파일은 이제 React라는 변수로 접근할 수 있다.





### React DOM vs React

그럼 이제 리액트 라이브러리를 불러왔으니 저장해서 다시 콘솔창을 확인해보자.



[사진5]

왜 나는 스티븐그리더님 처럼 에러가 안뜨지?

??읭??

React.render가 폐기되었으니 ReactDom.render를 'react-dom'으로 불러와 대신 사용하라. 컴포넌트 클래스 전달 대신React.createElement를 전달해 인스턴스화를 확인해라.  라고 에러가 다시 뜰것이다.



리액트는 두개의 분리된 라이브러리로 나뉜다.

> 리액트 라이브러리와 리액트돔 라이브러리

실제 DOM에 렌더링하는 기능을 가지고 이 컴포넌트를 가져와 DOM에 삽입하는 라이브러리는 React DOM이다.

실제 컴포넌트를 DOM에 렌더링하기 위해 쓰는 라이브러리인것.

 그래서 코드를 이렇게 바꿔줘야한다.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

// Create a new Component. 
// This Component should produce some HTML.
const App = function() {
    return <div>Hi!</div>;
}

// Take this component's generated HTML and put it on the page. (in the DOM)
ReactDOM.render(App); // App이라는 컴포넌트를 렌더링하라
```

그럼, 첫번째 에러는 사라질것.

하지만 여전히 컴포넌트 클래스 전달 대신React.createElement를 전달해 인스턴스화를 확인해라. 라는 에러는 해결하지 못했다.



### 컴포넌트 클래스와 컴포넌트 인스턴스의 차이











## Section 2. 리액트와 비동기 리퀘스트 (Ajax Requests)



## Section 3. 어플리케이션 스테이트 모델링



## Section 4. 리덕스로 앱 스테이트 관리하기



## Section 5. 리덕스 : 미들웨어



## Section 6. 리액트 라우터 + 리덕스 폼



## Section 7. 보너스 - 랠리코딩



## Section 8. 더 나아가기!




