---
layout: post
title: Node.js에서 MongoDB 사용하기
category: Nodejs
tags: [Nodejs, MongoDB]
comments: false
---

> [생활코딩 Node.js 강의](https://www.inflearn.com/course/nodejs-%EA%B0%95%EC%A2%8C-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9#) 와 KOSMO 노드JS 프로그래밍 수업을 듣고 정리합니다.  
> Node.js에서 MongoDB 사용하는 법을 알아본다  

# Node.js에서 MongoDB 사용과 메서드

[MongoDB 설치 및 명령어 포스트](https://hjban-dev.github.io/mongodb/2019/08/08/mongodb-00-mongo/)

## Mongojs 설치 및 모듈 선언 [npm mongojs 참고](https://www.npmjs.com/package/mongojs)

- 설치 `npm install mongojs --save`
  (package.json 에서 설치 확인)
- app.js에 해당 모듈 추가 
  - **const MongoClient = require('mongodb').MongoClient**
  - MongoClient : MongoDB 데이터베이스에 연결하면서 상호 작용을 처리하는 Nodejs 라이브러리
- MongoDB 서버에 대한 URL 추가 
 -  **const url = 'mongodb://localhost:27017'**  (MongoDB URL의 기본 포트 : 27017)

```javascript
const MongoClient = require('mongodb').MongoClient;
const url = 'mongodb://localhost:27017';
```

## MongoClient.connect() 사용하여 연결

MongoClient.connect() 메서드로 mongodb와 연결  
client.db() 메서드로 데이터 베이스 사용 가능

```javascript
MongoClient.connect(url, function(err, client) {
  if (err) throw err;
  // mydb 라는 데이터 베이스를 사용
  const dbMydb = client.db("mydb");
});
```

## collection 생성과 가져오기

collection() 메서드로 컬렉션을 한다.  
컬렉션이 없으면 자동 생성됨

```javascript
const collection = dbMydb.collection('dogs');
// dbMydb 데이터베이스에 컬렉션 생성 또는 가져오기
```

## collection에 데이터 추가

insertOne() 메소드를 사용하여 dogs 콜렉션에 데이터 추가

```javascript
collection.insertOne({name: 'Roger'}, (err, result) => {
  // ....
})
```

insertMany() 메서드를 사용하여 여러 항목 추가 가능  
첫 번째 매개 변수로 배열을 전달할 수 있다.

```javascript
collection.insertMany([{name: 'Togo'}, {name: 'Syd'}], (err, result) => {
  // ...
})
```

## 컬렉션 데이터 가져오기

find() 메소드를 사용하여 컬렉션에 추가 된 모든 데이터를 가져옵니다.  
추출한 데이터를 toArray()를 사용하여 배열 형태로 반환  
**매개변수 items 는 find() 의 실행 결과값이 들어있음**

```javascript
collection.find().toArray((err, items) => {
  console.log(items)
})
```

<center>
<figure>
<img src="/assets/post-img/nodejs/toarray.jpg" alt="">
<figcaption>코드 실행 결과</figcaption>
</figure>
</center>

### 특정 데이터 찾기

```javascript
collection.find({name: 'Togo'}).toArray((err, items) => {
  console.log(items)
})
```

데이터 최상단 하나만 찾기 (toArray() 생략가능)

```javascript
collection.findOne({name: 'Togo'}, (err, item) => {
  console.log(item)
})
```

## 데이터 업데이트

updateOne() 메서드 사용  
첫번째 매개변수는 필드 선택, 두번째 매개변수에 조건  

```javascript
collection.updateOne({name: 'Togo'}, {'$set': {'name': 'Togo2'}}, (err, item) => {
  console.log(item)
})
```

## 데이터 삭제

udeleteOne() 메서드 사용  
첫번째 매개변수는 필드 선택  

```javascript
collection.deleteOne({name: 'Togo'}, (err, item) => {
  console.log(item)
})
```

## 연결 종료

```javascript
client.close()
```
