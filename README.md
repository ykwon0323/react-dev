# React 개념 튜토리얼 따라하기

## 참고
### 튜토리얼 참고
https://react.dev/learn
### js 문법 참고
https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export
https://javascript.info/import-export
### HTML -> JSX
https://transform.tools/html-to-jsx



## 요약
- 구성 요소를 만들고 중첩하는 방법
- 마크업과 스타일을 추가하는 방법
- 데이터 표시 방법
- 조건 및 목록을 랜더링 하는 방법
- 이벤트 대응 및 화면 업데이트 방법
- 구성 요소 간에 데이터를 공유하는 방법

## 컴포넌트(=구성 요소) 생성 및 중첩
- React 앱은 컴포넌트로 만들어진다
- 컴포넌트 구분? -> 대문자로 시작하게끔 해야한다
~~~ javascript
// MyButton 구성요소 선언
function MyButton() {
    return (
        <button>I'm button</button>
    );
}

// MyButton 구성요소를 사용
export default function MyApp(){
    return (
        <div>
            <h1>Welcome to my app</h1>
            <MyButton />
        </div>
    );
}

~~~

## JSX로 마크업 작성하기
- 하나의 부모 태그로 래핑해야함
- 태그를 항상 닫아야함(HTML보다 엄격)

## Style 추가
- React [className] = HTML [class]
~~~ javascript
<img className="avatar">

.avatar {
    border-radius: 50%;
}
~~~

## 데이터 표시
- {}를 사용하면 Javascript로 "escape" 가능

~~~ javascript
return (
    <h1>
        {user.name}
    </h1>
)
~~~
~~~ javascript
return (
    <img
        className="avatar"
        src={user.imageUrl}
    >
)
~~~

~~~ javascript

const user = {
    name: 'Hedy Lamarr',
    imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
    imageSize: 90,
}

export default function Profile(){
    return(
        <>
            <h1>{user.name}</h1>
            <img
                className="avatar"
                src={user.imageUrl
                alt={'Photo of ' + user.name}}
                style={{
                    width: user.imageSize,
                    height: user.imageSize
                }}
                />
        </>
    )
}

~~~

## 조건부 렌더링
~~~ javascript
let content;

if (isLoggedIn){
    content = <AdminPanel />;
} else {
    content = <LoginForm />;
}

return (
    <div>
        {content}
    </div>
)
~~~
간결하게 하고 싶은 경우 3항 연산 사용
~~~ javascript
<div>
    {isLoggedIn?(
        <AdminPanel />
    ):(
        <LoginForm />
    )}
</div>
~~~
분기가 필요하지 않은 경우 더 짧은 논리 구문을 사용할 수 있음 
~~~ javascript

<div>
    {isLoggedIn && <AdminPanel />}
</div>

~~~

## 렌더링 목록
- for loop 및 map() 함수와 같은 JavaScript 기능을 사용하여 구성요소 목록을 렌더링 
~~~ javascript
const products = [
    { title: 'Cabbage', isFruit: false, id: 1},
    { title: 'Garlic', isFruit: false, id: 2},
    { title: 'Apple', isFruit: true, id: 3},
]

export default function ShoppingList(){
    const listItems = products.map(product => 
    <li
        key={product.id}
        style={{
            color: product.isFruit ? 'magenta' : 'darkgreen'
        }}
    >
        {product.title}
    </li>)
}

return (
    <ul>{listItems}</ul>
)

~~~

## 이벤트에 응답
- 이벤트 핸들러 함수를 선언하여 이벤트에 응답할 수 있음
- 이벤트 핸들러 함수를 호출하지 말 것, 전달만 할 것( 함수명에 괄호를 생략 )
~~~ javascript
function MyButton() {
    function handleClick(){
        alert('You clicked me!');
    }
    return (
        <button onClick={handleClick}>
            Click me
        </button>
    )
}

~~~

## 화면 업데이트 useState

~~~ javascript

import { useState } from 'react' ;

~~~

구성 요소 내에서 상태 변수를 선언 가능 

~~~ javascript
import { useState } from 'react';

export default function MyApp() {
  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
~~~

## 후크 사용 Hook
- use로 시작하는 것을 Hooks 라고함
- 후크는 다른 기능보다 더 제한적임 
- 구성요소(또는 다른 Hook)의 맨 위에서만 Hook를 호출할 수 있음

## 구성 요소 간 데이터 공유
- 최상위 요소에 Props를 설정하여 데이터를 공유함