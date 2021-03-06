---
layout: post
title: 실전형 리액트 Hooks 10가지 - useInput(useState)
category: React
tags: [React]
comments: true
---

> 노마드코더의 실전형 리액트 Hooks 10가지 수업을 듣고 정리합니다. <https://academy.nomadcoders.co/>

# 1 useState

## 1.1 useInput

useState를 사용하여 커스텀 Hooks인 useInput을 만들어보겠습니다.  
useInput은 기본적으로 input을 업데이트 합니다.  
  
useInput은 args로 initialValue를 받고, initialValue를 초기값으로 갖는 useState를 작성해주었습니다.

```javascript
const useInput = initialValue => {
  const [value, setValue] = useState(initialValue);
  return { value };
};

const App = () => {
  const name = useInput("Mr.");

  return (
    <div className="App">
      <h1>Hello </h1>
      <input placeholder="Name" {...name} />
    </div>
  );
};
```
useInput함수에서 사용자가 변화를 주기 전에 value를 return하여 args를 초기값으로 갖게 합니다.  
{...name}은 value={name.value}로도 작성할 수 있습니다.

<center>
<figure>
<img src="/assets/post-img/react/hooks/nomad_react_hooks_1.JPG" alt="">
<figcaption>코드 실행 결과</figcaption>
</figure>
</center>

이어서 useInput내부에 onChange함수를 만들어보겠습니다.

```javascript
const useInput = initialValue => {
  const [value, setValue] = useState(initialValue);
  const onChange = event => {
    console.log(event.target); // <input placeholder="name" value="Mr."></input>
  };
  return { value, onChange }; 
};
```
App 컴포넌트는 따로 수정할 필요가 없습니다. {...name}형태인 전개구문 문법으로 입력해주었기 때문입니다.

## 1.2 useInput part Two

useInput에 validator args를 추가하겠습니다. useInput은 validator가 있는지 확인하고 실행하게 합니다.

```javascript
const useInput = (initialValue, validator) => { // validator 추가
  const [value, setValue] = useState(initialValue);
  const onChange = event => {
    const {
      target: { value }
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(value); // validator 실행
    }
    if (willUpdate) {
      setValue(value);
    }
  };

  return { value, onChange };
};

const App = () => {
  const maxLen = value => value.length < 10; // maxLen 함수 선언
  const name = useInput("hj", maxLen); // maxLen을 args로 전달
  return (
    <div className="App">
      <h1>Hello</h1>
      <input placeholder="name" {...name} />
    </div>
  );
};
```

useInput을 활용하면 여러 조건들을 제어할 수 있습니다.
