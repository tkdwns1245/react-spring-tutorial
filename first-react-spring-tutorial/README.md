# Hello React Spring

리액트 스프링을 활용하여 이벤트를 핸들링 하여 다양한 효과를
만들어보기위한 학습을 시작하기로 하였다. 그 첫번째 프로젝트로
react-spring 을 활용하여 프로젝트를 만들어보자

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
<iframe src="https://codesandbox.io/embed/quirky-roman-kypdo4?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:250px; border:0; border-radius: 4px; overflow:hidden;"
     title="quirky-roman-kypdo4"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

우리의 첫번째 React-Spring 이벤트 예제이다!~