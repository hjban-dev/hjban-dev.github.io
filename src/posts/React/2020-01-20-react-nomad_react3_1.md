---
layout: post
title: Movie App ReactJS State 1
category: React
tags: [React]
comments: true
---

> 노마드코더의 ReactJS로 웹 서비스 만들기 수업을 듣고 정리합니다. <https://academy.nomadcoders.co/>

# 3 State

## 3.0 Class Components and State

state가 중요한 이유는 보통 **동적 데이터**와 함께 작업할 때 만들어지기 때문입니다. 동적 데이터는 갑자기 생기고, 사라졌다가 다시 변경되는 데이터들을 말합니다.

전에 만들었던 Food Component는 지우고, function Component 만들어져 있던 App Component를 class Component로 변경해봅시다.

class Component의 선언은 `class App extends React.Component` 입니다.  
**React.Component를 기반으로 class 형태인 App Component를 만들겠다는 의미**입니다.
위 선언 작업은 class Component의 필수 단계이고, 선언 후엔 React.Component의 많은 부분들을 class Component를 구현할 때 사용할 수 있습니다.  

우리는 React.Component를 사용하여 App Component를 생성한다고 했고, 똑똑한 React의 특징 중 하나는 **React가 class component를 만나면 자동으로 render method 실시**한다는 것 입니다.

그래서 class로 구성된 App Component는 render method를 실행할 것 입니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_4-2.jpg" alt="">
<figcaption>App Component가 render method 실행</figcaption>
</figure>
</center>

## 3.1 All you need to know about State

render method가 실행된다는 것을 확인했으니, state를 변경해봅시다!  
class 방식이니 this를 사용해서 변경하면 될 것 같죠? React는 Javascript언어를 사용한다고 했으니, add function과 minus function을 만들어봅시다. add function과 minus function을 만들고 그 안엔 **this.state.count**을 사용했습니다. 그리고 각각의 버튼에 함수를 연결해줍니다!  

button은 내부에서 onClick으로 {this.add}으로 add() 호출했습니다. ()를 쓰지 않는건 즉시 호출이 아니고 클릭 할때 호출이라 ()를 쓰지 않았습니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_4-4.jpg" alt="">
<figcaption>작동하지 않는 모습</figcaption>
</figure>
</center>

엥... •́︿•̀ ...일단 위 이미지의 Warning 텍스트를 해석하자면.  
state를 직접적으로 바꾸지 말고, setState()를 사용하세요  

먼저...우리에게 무슨 문제가 있는지 확인해봅시다..!   
add 함수 내부에서 this.state.count를 변경한다. 맞게 쓴 것 같은데 실행이 안되는 이유는 무엇일까요?  

흠...state는 변경 되고 있는데 render fucntion은 실행되지 않는것 같네요. 우리는 state가 변경 될 때마다 React가 render fucntion을 실행해야 된다고 생각하는데요??

여기서 우리가 알아야 할 것은 React는 setState function을 호출해야 state가 변경됐다는 것을 감지합니다. 또한 변경 된 state를 보여줘야 한다고 생각하고 rerender를 실행합니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_4-3.jpg" alt="">
<figcaption>state.count를 setState로 변경</figcaption>
</figure>
</center>

버튼을 클릭할 때 마다 render method를 잘 실행하는 것을 확인했습니다.

정리하자면 Component에는 data를 넣을 공간이 있습니다. 그리고 그 데이터는 변경될 수도 있습니다. 우리는 그러한 데이터를 state라고 말합니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_4-5.jpg" alt="">
<figcaption>state.count를 setState로 변경</figcaption>
</figure>
</center>

this.state를 쓰는 방법도 좋지 않기 때문에 minus 함수안에 current라는 변수를 넣어서 current.count를 변경하는 방법으로 변경했습니다.
**this.state를 변경하는 것은 좋지 않습니다.**
