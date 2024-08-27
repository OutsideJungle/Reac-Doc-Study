## Section 1. GET STARTED - Quick Start

<br>

1. [컴포넌트를 만들고 중첩하는 방법](#1-컴포넌트를-만들고-중첩하는-방법)
2. [마크업과 스타일을 추가하는 방법](#2-마크업과-스타일을-추가하는-방법)
3. [데이터를 표시하는 방법](#3-데이터를-표시하는-방법)
4. [조건과 리스트를 렌더링하는 방법](#4-조건과-리스트를-렌더링하는-방법)
5. [이벤트에 응답하고 화면을 업데이트하는 방법](#5-이벤트에-응답하고-화면을-업데이트하는-방법)
6. [컴포넌트 간에 데이터를 공유하는 방법](#6-컴포넌트-간에-데이터를-공유하는-방법)

<br>

### 1. 컴포넌트를 만들고 중첩하는 방법

📎 **컴포넌트란?**
- **독립성** : 각 컴포넌트는 자체적인 로직과 렌더링 방식을 가짐
- **재사용성** : 한 번 만든 컴포넌트는 여러 곳에서 재사용 가능
- **계층 구조** : 컴포넌트들은 서로 중첩되어 복잡한 UI 생성 가능
- **속성** : 부모 컴포넌트로부터 데이터를 받아 동적으로 렌더링 가능
- **상태** : 컴포넌트 내부에서 관리되는 데이터로, 변경 시 재렌더링을 트리거

💡 **Example**
```javascript
function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```
- ✔ `export default`는 파일의 **기본 컴포넌트** 지정
- ✔ **React 컴포넌트**의 이름은 항상 **대문자**로 시작, **HTML 태그**는 **소문자**로 시작

<br>

### 2. 마크업과 스타일을 추가하는 방법

📌 **JSX로 마크업 작성하기**
- JSX는 HTML보다 엄격하기 때문에 `<br />`과 같이 태그를 닫아야 함
- 컴포넌트는 여러 개의 JSX 태그를 반환할 수 없음
- JSX 표현식은 **반드시 하나의 부모 요소**로 감싸져야 함

📌 **스타일 추가하기**
- React에서는 `className`으로 **CSS 클래스 지정**
```javascript
<img className="avatar" />
```

- 그 다음 별도의 CSS 파일에 해당 **CSS 규칙 작성**
```css
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```

<br>

### 3. 데이터를 표시하는 방법
> - JSX 컨텍스트에서 "escape"란 JSX 문법에서 잠시 빠져나와 **순수한 자바스크립트 코드를 실행**할 수 있게 하는 것
> - 즉, JSX의 "HTML-like" 환경에서 잠시 "탈출"하여 자바스크립트 영역으로 들어가는 것을 의미
> - 이런 방식을 통해 JSX에서 **정적인 HTML**과 **동적인 JavaScript**를 자연스럽게 섞어서 사용 가능

📌 **중괄호 {} 사용**
```javascript
<h1>{user.name}</h1>
```
📌 **속성에서의 중괄호 사용**
```javascript
<img className="avatar" src={user.imageUrl} />
```

<br>

### 4. 조건과 리스트를 렌더링하는 방법
#### 4-1. 조건부 렌더링
일반적인 자바스크립트 코드를 작성할 때 사용하는 것과 동일한 방법 사용

📌 **`if`문 사용**
```javascript
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```

📌 **조건부 삼항 연산자 사용**
```javascript
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

📌 **`&&` 연산자 사용 (`else` 분기가 필요 없을 때)**
```javascript
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

<br>

#### 4-2. 리스트 렌더링
컴포넌트 리스트를 렌더링하기 위해서는 `for`문 및 `map()` 함수와 같은 자바스크립트 기능 사용

```javascript
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```

📎 **React의 `key` 속성**
- `key` 속성에 목록의 각 항목에 대해, 형제 항목 사이에서 해당 항목을 고유하게 식별하는 문자열 또는 숫자를 전달해야 함
- React는 `key`를 사용하여 리스트 항목의 추가, 제거, 순서 변경 등을 추적 (주로 ID를 사용)
- 이를 통해 불필요한 리렌더링을 줄이고 성능을 최적화

<br>

### 5. 이벤트에 응답하고 화면을 업데이트하는 방법
- 컴포넌트 내부에 이벤트 핸들러 함수를 선언하여 이벤트에 응답
- 이벤트 핸들러 함수를 호출하지 않고 전달만 하면 됨 (ex. `onClick={handleClick}`)

```javascript
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

<br>

- 컴포넌트가 특정 정보를 "기억"하여 표시하기를 원하는 경우, 컴포넌트에 `state` 추가
- `useState`로부터 현재 `state`와 이를 업데이트할 수 있는 함수를 얻을 수 있음
- 주로 `[something, setSomething]`으로 작성하는 것이 일반적
- 같은 컴포넌트를 여러 번 렌더링하면 각각의 컴포넌트는 고유한 `state`를 얻게 됨

```javascript
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
```

📎 **Hooks 사용하기**
- `use`로 시작하는 함수를 **Hooks**라고 함
- `useState`는 React에서 제공하는 내장 Hook
- Hooks는 다른 함수보다 **제한적**임
- **컴포넌트 또는 다른 Hooks의 상단**에서만 Hooks를 호출 가능
- ex. 조건이나 반복문에서 `useState`를 사용하고 싶다면, 새 컴포넌트를 추출하여 삽입해야 함

<br>

### 6. 컴포넌트 간에 데이터를 공유하는 방법

```javascript
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}
```

```javascript
function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

📌 **코드 분석**
- **초기 상태**
  - 부모 컴포넌트(`MyApp`)에서 `count` 상태와 `handleClick` 함수를 정의
  - 이 `count`와 `handleClick`을 자식 컴포넌트(`MyButton`)에 **props**로 전달

- **이벤트 핸들링**
  - 클릭 이벤트가 발생하면, 자식 컴포넌트에서 props로 받은 `onClick` 함수(실제로는 부모의 `handleClick` 함수) 실행

- **상태 업데이트**
  - 부모 컴포넌트의 `handleClick` 함수가 실행되어 `setCount(count + 1)`를 호출
  - 이로 인해 부모 컴포넌트의 `count` 상태 업데이트

- **리렌더링**
  - React는 상태 변경을 감지하고 부모 컴포넌트를 리렌더링
  - 리렌더링 과정에서 업데이트된 `count` 값이 다시 자식 컴포넌트들에게 **props**로 전달

- **자식 컴포넌트 업데이트**
  - 새로운 `count` 값을 받은 자식 컴포넌트들도 리렌더링되어 업데이트된 값 표시

📌 **데이터의 흐름**
- 부모 → 자식 (데이터와 함수 전달)
- 자식 → 부모 (함수 호출)
- 부모 → 자식 (업데이트된 데이터 전달)