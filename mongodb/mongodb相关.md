
#mongodb服务

  
```javascript
1.先无权限启动数据库                   /usr/local/mongodb/bin/mongod   --dbpath=/data/db --fork --logpath=/data/db/mongodb.log
2.进入数据库                           use admin
3.创建角色                             db.createRole({role:'sysadmin',roles:[],privileges:[{resource:{anyResource:true},actions:['anyAction']}]})
4.在admin中创建超级管理员              db.createUser({user:'admin',pwd:'password123',roles:[{role:'sysadmin',db:'admin'}]})
5.在主数据库下关闭数据库               db.shutdownServer();
6.有权限启动数据库                     /usr/local/mongodb/bin/mongod  --auth --dbpath=/data/db --fork --logpath=/data/db/mongodb.log
/usr/local/mongodb/bin/mongod --auth --dbpath=/data/db --fork --logpath=/data/db/mongodb.log --storageEngine wiredTiger --journal --maxConns=50000 --bind_ip 0.0.0.0

创建数据集合                           use newdb
创建普通管理员                         db.createUser({user:'userName',pwd:'password123',roles:[{role:'readWrite',db:'admin'}]});
登陆数据集合                           db.auth("userName","password123");

把指定的数据库备份到指定目录            ./mongodump -u lzt -p dgxkkg -h 127.0.0.1:27017 -d lwx -o /data/dump
```




#mongdob 聚合查询
```javascript

     var MongoClient = require('mongodb').MongoClient;
     var urla = 'mongodb://x:xxxxxx@127.0.0.1:27017/x';
     MongoClient.connect(urla,async function(err, client) {
         if(err){console.error(err);return false;}
         var a=client.collection('bbb');
         await a.remove();
         await a.insertOne({
             'name':"dd",
             array:[{name:"11"}, {name:"12"}, {name:"13"}],
             array2:[{id:"11"}, {id:"12"}, {id:"13"}]
         });

         var find=await a.find({}).toArray();
         console.log(JSON.stringify(find));
        var finda=await a.aggregate([
            {"$unwind":"$array"}, //将存在指定数组字段的数据拆分成多条
            {"$unwind":"$array2"},
            {"$match":{"array.name":"11","name":"dd"}},
            {"$project":{"array":1}}
            ]).toArray();
         console.log("finda",JSON.stringify(finda));

         /*
         打印的内容
         [{"_id":"5c3849e7c89f764a1494c190","name":"dd","array":[{"name":"11"},{"name":"12"},{"name":"13"}],"array2":[{"id":"11"},{"id":"12"},{"id":"13"}]}]
         finda [{"_id":"5c3849e7c89f764a1494c190","array":{"name":"11"}},{"_id":"5c3849e7c89f764a1494c190","array":{"name":"11"}},{"_id":"5c3849e7c89f764a1494c190","array":{"name":"11"}}]

         */
     });

   

```

|表达式 |描述 | 实例|
|---|---|---  |
|$sum                   | 计算总和。                                  |    db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])       |
|$avg                   | 计算平均值                                  |    db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])       |
|$min                   | 获取集合中所有文档对应值得最小值。              |    db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])       |
|$max                   | 获取集合中所有文档对应值得最大值。              |    db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])       |
|$pus                   | 在结果文档中插入值到一个数组中。                |    db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])                  |
|$addToSet              | 在结果文档中插入值到一个数组中，但不创建副本。    |     db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])             |
|$first                 | 根据资源文档的排序获取第一个文档数据。           |    db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])          |
|$last                  | 根据资源文档的排序获取最后一个文档数据。         |    db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])            |




### 管道的概念

    管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。
    MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。
    表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。
    这里我们介绍一下聚合框架中常用的几个操作：

    $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
    $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
    $limit：用来限制MongoDB聚合管道返回的文档数。
    $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
    $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
    $group：将集合中的文档分组，可用于统计结果。
    $sort：将输入文档排序后输出。
    $geoNear：输出接近某一地理位置的有序文档。





```javascript
var listCollections={"name":{$in:["test","test2"]}};//限制哪个表
var isA=await client.listCollections(listCollections).toArray();  查询所有表的名称和信息
```



    update 返回的部分对象取值  {result:{n:10,nModified:0,ok:1}}
    query : update的查询条件，类似sql update查询内where后面的。
    update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
    upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
    multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
    writeConcern :可选，抛出异常的级别。

    $ne不等于
    (>) 大于 - $gt
    (<) 小于 - $lt
    (>=) 大于等于 - $gte
    (<= ) 小于等于 - $lte

    Comparison
    名称 描述
    $eq    匹配等于指定值的值。
    $gt    匹配大于指定值的值。
    $gte    匹配大于或等于指定值的值。
    $in    匹配数组中指定的任何值。
    $lt    匹配小于指定值的值。
    $lte    匹配小于或等于指定值的值。
    $ne    匹配所有不等于指定值的值。
    $nin    不匹配数组中指定的任何值。
    
    
    Logical
    名称    描述
    $and    使用逻辑连接查询子句AND将返回与两个子句的条件匹配的所有文档。
    $not    反转查询表达式的效果并返回与查询表达式不匹配的文档。
    $nor    使用逻辑连接查询子句NOR将返回所有无法匹配两个子句的文档。
    $or    使用逻辑连接查询子句OR将返回与任一子句的条件匹配的所有文档。
    
    
    Element
    名称    描述
    $exists    匹配具有指定字段的文档。
    $type    如果字段是指定类型，则选择文档。
    
    
    Evaluation
    名称    描述
    $expr    允许在查询语言中使用聚合表达式。
    $jsonSchema    根据给定的JSON模式验证文档。
    $mod    对字段的值执行模运算，并选择具有指定结果的文档。
    $regex    选择值与指定正则表达式匹配的文档。
    $text    执行文本搜索。
    $where    匹配满足JavaScript表达式的文档。









```javascript


//mongodb , 批量操作

db.getCollection("a123").bulkWrite([

    {insertOne:{a:1}}

    {updateMany:{filter:{a:1},update:{$set:{a:11}},upsert:1}},
    {updateMany:{filter:{a:2},update:{$set:{a:111}},upsert:1}},
])

bulkArr.push({updateMany:{filter:filterData,update:{$set:updateData},upsert:true}});
await db_allStatisticsCount.bulkWrite(bulkArr);




{ mongodb：{$exists:false}}   //字段是否存在
db.getCollection("ykx_Configuration").find({payFor:{$exists:false}})




db.getCollection("ykx_OutboundContainerLog").aggregate([

    { $group: { _id : {

                containerNumber:"$containerNumber",
                missionCode:"$missionCode",
            }, count: { $sum : 1 } } },
    { $match: { count: { $gt : 1} } },
    {"$project": {
            _id:0,
            containerNumber:"$_id.containerNumber",
            missionCode:"$_id.missionCode",
            travelTaskNumber:1,
            loadingTaskNumber:1,

        } },

])




db.getCollection("mission").aggregate([
    {$match:{createTime:{$gt:1601481600000,$lt:1604160000000}}},
    { $group: { _id : {route:"$route"}, count: { $sum : 1 } } },
    {"$project": {
            _id:0,
            route:"$_id.route",

        } },
])

//聚合去重
db.getCollection("ykx_clientAddress").aggregate([
//{$match:{route:{$in:["西堤"]}}},
    { $group: { _id : {addressCode:"$addressCode"}, count: { $sum : 1 } } },
    { $match: { count: { $gt : 1} } },
    {"$project": {
            _id:0,
            addressCode:"$_id.addressCode"
        } },
])


//find查询时需要 {projection:{}} 对象
let  aa=await obj1.find({_id:{$in:newArr},state: {$ne:"0"}},{projection:{_id:1,orderCode:1,state:1}}).toArray();

    
    
```

