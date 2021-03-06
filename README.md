# [1] 몽고디비 학습하기

## 1) 몽고디비 유래

### 1. Humongouse : 휴몽고스, 거대한

## 2) 다운로드

### 1. https://mongodb.com 에서 운영환경에 맞게 다운로드 하면됩니다.

### 2. Program Files/MongoDB/Server/3.2/bin 환경변수를 설정한다.

## 3) data, log 폴더 생성

### 1. 데이터 폴더 : C:\Program Files\MongoDB\data

### 2. 로그 폴더 : C:\Program Files\MongoDB\log

## 4) MongoDB 실행

- 서버를 실행시킬때 데이터 폴더 경로를 꼭 지정해줘야 한다

### 1. mongod.exe --dbpath "C:\Program Files\MongoDB\data"

or

### 2. mongod --dbpath "C:\Program Files\MongoDB\data"

## 5) 몽고디비 자동 실행을 위한 설정

### 1. mongod.cfg 파일 만들기

<pre>
<code>
#데이터베이스 폴더
dbpatch = C:\Program Files\MongoDB\data<br/>
#mongod 포트
port = 27017<br/>
#로그파일
logpath = C:\Program Files\MongoDB\logs\mongo.log<br/>
#웹 관리 사용
rest = true<br/>
</code>
</pre>

### 2. 윈도우 서비스 등록하기

- "C:\Program Files\MongoDB\Server\4.2\bin\mongod.exe" -f "C:\Program Files\MongoDB\mongod.cfg" -install

## 6) 접속 및 확인

1. mongo
2. show dbs
3. use dbname
4. show tables (테이블 컬렉션)
5. db.TABLE.find().pretty()

# [2] MongoDB 개념과 RDBMS 비교

1. 대용량 빅 데이터에 적합한 NoSQL 데이터 베이스입니다.
2. NoSQL 데이터 베이스 중 사용 인지도 1위이다.
3. 구글, 페이스북, 포스퀘어, 이베이 등 주요 대기업 에서 사용

## NoSQL이란?

1. SQL = Structured Query Language (구조적 질의 언어)
2. NoSQL = No Structore Query Language (구조가 없는 질의 언어)

- 즉 table(Collection) 에서 스키마를 가지고 있지 않음
- 지정된 데이터 형식이 없고 넣고 싶은 데이터 형식을 마음대로 넣을 수 있다.

## Collection 과 Documente 란?

1. RDBMS = 테이블, 데이터(Row)
2. MongoDB = Collection, Document

## RDBMS Table의 구조

1. RDBMS의 테이블은 스키마를 가지고 있고 고정된 구조 이다. (SQL)

- select \* from g5;
- select CU.userName, G.channelId from Channel_User as CU
  join Group as G on CU.groupId = G.id
  where CU.userId = 3
- N : M 의 경우에는 테이블이 하나더 생성된다.

## MongoDB의 구조

1. 테이블을 생성하지 않아도 insert하면 테이블이 바로 생성된다.
2. 여러개의 테이블 구조를 배열 형태로 하나의 컬렉션으로 관리할 수 다. (데이터를 읽을 때 join 하는 구조가 아니라 데이터를 생성할 때 join을 하게 된다.)
3. 고정된 스키마로부터 구애 받지 않고 자유로운 문서 지향 데잍베이스 이다.
4. 다양한 타입지원 : String, Integer, Boolean, Arrays, Timestamp, Data, Object등 여러 데이터 타입을 지원한다.
5. 읽기 쓰기 효율을 높이고 자동으로 장애 조치를 하고 확장이 용이함 (특별한 경우를 제외하고 오류가 잘안남)
6. 여러 서버에 분산 저장 및 확장이 용이하며(Sharding - 파편화), 방대한 데이터 처리가 (빅데이터) 빠르다는 장점이 있다.

- mongo
- show dbs : 디비 목록보기
- use dbname : 디비로 접속 하기
- show tables : 테이블 목록 보기
- db.g5_geonil.find().pretty() : 테이블 내용 보기
  <pre>
  <h1>insert 하는 방법</h1>
  <ul>
  <li>입력 하는 데이터 틀에 제약없이 막 넣을 수 있다.</li>
  </ul>
  <code>
  #현재의 데이터 베이스 db 로 접근이 가능하다.
  db.g5_geonil.insert({
    "user_id":1,
    "user_name":"geonil",
    "subjects":[
      {
        "title":"수학",
        "score":10
      },{
        "title":"국어",
        "score":9
      },{
        "title":"영어",
        "score":10
      },
    ],
    "hit":1000
  });
  </code>
  </pre>

# [3] Robomongo 관리툴 사용하기

## 1) 관리툴의 장점

1. 난해한 구조인 json 형태의 데이터를 일목요연 하게 보여준다.
2. 컬렉션, 도큐먼트의 관리가 쉽다.
3. 단점 : 한글 지원이 정상적으로 되지 않는다 그렇기 떄문에 다른 에디터에서 작성된 데이터를 넣는 방법이 있다.

## 2) 원격서버에 접속하는 방법

1. SSH 텝에서 - Use SSH tunnel 을 이용

## 3) 좌측 메뉴

1. 서버의 상태
2. 버전확인
3. show log를 통한 기동로그 확인.

## 4) 데이터를 입력하는 방법

1. insert 명령어 or tool에서 insert document로 직접 데이터를 입력한다.

# [4] DataBase와 Collection(table) 관리

## 데이터 베이스 명령어

1. 컬렉션을 생성할 시점에 데이터 베이스가 생성이된다.
2. use database 이름 : 해당 디비가 없다고 하더라도 데이터 베이스로 접근이 가능하다.
3. db.createCollection("test")
4. db.tablename.drop() : 데잍 베이스가 지워진다.
5. 해당 db에 테이블(컬렉션)이 다 사라지면 데이터 베이스가 자동으로 사라진다.

## Robo를 이용해서 데이터베이스 생성 및 컬렉션 관리해보기

# [5] find()를 통한 조회

## 1. 학습을 위한 컬렉션 생성하기

   <pre>
   <code>
   db.getCollection('board').insert(
   [
   	{
   		"idx":1,
   		"subject":"Board title 1",
   		"content":"This is content 1",
   		"name":"Kim",
   		"hits": 5,
   		"date":"2016-11-10"
   	},
   	{
   		"idx":2,
   		"subject":"Board title 2",
   		"content":"This is content 2",
   		"name":"Kang",
   		"hits": 10,
   		"date":"2016-11-10"
   	},
   	{
   		"idx":3,
   		"subject":"Board title 3",
   		"content":"This is content 3",
   		"name":"Lee",
   		"hits": 15,
   		"date":"2016-11-10"
   	},
   	{
   		"idx":4,
   		"subject":"Board title 4",
   		"content":"This is content 4",
   		"name":"Park",
   		"hits": 20,
   		"date":"2016-11-11"
   	},
   	{
   		"idx":5,
   		"subject":"Board title 5",
   		"content":"This is content 5",
   		"name":"Jang",
   		"hits": 25,
   		"date":"2016-11-11"
   	}
   ]
   )

</code>
</pre>

## 2. 기본 Equal(=) 조회

- select \* from board where = 'Kim' (SQL)
- db.board.find({"name":"Jang"})
- db.getCollection.find({"name":"Jann"})
- db.table's name.findOne({"name":"Jang"}) : 하나만 찾을 경우 [sql에서는 limit = 1]
- db.board.find({"date":"2016-11-10","name":"Kang"}) : AND 조건을 줄경우

## 3. And 와 Or 조건으로 검색하기

- db.board.find({\$or:[{"date":"2016-11-10"},{"name":"Kang"}]})
- db.board.find({\$and:[{"date":"2016-11-10"},{"name":"Kang"}]})
- db.board.find({$and:[{"date":"2016-11-10"},{$or:[{"name":"Kang"},{"name":"Jang"}]}]}) : and 와 or 조건 같이 사용하기

## 4. like 조건 : [ Sql ] : where field like '%a%'<br/>

### 4-1 '%a%': a 가 들어가는 모든 문자열<br/>

- [1] db.board.find({"name":/a/}) : 정규표현식을 사용한다.
- [2] db.board.find({"name":{\$regex:'a'}})

### 4-2 '%a: a 로 끝 나는 모든 문자열

- [1] db.board.find({"name":/a\$/}) : 정규표현식을 사용한다.

### 4-3 'a%': a 로 시작하는 모든 문자열

- [1] db.board.find({"name":/^a/}) : 정규표현식을 사용한다.

## 5. 부등호 검색 : [ Sql ] : where hit > 10 { $gt | $lt | $gte | $lte | \$ne : "조건"}

- db.board.find({"hits":{\$gt:10}})
- db.board.find({"hits":{\$lt:10}})
- db.board.find({"hits":{\$gte:10}}) : e를 붙여서 사용한다. >= 10
- db.board.find({"hits":{\$ne:10}}) : e를 붙여서 사용한다. != 10
- db.board.find({
  $and:[ {"hits":{$gt:10}}, {"hits":{\$lt:25}} ]
  })

## 6. Exist 있는지 없는지 {\$exists:"조건"}

- 테스트 데이터 추가
- db.board.insert(
  {
  "idx":6,
  "subject":"Board title 6"
  "content":"This is content 6",
  "hits":6,
  "date:"2016-11-10"
  }
  )
- db.board.find({"name":{\$exists:true}]}})

## 7. 테스트 해보기

- and 와 or 조건은 배열로 조건 케이스들을 넣어주고, 조건을 만들 때는 객체 형태로 만든다.
- db.board.find({
  $or:[{$and:[{"date":"2016-11-10"},{"name":/e/}]}, {"hits":{\$gte:20}}]
  })

# [6] find() 고급 조회, sort(), limit(), skip() 등

## 1. sort() 정렬

- db.board.find().sort({"hits":1}) : 오름차순
- db.board.find().sort({"hits":-1}) : 내림차순
- db.board.find({"name":{\$exists:true}}).sort({"date":-1,"hits":-1}) : 중복 sort 조건

## 2. limit() 제한

- db.getCollection('board').find().limit(1)
- db.board.find().sort({"name":1}).limit(4)

## 3. skip() 건너뛰기, 0부터 시작

- db.board.find().skip(1) : 0이면 전부 다가져옵니다.

## 4. distinct 구분하기 Group By 중복을 하나로 그룹진 배열리턴

- db.board.distinct("date")

## 5. 사용해보기

- db.board.find({$and:[{"hits":{$gte:5}}, {"hits":{\$lte:15}}]}).sort({"hits":-1}).skip(1).limit(2)

# [7] Insert(), update() , remove() 데이터 처리

## 1. insert

- db.user.insert({
  "name":"Gi",
  "age":20
  }) : 1건 삽입
- db.user.insertOne({
  "name":"bob",
  "age":11,
  "status":"G"
  })
- db.user.insert([
  {
  "name":"hong",
  "age":100,
  "status":"A"
  },{
  "name":"kin",
  "age":73,
  "status":"B"
  },{
  "name":"lee",
  "age":23,
  "status":"C"
  }
  ]) : 다수건 삽입
- db.user.insertMany([
  {
  "name":"hong",
  "age":100,
  "status":"A"
  },{
  "name":"kin",
  "age":73,
  "status":"B"
  },{
  "name":"lee",
  "age":23,
  "status":"C"
  }
  ])

## 2. update : [Sql] update table set name="Lee", age="30" where name="lee"

### 2-1. 한 건 업데이트

- db.user.update({
  "status":"C"
  },{
  "status":"C",
  "name":"lee",
  "age":30
  })
- db.user.updateOne({
  "name":"Suzy",
  },{\$set:{
  "name":"Suzy",
  "age":28,
  "status":"S10"  
  }});

### 2-2. insert and update : 있으면 업데이트를하고, 없으면 만들어라

- db.user.update({
  "name":"min"
  },{
  "name":"min",
  "age":22,
  "status":"SS"
  },{
  upsert:true // update and insert 하겠다.
  })

### 2-3. 여럿건 업데이트

- db.user.updateMany({
  "name":"hong"
  },{\$set:{
  "name":"Home",
  "age":44,
  "status":"FF"
  }})
  - db.user.update({
    "name":"hong"
    },{\$set:{
    "name":"Home",
    "age":44,
    "status":"FF"
    }},{multi:true}>)

## 3. remove 데이터 삭제

### 3-1. 모든데이터 삭제

- db.user.remove({})

### 3-2. 특정 한 개 삭제

- db.user.deleteOne({
  "name":"lee"
  })

### 3-3. 특정 데이터 모두 삭제

- db.user.deleteMany({
  "name":"lee"
  })
- db.user.remove({
  "name":"lee"
  })

# [8] Group 관련 함수 사용하기

- Group 함수 사용을 위한 데이터 삽입
- Robo에서 실행 시키면 됩니다.
  <pre>
  <code>
  db.getCollection('board2').insert(
  [
    {
      title: 'MongoDB Overview',
      description: 'MongoDB is no sql database',
      by_user: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 100
    },
    {
      title: 'NoSQL Overview',
      description: 'No sql database is very fast',
      by_user: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 10
    },
    {
      title: 'Neo4j Overview',
      description: 'Neo4j is no sql database',
      by_user: 'Neo4j',
      url: 'http://www.neo4j.com',
      tags: ['neo4j', 'database', 'NoSQL'],
      likes: 750
    }
  ]
  )
  </code>
  </pre>

## 1. Group 해보기

- 필드를 지칭하기 위해서는 $기호를 사용한다 ex) $name 이름 컬럼

### 1-1 count

1. \_id 컬럼을 \$by_user값으로 그룹한다.
2. 두 번째 인자 값으로 그룹의 결과를 보여줄 것이다.
3. \$sum 함수를 사용해서 그룹 지을때 값을 어떤 식으로 표현할 지 보여준다.
4. 다음과 같은경우는 필드를 1씩 판단하여 갯 수를 나타낸다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",count:{
  $sum:1
  }
  }}
  ])

### 1-2 sum

1. \_id 컬럼을 \$by_user값으로 그룹하며
2. 그룹할 때 \$like 컬럼의 값을 함친다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",
  sum_count:{$sum:"$likes"}
  }}
  ])

### 1-3 average

1. \_id 컬럼을 \$by_user값으로 그룹하며
2. 그룹할 때 \$like 컬럼의 값을 함친다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",
  avg_cnt:{$avg:"$likes"}
  }}
  ])

### 1-4 min

1. \_id 컬럼을 \$by_user값으로 그룹하며
2. 그룹할 때 \$like 컬럼의 값을 함친다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",
  min_cnt:{$min:"$likes"}
  }}
  ])

### 1-5 max

1. \_id 컬럼을 \$by_user값으로 그룹하며
2. 그룹할 때 \$like 컬럼의 값을 함친다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",
  max_cnt:{$max:"$likes"}
  }}
  ])

### 1-6 first

1. \_id 컬럼을 \$by_user값으로 그룹하며
2. 그룹할 때 \$like 컬럼의 값을 함친다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",
  first:{$first:"$likes"}
  }}
  ])

### 1-6 last

1. \_id 컬럼을 \$by_user값으로 그룹하며
2. 그룹할 때 \$like 컬럼의 값을 함친다.

- db.board2.aggregate([
  {$group:{
  _id:"$by_user",
  last:{$last:"$likes"}
  }}
  ])

# [9] 페이징 처리 기법 배우기

- 페이이징 학습을 위한 데이터 삽입
  <pre>
  <code>
  db.board.insert(
     [
       { subject: "Board title 1" },
       { subject: "Board title 2" },
       { subject: "Board title 3" },
       { subject: "Board title 4" },
       { subject: "Board title 5" },
       { subject: "Board title 6" },
       { subject: "Board title 7" },
       { subject: "Board title 8" },
       { subject: "Board title 9" },
       { subject: "Board title 10" },
       { subject: "Board title 11" },
       { subject: "Board title 12" },
       { subject: "Board title 13" },
       { subject: "Board title 14" },
       { subject: "Board title 15" },
       { subject: "Board title 16" },
       { subject: "Board title 17" },
       { subject: "Board title 18" },
       { subject: "Board title 19" },
       { subject: "Board title 20" },
     ]
  )

</code>
</pre>

## 9-1 skip과 limit을 사용하여 페이징

- 페이징 전략
  <pre>
  <code>
  #1 0부터 시작해서 5개만 가져오겠다. 0 ~ 4
  // start_cnt = {page-1} \* 5;
  // 1page: 0
    db.board.find().skip(0).limit(5)
  #2 5부터 시작해서 5개만 가져오겠다. 5 ~ 9
  // start_cnt = {2-1} \* 5;
  // 2page: 5
    db.board.find().skip(5).limit(5)
  #3 10부터 시작해서 5개만 가져오겠다. 5 ~ 9
  // start_cnt = {3-1} \* 5;
  // 3page: 15
    db.board.find().skip(10).limit(5)
  </code>
  </pre>

# [10] Index 생성 및 삭제

- index 학습을 위해서 데이터를 입력해줍니다.
  <pre>
  <code>
  db.board.insert(
     [
       { subject: "Board title 1", "name":"Kim 1", "hits":10 },
       { subject: "Board title 2", "name":"Kim 2", "hits":10 },
       { subject: "Board title 3", "name":"Kim 3", "hits":10 },
       { subject: "Board title 4", "name":"Kim 4", "hits":10 },
       { subject: "Board title 5", "name":"Kim 5", "hits":10 },
       { subject: "Board title 6", "name":"Kim 6", "hits":10 },
       { subject: "Board title 7", "name":"Kim 7", "hits":10 },
       { subject: "Board title 8", "name":"Kim 8", "hits":10 },
       { subject: "Board title 9", "name":"Kim 9", "hits":10 },
       { subject: "Board title 10", "name":"Kim 10", "hits":10 },
       { subject: "Board title 11", "name":"Kim 1", "hits":10 },
       { subject: "Board title 12", "name":"Kim 2", "hits":10 },
       { subject: "Board title 13", "name":"Kim 3", "hits":10 },
       { subject: "Board title 14", "name":"Kim 4", "hits":10 },
       { subject: "Board title 15", "name":"Kim 5", "hits":10 },
       { subject: "Board title 16", "name":"Kim 6", "hits":10 },
       { subject: "Board title 17", "name":"Kim 7", "hits":10 },
       { subject: "Board title 18", "name":"Kim 8", "hits":10 },
       { subject: "Board title 19", "name":"Kim 9", "hits":10 },
       { subject: "Board title 20", "name":"Kim 10", "hits":10 },
     ]
  )

</code>
</pre>

### 10-1 인덱스 생성해보기

- db.board.createIndex({subject:1}) : 인텍스 생성
- db.board.getIndexes() : 인덱스 확인
- db.board.dropIndex({subject:1}): 인덱스 드랍하기
- db.board.createIndex({subject:1, hits:-1}) : 한 번에 여러 인덱싱
- db.board.dropIndex({subject:1, hits:-1})
- db.board.createIndex({subject:1},{unique:true}) : 유니크 인덱스 사용하기
