# <b>리액트 정리</b>

## React 정리

# react와 reactDOM의 차이!

- react = UI라이브러리, reactDOM = 리액트를 웹사이트에 출력을 도와주는 모델

* 리액트의 주요 특징 중 하나는 Virtual DOM을 사용

* DOM이란? (Document Object Model)
  객체로 문서 구조를 표현하는 방법으로 XML이나 HTML로 작성한다. 웹 브라우저는 DOM을 활용하여 자바스크립트와 css를 적용한다.

* React는 Virtual DOM방식을 사용하여 DOM 업데이트를 추상화함으로써 DOM 처리 횟수를 최소화하고 효율적으로 진행한다.

* 동작방식

1. 데이터를 업데이트하면 전체 UI를 Virtual DOM에 리렌더링 한다.
2. 이전 Virtual dom에 있던 내용과 비교
3. 바뀐 부분만 실제 DOM에 적용

- 리액트는 단방향(Unidirectional) 데이터 플로우를 가지고 있다.
- 데이터는 항상 일정한 장소에 위치해있고, 그 장소에서만 변경 가능!
- UI가 바뀌지 않음.
- 데이터 -> 데이터 변경 -> UI변경
- reactDOM은 1개의 컴포넌트를 출력(render)하고, Component는 항상 render , return 해줘야 한다.

# 주요 Tip!!

- 함수에 언더스코어(\_)를 붙여서 만듬

* -> 이유는, 리액트는 자체 기능이 많기 때문에 리액트 자체기능과 구분하기 위해서

- 주석 : {/_ … _/} 사이에 넣거나, 태그 사이에 넣을 수 있다.

* 모든 Component는 render()함수를 가지고 있다.
* // Component에서 사용하는 유일한 function

* react application은 하나의 component만 rendering 한다.

* 구조 분해 할당 : 배열이나 객체 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식이다.  
  ex) [a, b, ...rest] = [1, 2, 3, 4, 5];

# Props

- -> 부모 컴포넌트가 자식 컴포넌트에게 주는 값

- defaultProps값 설정으로 초기값 설정 가능!  
  https://velopert.com/3629

- propType 라이브러리 사용해서 입력값 검증한다.

- 함수형 컴포넌트 : props만 받아와서 보여주기만 하는 함수형 컴포넌트

# State

- state는 리액트 컴포넌트 안에 있는 상태

- state가 바뀔 때 마다 render가 발생한다.

- state를 직접 명시에서 바꾸면 안된다.
- state처음에 명시해주고, state를 바꿀떄는 setState를 설정한다.  
  (setState로 state를 바꿔줘야 state를 바꾸고, render()함수를 호출한다.)  
  (setState는 DidMount안에 넣어줌)

- State 변경 방법
- ex1) this.setState(current => ({ count : current.count + 1})) // 이런 방식이 좋음

- ex2) this.setState(this.state.count + 1)

# JSX

- jsx란 리액트로 html쓰는 방법!

* jsx의 경우 명령을 실행시키려면 괄호{} 를 꼭 쳐야한다.

* JSX내부에서 조건부 렌더링을 할 때는 보통 삼항 연산자를 이용하거나, AND연산자를 이용한다.

# LifeCycle

https://ko.reactjs.org/docs/react-component.html#static-getderivedstatefromprops  
https://velopert.com/3631

## 1. mounting : 페이지 생성

- ### 1) constructor (javascript에서 class만들 때 호출)

  - 컴포넌트 생성자 함수
    - super(props)를 호출해야 한다.
  - 목적
    - this.state에 객체를 할당하여 지역 state 초기화
      - this.state를 직접 할당할 수 있는 유일한 곳
      - 이외 메소등서는 this.setState() 사용해야 한다.
    - 인스턴스에 이벤트 처리 메소드 바인딩

- ### 2) static getDerivedStateFromProps()
  - 시간에 따라 변하는 props에 state가 의존하는 경우 사용
  - 보다 간단한 대안
    - 1. props 변화에 대응한 부수효과 발생
      - ComponentDidUpdate사용!
    - 2. props가 변화했을 때 일부 데이터만 변환
      - (https://ko.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#what-about-memoization)
    - 3. props가 변화할 때 일부 state 재설정
      - 완전 제어 컴포넌트
        - https://ko.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-controlled-component
      - key를 사용하는 완전 비제어 컴포넌트
        - https://ko.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-uncontrolled-component-with-a-key

* ### 3) render()

  - 컴포넌트에서 반드시 구현
  - props와 state값을 활용하여 값을 반환
  - 반환 값

    - React 엘리먼트 ex) `<MyComponent />`

      - Dom노드
      - 사용자가 정의한 컴포넌트

    - Fragment : 여러개의 엘리먼트 반환 ex) `<React. Fragment> or <> </>`
    - Fragment에 전달 가능한 유일한 속성 -> key
    - Portal (React 16에서 도입된 기능)  
      : 리액트 프로젝트에서 컴포넌트를 렌더링하게 될 때 UI 를 어디에 렌더링 시킬지 DOM을 사전에 선택하여 부모 컴포넌트의 바깥에 렌더링 할 수 있게 하는 기능  
      (https://velog.io/@velopert/react-portals 참고)

      - 불필요한 상속, 레이어 위치 관리(z-index) 스타일 관리할 때 유용하게 사용된다.
      - DOM의 계칭구조 시스템에 종속되지 않으면서 컴포넌트 렌더링 가능!
      - index.html에 해당 DOM 있어야 함.
      - modal 구현 좋음
        - modal이란 ?
          : 사용자 인터페이스 디자인 개념에서 자식 윈도에서 부모  
           윈도로 돌아가기 전에 사용자의 상호동작을 요구하는 창

    - 문자열, 숫자
      - Boolean 또는 null
      - return test && <Child /> 패턴을 지원하는데 사용된다.

* ### 4) componentDidMount()
  - <b>외부 라이브러리 연동
  - 컴포넌트에 필요한 데이터 요청 (axios, fetch, DB)
  - DOM의 속성을 읽거나 변경하는 작업 : 스크롤 설정, 크기 읽어오기 등</b>

## 2. updating : 페이지 업데이트 , state가 변경될 때

- ### 1) static getDerivedStateFromProps()

  - props로 받아온 값을 state로 동기화 하는 작업을 해줘야 하는 경우에 사용
  - setState (x) / <b>특정 props가 바뀔 때 설정하고 싶은 state를 반환하는 형식으로 사용</b>

- ### 2) shouldComponentUpdate()
  - 변화가 필요한 부분만 업데이트 하기 위해 사용
  - 조건에 따라 false를 반환하면 해당 조건에서 render실행 x
- ### 3) render()
- ### 4) getSnapshotBeforeUpdate()
  - DOM에서 변화하기 직전의 DOM값을 가져오고 여기서 리턴하는 값을 componentDidUpdate에서 3번째 값으로 가져올 수 있다.
- ### 5) componentDidUpdate() : setState 실행 후 실행이 된다.
  - 이 시점에서 props와 state 값 바뀌어 있음.
  - prevProps, prevState, snapshot 조회 가능

## 3. unmounting

- ### 1) componentWillUnmount() : component가 죽을 때 동작
  - 이벤트 제거, 외부 라이브러리 인스턴스 제거 (해당 라이브러리에 dispose 기능이 있을 경우)

## 4. Error boundary

- 1), 2) 함수를 정의할 경우 해당 컴포넌트는 Error boundary가 됨
  - 자신보다 하위에 존재하는 컴포넌트 오류만 잡아낼 수 있다.
- ### 1) static getDerivedStateFromError()
- ### 2) componentDidCatch()
  - 2개의 매개변수를 전달받음
    - 1. error : 발생한 오류
    - 2. info : 어떤 컴포넌트가 오류를 발생시켰는지에 대한 정보
  - <B>로그 기록</B>같은 부수 효과를 발생시켜도 된다.
  - render함수 작성해서 대체 UI 렌더링 가능!

## 기타 API

- setState()
- forceUpdate()

# Router 구현

- `<a>` 태그로 구현하면 페이지가 새로 고침이 되기 때문에
- Router 기능 구현을 위해 react-router-dom라이브러리에 link 사용
  // link는 <router> 컴포넌트 안에 있어야 한다.

# 기타 Tip!!

npx 는 현재 프로젝트에 설치된 디펜던시를 마치 Path로 잡아 놓은 것 마냥 바로 사용할 수 있게 해주는 명령이다. npm에 포함되어 있다. 모드 옵션을 development로 주었다.

map함수는 1) index, 2) 값 넘겨준다.

route기능 : react-router-dom

# Github 배포 순서

1. gh-page 설치
2. package.json에 homepage 작성
3. build -> deploy
