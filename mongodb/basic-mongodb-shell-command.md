## Basic MongoDB Shell Command

- Insert

```
 db.info.insert([
 {"subject" : "python", "level" : 3},
 {"subject" : "web", "level" : 1},
 {"subject" : "sql", "level" : 2},
 {"subject" : "python", "level" : 3},
 {"subject" : "web", "level" : 1},
 {"subject" : "sql", "level" : 2}
 ])
```
 - Find

```
 db.<collection_name>.find(query, projection)
 query : document를 조회할 때 조건 설정
 projection : document를 조회할 때 보여지는 필드를 설정

 db.info.find({"subject" : "python"})
```

 - 연산자 : 비교, 논리

```
 less then equal
 db.info.find({"level" : {\$lte:2}})

 \$in
 db.info.find({"subject" : {\$in:["web", "sql"]}})
```

 - 논리연산자

```
 \$or, \$and, \$not, \$nor(\$or의 반대개념)
 db.info.find( { \$and:[ { "subject" : "python" }, { "level" : {\$lte : 3} } ] } )

 db.info.insert([
 { "subject":"r", "level":3, "comments": [{"name":"jin","msg":"bad"}, {"name":"alice","msg":"hi"}] }, { "subject":"java", "level":1, "comments": [{"name":"po","msg":"check"}] },
 { "subject":"javascript", "comments": [{"name":"jin","msg":"nice"}] },
 { "subject":"html", "level":3, "comments": [] },
 { "subject":"css", "level":1, "comments": [{"name":"alice", "msg":"hello"}] },
 { "subject":"python", "level":2, "comments": [{"name":"alice", "msg":"hello"}] },
 { "subject":"python", "level":5, "comments": [{"name":"jin","msg":"nice"}] }
 ])
```

 - \$where

```
 db.info.find( { \$where : "this.comments.length >= 1" } )
```

 - \$elemMatch

```
 db.info.find( { "comments" : { \$elemMatch : { "name" : "alice" } } } )
```

 - \$exists

```
 db.info.find( { "level" : { \$exists : false } } )
```

 - Projection

```
 설정을 할 때 true, false : \_id 값은 따로 설정을 안하면 true
 db.info.find( {}, { "\_id" : false, "level" : false } )
 true를 넣으면 나머지는 자동으로 false로 지정되지만, \_id는 컬럼은 예외다. 그래서 보고싶지않은 경우엔 따로 "\_id" : false를 추가 해줘야한다.
 마찬가지로 false를 넣으면 나머지는 자동으로 true로 지정됨.
 db.info.find({}, { "subject" : true, "comments" : true })
```

- \$slice : 도큐먼트를 읽어올 때 출력 개수를 설정

```
db.info.find( {}, { comments : { \$slice : 1}} )
```

- Find method sort, limit, skip

```
 1 : 오름차순, -1 : 내림차순
 db.info.find( {} ).sort( { "level" : 1 } )

 레벨로 Sorting하고, 레벨이 같으면 id 값으로 Sorting한다.
 db.info.find().sort({ "level" : -1, "\_id" : 1 })
```

 - limit

```
 db.info.find().limit(3)

 skip 숫자만큼의 개수를 위에서부터 skip하고 가져온다
 db.info.find().skip(2)

 아래의 경우는 mysql에서 limit 2, 2랑 같은 의미
 db.info.find().skip(2).limit(2)
```

- function : 자바스크립트 문법으로 함수 작성이 가능하다.

```
var showSkip = function(start){
    return db.info.find().skip(start)
}

var showLimit = function(end){
    return db.info.find().limit(end)
}

function findAll(){
    return db.info.find()
}

var showPage = function(page, block){
    var x = (page - 1)* block;
    return db.info.find().skip(x).limit(block)
}

showSkip(2)
showLimit(3)
findAll()
showPage(2, 3)
```
