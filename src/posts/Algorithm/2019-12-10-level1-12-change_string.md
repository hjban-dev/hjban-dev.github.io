---
layout: post
title: level 1-12. 문자열을 정수로 바꾸기 (Javascript)
category: Algorithm
tags: [Algorithm, Javascript, Exercise]
comments: true
---
# level 1. 문자열을 정수로 바꾸기
> 출처 : <https://programmers.co.kr/learn/courses/30/lessons/12925>

## 문제

```
문자열 str를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.
```

### 제한사항

- str의 길이는 1 이상 5이하입니다.
- str의 맨앞에는 부호(+, -)가 올 수 있습니다.
- str는 부호와 숫자로만 이루어져있습니다.
- str는 "0"으로 시작하지 않습니다.

#### 입출력 예

str | return 
--------- | ---------
"1234" | 1234
"-1234" | -1234

입출력 예 설명  

- 예를들어 str이 1234이면 1234를 반환하고, -1234이면 -1234를 반환하면 됩니다.
- str은 부호(+,-)와 숫자로만 구성되어 있고, 잘못된 값이 입력되는 경우는 없습니다.

***

## 내가 한 풀이
```javascript
function solution(str) {
  var answer = Number(str);
  return answer;
}
```
Number() 메서드로 자료형 변형

***

## 다른사람 풀이
```javascript
function solution(str) {
  return str/1
}
```
신박. 들어온 자료형을 사칙연산으로 문자가 자동으로 파싱된다고 함

## 배운점

이 문제도 가뿐했지만 다른 사람의 풀이는 여전히 대단.
