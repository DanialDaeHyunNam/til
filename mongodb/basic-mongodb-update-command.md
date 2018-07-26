## Basic MongoDB Update Command

update<br>
db.<collection_name>.update(query, update, {upsert:<bool>, multi:<bool>})<br>
query : mysql에서 where절에 해당한다.<br>
update : mysql에서 set에 해당되는 부분.<br>
upsert : insert와 update의 합성어 - 데이터가 있으면 update하고, 없으면 insert를 하는 옵션.<br>
multi : 여러개의 데이터를 update하고 싶으면 true로 설정한다. (default는 false)<br>
<br>
javascript 에서 dictionary타입의 데이터는 key값은 굳이 문자열로 안해도 문자열로 들어간다.<br>
<br>
```
db.info.update(
    { subject : "python" },
    { subject : "sass", level : 2, comments : [ { name : "alice", msg : "hello" } ]}
)

db.info.update(
    { subject : "less" },
    { subject : "less", level : 1, comments : [ { name : "alice", msg : "hello" } ]},
    { upsert : true }
)
```
\$set : 특정 document의 field를 수정할 수 있습니다. (특정 field만 수정하고 싶을 때)<br>
\$unset : 특정 document의 field값을 제거할 수 있습니다.

```
db.info.update(
    { subject : "sass" },
    { $set : { level : 4 } },
    { multi : true }
)

db.info.update(
    { subject : "java" },
    { $unset : { level : 1 } }
)

// 1: true, -1 : false   

// level이 3 이하인 데이터의 레벨을 1로 수정.
// set의 경우는 1을 숫자로 인식
db.info.update(
    { level : { $lte : 3 } }, // find하던 방식으로 조건을 넣을 수 있다.
    { $set : { level : 1 } },
    { multi : 1 }
)

// level이 없는 데이터에 level을 3으로 추가
db.info.update(
    { level : { $exists : false } },
    { $set : { level : 3 } },
    { multi : 1 }
)
```

\$push : value가 배열형태로 되어있는 필드에 엘리먼트를 추가할 때 사용. <br>
\$each : 여러개의 엘리먼트를 추가할 때 사용

```
db.info.update(
    { subject : "java" },
    { $push : { comments : { name : "peter",  msg : "java is good!" } } }
)

db.info.update(
    { subject : "java" },
    { $push : {
                comments :  {   
                                $each : [
                                        { name : "peter",  msg : "python is good!" } ,
                                        { name : "jin",  msg : "css is good!" }
                                        ]
                            }
              }
    }
)
```

\$pull : 배열의 값을 제거할 때 사용<br>
\$in : 여러개의 배열 값을 선택<br>

```
db.info.update(
    { subject : "java" },
    { $pull : { comments : { name : "peter",  msg : "java is good!" } } }
)

db.info.update(
    { subject : "java" },
    { $pull : {
                comments :  {   
                                $in :  [
                                        { name : "peter",  msg : "python is good!" } ,
                                        { name : "jin",  msg : "css is good!" }
                                        ]
                            }
              }
    }
)
```
