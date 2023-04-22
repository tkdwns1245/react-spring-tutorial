# Hello React Spring

리액트 스프링을 활용하여 이벤트를 핸들링 하여 다양한 효과를
만들어보기위한 학습을 시작하기로 하였다. 그 첫번째 프로젝트로
react-spring 을 활용하여 프로젝트를 만들어보자
먼저 프로젝트를 생성하고 기본이 되는 기능들을 살펴보며 react spring의 컨셉에 대해서 알아보자.

## Install
먼저 프로젝트를 세팅해보자

### Create React APP
먼저 create-react-app으로 간단하게 리액트 프로젝트를 구성하였다.
~~~
npx create-react-app first-react-spring-tutorial
~~~
### react-spring 다운로드
yarn 을 활용해 간단하게 라이브러리를 다운로드 할 수 있다.
~~~
yarn add @react-spring/web
~~~


## First Animation
프로젝트 세팅을 마쳤다면 처음으로 react spring 을 활용하여 이벤트를 발생하는 컴포넌트를 만들어보자.

### 컴포넌트 만들기

create-react-app 으로 프로젝트를 세팅하였다면 프로젝트 폴더 하위에 public,src,components 폴더가 생겼을 것이다.
src 폴더 하위에 components 폴더를 만들고 그 하위에 MyComponents.js 파일을 만들고 코드를 작성해보자.
코드는 다음과 같다.

```javascript
import { useSpring, animated } from '@react-spring/web'

export default function MyComponent() {
  const springs = useSpring({
    from: { x: 0 },
    to: { x: 100 },
  })

  return (
    <animated.div
      style={{
        width: 80,
        height: 80,
        background: '#ff6d6d',
        borderRadius: 8,
        ...springs,
      }}
    />
  )
}
```

 위 코드를 작성하고 App.js 에 MyComponent를 작성 해 보면 다음 결과물을 확인 할 수 있다.
https://codesandbox.io/s/hello-react-spring-example-kypdo4?file=/src/App.js

우리의 첫번째 React-Spring 이벤트 예제이다!~

### 사용법 설명

1. Animated Element 생성
   - 다음 코드를 보면 알 수 있듯이 
   ```javascript  
   import { animated } from '@react-spring/web'

   <animated.div
      style={{
        width: 80,
        height: 80,
        background: '#ff6d6d',
        borderRadius: 8,
        ...springs,
      }}
    />
    ```
    animated.div components 를 생성한다. 이 animated components 를 통해 이벤트가 동작한다. 이것은 higher-order component (HOC) 패턴으로 동작하단다. 이에대한 설명은 다음 docs 에서 확인 할 수 있다.
    https://ko.legacy.reactjs.org/docs/higher-order-components.html
    
2. useSpring Hook 사용
   - 다음으로는 useSpring Hook 을 사용하여 SpringValues 들을 생성하고 이를 Animated Component 의 props 에 전달함으로써 이벤트를 선언한다.

```javascript
import { useSpring, animated } from '@react-spring/web'

export default function MyComponent() {
  const springs = useSpring({
    from: { x: 0 },
    to: { x: 100 },
  }) /* useSpring Hook을 사용하여 springValues를 생성*/

  return (
    <animated.div
      style={{
        width: 80,
        height: 80,
        background: '#ff6d6d',
        borderRadius: 8,
        ...springs, /* spread operator 를 활용하여 springValues Object 전달*/
      }}
    />
  )
}
```
   - 위 코드에서 from 과 to 에는 이벤트의 시작과 끝에 동작하는 효과를 정의한다. 아주 간단하게 이벤트가 동작하는것을 확인 할 수 있다.

### 이벤트 바인딩하여 애니메이션 적용해보기
보통에 애니메이션는 mouseenter,click,keydown 등 이벤트가 발생 시 동작하도록 하여 활용한다. react spring 에서는 이를 아주 간단하게 구현 할 수 있다.

```javascript
import { useSpring, animated } from '@react-spring/web'

export default function MyComponent() {
  const [springs, api] = useSpring(() => ({
    from: { x: 0 },
  }))

  const handleClick = () => {
    api.start({
      from: {
        x: 0,
      },
      to: {
        x: 100,
      },
    })
  }

  return (
    <animated.div
      onClick={handleClick}
      style={{
        width: 80,
        height: 80,
        background: '#ff6d6d',
        borderRadius: 8,
        ...springs,
      }}
    />
  )
}
```

useSpring Hook의 첫번째 인자로 함수를 넣으면 springValues와 api object 가 리턴된다. springValues는 기존에 애니메이션을 발생시키는 animated component에 그대로 활용하면 되고, api object 는 이벤트를 발생시키는 함수를 선언하여 활용하면 된다!. 아주 간단하다.

위 코드에서는 handleClick 이라는 함수를 선언해주고 api 의 start 함수를 활용해 이벤트를 발생시키는 함수를 작성하고 이를 animated.div 에 바인딩 해 주었다.

그 결과! 해당 component 를 클릭시 이벤트가 발생하는것을 확인 할 수 있다.

https://codesandbox.io/s/hello-react-spring-example2-l41pdu?file=/src/components/MyComponent.js



## Referenced  
- React Spring Getting Started :https://www.react-spring.dev/docs/getting-started#the-animated-element