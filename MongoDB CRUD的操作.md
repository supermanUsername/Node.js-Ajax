# MongoDB CRUD的操作 #


CRUD操作指对文档做create（创建、增加）、read（读取、查询）、update（修改）、delete（删除）四个操作。
 
注 ： db 为当前数据库；collection 为需插入文档的集合名。
 
## create（创建、增加） ##
 
    // 增加操作指向集合中插入一个新的文档，如果数据库中不存在该集合则会自动创建集合。
     
    db.collection.insert();// 在当前集合插入一个或多个文档
    // 在当前集合插入一个文档
    db.collection.insert({name : "孙悟空", age : 18});
    // 在当前集合插入多个文档
    db.collection.insert([{name : "孙悟空", age : 18},{name : "猪八戒", age : 18}]);
     
     
    db.collection.insertOne();// 在当前集合插入一个文档
    // nsertOne()将一个新的文档插入到集合中
    db.collection.insertOne({name : "孙悟空", age : 18});// 32位操作系统不兼容
     
     
    db.collection.insertMany();// 在当前集合插入多个文档
    // insertMany()可以将多个文档插入进集合中，它需要一个文档数组作为参数
    db.collection.insertMany([{name : "孙悟空", age : 18},{name : "猪八戒", age : 18}]);// 32位操作系统不兼容
 
 
## read（读取、查询）##
 
    db.collection.find();// 查询集合中的所有文档
    // 查询集合中的所有文档
    db.collection.find({});
 
 
    db.collection.findOne();// 查询集合中的第一个文档
    // 查询集合中的第一个文档
    db.collection.findOne({name : "孙悟空"});
 
 
    // 条件查询
    db.collection.find({name : "孙悟空"});// 查找符合条件的所有文档
 
    // 操作符查询
    db.collection.find({age : {$in : [18 , 28]});
 
    db.collection.find({age : {$eq : 18}});
 
    db.collection.find({$or:[{name:"孙悟空"},{age:18}]});
 
### 操作符(部分) ###

#### 比较操作符  ####

- $eq  匹配和指定值相等的值
- $gt  匹配大于指定值的值
- $gte 匹配大于或等于指定值的值
- $lt  匹配小于指定值的值
- $lte 匹配小于或等于指定值的值
- $ne  匹配不等于指定值的值
- $in  匹配和数组中任意值相等的值
- $nin 不匹配和数组中任意值相等的值

 
#### 逻辑操作符  ####

- $or  返回与条件数组中任意一个条件匹配的文档
- $and 返回与条件数组中所有条件匹配的文档
- $not 返回与条件表达式不匹配的文档

 
 
## update（修改） ##
 
    db.collection.update();// 修改集合中一个或多个文档(或字段)
    // 修改第一个文档字段
    db.collection.update({name : "孙悟空"},{$set: {age : 28}},{multi : false});/*{multi : false}为默认值，
                                                                                表示为不修改多个文档，
    // 修改多个文档字段                                                         可以省略不写*/
    db.collection.update({name : "孙悟空"},{$set: {age : 28}},{multi : true});/*{multi : true}为默认值，
    // 替换第一个文档                                                          表示为是修改多个文档*/
    db.collection.update({name : "孙悟空"},{name : "孙悟饭"});
 
 
    db.collection.updateOne();// 修改集合中的第一个文档字段
    // 修改集合中的第一个文档字段
    db.collection.updateOne({name : "孙悟空"},{$set: {age : 28}});// 32位操作系统不兼容
 
 
    db.collection.updateMany();// 修改集合中的多个文档字段
    // 修改集合中的多个文档字段
    db.collection.updateMany({name : "孙悟空"},{$set: {age : 28}});// 32位操作系统不兼容
 
 
    db.collection.replaceOne();// 替换第一个文档
    // 替换第一个文档
    db.collection.replaceOne({name : "孙悟空"},{name : "孙悟饭"});// 32位操作系统不兼容
 
 
###  修改操作符 ###

- $inc  为字段的值增加指定的数量
- $mul  为字段的值乘以指定的数量
- $rename  重命名一个字段
- $set  设置文档中字段的值
- $unset  从文档中删除指定的字段
- $min  限制目标字段的最小值
- $max  限制目标字段的最大值
- $currentDate  将字段设置为当前日期
- $  匹配和查询条件符合的数组中的第一个元素
- $addToSet  将数组中没有的元素添加到数组中
- $pop  删除数组的第一个或最后一个元素
- $push  将一个元素添加到数组

 
 
## delete（删除） ##
 
    db.collection.remove();// 删除多个或一个文档
    // 删除第一个文档
    db.collection.remove({name : "孙悟空"},true);// true表示只删除第一个文档
    // 删除多个文档
    db.collection.remove({name : "孙悟空"},false);/*false表示删除多个文档，
                                                   为默认值可以省略不写*/
 
    db.collection.deleteOne();// 删除第一个文档
    // 删除第一个文档
    db.collection.deleteOne({name : "孙悟空"});// 32位操作系统不兼容
 
 
    db.collection.deleteMany();// 删除多个文档
    // 删除多个文档
    db.collection.deleteMany({name : "孙悟空"});// 32位操作系统不兼容
 
 
    // 删除集合
    db.collection.drop();
 
 
    // 删除数据库
    db.dropDatabase();
 
 
 
 
 
 

### 代码英语 ###
 
create  英 [kriː'eɪt]    vt. 创造，创作；造成
read    英 [ri:d;red]    n. 阅读；读物
update  英 [ʌp'deɪt]    n. 更新；现代化
delete  英 [dɪ'liːt]    vt. 删除
collection    英 [kə'lekʃ(ə)n]    n. 采集，聚集
insert  英 [ɪn'sɜːt]    vt. 插入；嵌入
one     英 [wʌn]    num. 一；一个
many    英 ['menɪ]    adj. 许多的
find    英 [faɪnd]    vt. 查找，找到
multi   英 ['mʌltɪ]    pref. 多
replace 英 [rɪ'pleɪs]   vt. 取代，代替；替换，更换
drop    英 [drɒp]    vi. 下降；终止
databese    英 ['deɪtəbeɪs]    n. 数据库，资料库
 
