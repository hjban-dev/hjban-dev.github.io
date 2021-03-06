---
layout: post
title: Movie App ReactJS Routing Bonus 2
category: React
tags: [React]
comments: true
---

> 노마드코더의 ReactJS로 웹 서비스 만들기 수업을 듣고 정리합니다. <https://academy.nomadcoders.co/>

# 6 Routing Bonus

## 6.2 Building the Navigation

이번엔 Navigation Component를 만들고 모든 페이지의 상단에 떠있게 만들어봅시다.  
routes폴더에 Navigation.js를 만들고 Home과 About 두 개의 메뉴를 가진 div를 return하는 function Component를 만들겠습니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-8.jpg" alt="">
<figcaption>function Component로 구성된 Navigation.js</figcaption>
</figure>
</center>

위 코드를 실행해보겠습니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-19.gif" alt="">
<figcaption>페이지가 새로고침되어 이동되는 모습</figcaption>
</figure>
</center>

상단에 링크의 파비콘이 새로고침 되는게 보이시죠?  

위 현상은 React는 페이지가 이동할 때 다운되고, 링크가 이동된 후에 다시 실행되는 것입니다. 하지만 우리는 React로 만든 SPA페이지에서 그런 현상을 원하지 않습니다.  
그래서 우리는 a 태그의 href가 아니라 'react-router-dom'을 이용한 `Link`를 사용할겁니다.

'react-router-dom'에서 Link를 import 해오고, a 태그를 전부 Link로 변경하고, href속성은 to로 변경해주겠습니다.  

왜? 라고 물으신다면 아래 링크를 확인해보시면 됩니다. 그냥 'react-router-dom'의 문법입니다!

> [react-router의 공식페이지 구성요소 링크](https://reacttraining.com/react-router/web/guides/primary-components)

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-9.jpg" alt="">
<figcaption>a태그를 Link로 변경한 Navigation.js</figcaption>
</figure>
</center>

다시 한번 코드를 실행해보겠습니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-16.gif" alt="">
<figcaption>a태그를 Link로 변경한 Navigation.js</figcaption>
</figure>
</center>

이번에도 상단 파비콘과 url쪽을 살펴보면 페이지는 새로고침되지 않고 url과 뷰 페이지만 변경되는게 보입니다. 속도도 매우 빠르고, 새로고침 없이 React를 다운시키지도 않았습니다.  

참고로 여러분은 **Router밖에선 Link를 사용할 수 없습니다**.  
만약 여러분이 바뀌지 않을 부분, 예를 들면 footer Component 같은 부분은 Router 밖에 넣어도 되지만, Link를 사용하기 위해선 Router내부에서 실행되야 합니다.

------

## 6.3 Sharing Props Between Routes

네비게이션은 만들었고, 이제 movie를 클릭하면 movie에 대한 정보가 나오는 detail 페이지를 만들어봅시다.  

그러면 우리는 <u>카드를 클릭 했을때 그 movie에 대한 정보</u>를 받아와야겠죠?

아시다 시피 모든 Component에는 props를 넣을 수 있습니다. 우리는 이전에 만들었던 단순 태그들을 return하는 Detail Component에 <u>props를 넣고 console로 props를 확인</u>해봅시다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-12.jpg" alt="">
<figcaption>movie-detail Component에서 props확인하기</figcaption>
</figure>
</center>

router안에 들어있는 모든 route들은 react-router가 주는 props를 가지고,  
history, location, match, staticContext 4가지의 props가 react-router에 의해 넣어진 props들 입니다.  
이 props가 각각 무엇인지는 지금은 몰라도 됩니다.


> [react-router-dom의 공식문서의 Link 페이지](https://reacttraining.com/react-router/web/api/Link)

그 props를 활용하기 전에 위 링크를 확인해보면 우리는 to의 속성 부분을 객체로 변경할 수 있는 것을 확인 할 수 있습니다.  

우리의 경우는 pathname과 state를 정의해주겠습니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-10.jpg" alt="">
<figcaption>pathname과 state를 정의한 Navigation Component와 결과</figcaption>
</figure>
</center>

Home에서 Navigation을 통해 movie-detail 페이지로 들어올 때, **state를 전달하고 있는 것을 확인** 할 수 있습니다.  
위의 확인으로 `우리는 props를 전달하고 전달 받을 수 있다는 것`을 알았습니다!  
props를 movie-detail화면으로 가져올 수도 있다는 말입니다!  

이제 우리는 movie를 클릭하면 movie-detail 페이지로 이동하게 하고, 그 movie의 데이터를 movie-detail 페이지로 보낼 수 있겠죠?

먼저 Movie 카드 각각을 만들어주는 Movie Component에 가서 각 카드를 감싸는 태그를 Link로 감싸주겠습니다.

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-13.jpg" alt="">
<figcaption>pathname과 state를 정의한 Navigation Component와 결과</figcaption>
</figure>
</center>

'react-router-dom'의 Link를 사용하여 movie태그를 감싸주었고, state로 Movie Component의 props들을 전송하였습니다.  

이제 movie 카드를 클릭하면 React router는 User를 /movie-detail로 데려가고 Detail Component를 보여주면서 전달받은 props를 확인시켜줍니다. Movie Component가 Detail Component로 정보를 보내고 있는 것 입니다. 

<center>
<figure>
<img src="/assets/post-img/react/nomad_react_6-11.jpg" alt="">
<figcaption>다른 카드를 선택 했을 때의 console 결과</figcaption>
</figure>
</center>

state의 값이 각각 다른게 확인됩니다!
