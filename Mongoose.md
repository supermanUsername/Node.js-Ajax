# Mongoose #

Mongoose是一个对象文档模型（ODM）库，它对Node原生的MongoDB模块进行了进一步的优化封装，并提供了更多的功能。而Mongoose就是一个让我们可以通过Node来操作MongoDB的模块。在大多数情况下，它被用来把结构化的模式应用到一个MongoDB集合，并提供了验证和类型转换等好处。
    
    
## Mongoose好处所在 ##
-   可以为文档创建一个模式结构（Schema）。
-   可以对模型中的对象/文档进行验证。
-   数据可以通过类型转换转换为对象模型。
-   可以使用中间件来应用业务逻辑挂钩。
-   比Node原生的MongoDB驱动更容易。
      
      
## Mongoose中的核心对象 ##
      
### Schema ###
Schema对象定义约束了数据库中的文档结构。

### Model ###
Model对象作为集合中的所有文档的表示，相当于MongoDB数据库中的集合collection。

### Document ###
Document表示集合中的具体文档，相当于集合中的一个具体的文档。
        
        
## Mongoose的使用 ##
    
### 安装Mongoose ###
  npm install mongoose


### 加载Mongoose ###
  var mongoose = require("mongoose");


### 连接MongoDB ###
  mongoose.connect("mongodb://地址")

  地址格式：mongodb://ip地址:端口号/数据库
  例子：mongodb://127.0.0.1:27017/mg_test


### 断开连接断开连接 ###
  mongoose.disconnect();


#### connection ####

一旦连接了MongoDB数据库，底层的Connection对象就可以通过mongoose模块的conection属性来访问。

connection对象是对数据库连接的抽象，它提供了对象连接、底层的Db对象和表示结合的Model对象的访问。

并且可以对connection对象上的一些事件进行监听，来获悉数据库连接的开始与端开。

比如，可以通过open和close事件来监控连接的打开和关闭。
    
    
## 使用MongoDB操作数据库 ##
    
### 模式对象（Schema） ###
    
使用Mongoose必须定义模式。
        
模式为集合中的文档定义字段和字段类型。

如果你的数据是被结构化成支持模式的，这是非常有用的。

简单来说，模式就是对文档的约束，有了模式，文档中的字段必须符合模式的规定。否则将不能正常操作。

模式为集合中的文档定义字段和字段类型。

对于在模式中的每个字段，你都需要定一个特定的值类型。受支持的类型如下：
- String字符串类型
- Number数字类型
- Boolean   布尔类型
- Array 数组类型
- Buffer缓冲区类型
- Date  日期类型
- ObjectId或Oid对象ID类型
- Mixed混合使用类型
  
需要为你计划使用的每个不同的文档类型都定义一个模式。

#### 创建模式对象 ####

     // 引入mongoose模块
    var mongoose = require("mongoose");
    
    // 调用mongoose对象中Schema方法为一个构造函数保存到变量中
    var Schema = mongoose.Schema;
    
    // 定义一个构造函数的事例对象限定数据类型
    var SchemaObj = new Schema({
     userName : {
       type : String,// 限定为字符串类型
       unique : true // 限定唯一性
     }，
     password ： String，
     email : String，
     date ： {
       type ： Date，// 限定为日期类型
       default ： Date.now // 默认值，如果为设定则为默认值
     }
    });
        
        
### 模型对象（Model） ###
        
一旦定义好了Schema对象，就需要通过该Schema对象来创建Model对象。
  
一旦创建好了Model对象，就会自动和数据库中对应的集合建立连接，以确保在应用更改时，集合已经创建并具有适当的索引，且设置了必须性和唯一性。
  
Model对象就相当于数据库中的集合，通过Model可以完成对集合的CRUD操作。
  
#### 定义模型对象需要使用mongoose的model()方法，语法如下： ####

    var Model = mongoose.model("user" , SchemaObj);
    
    /*model(name, [schema], [collection] , [skipInit])
      name
      参数相当于模型的名字，以后可以同过name找到模型。
      schema
      是创建好的模式对象。
      collection
      是要连接的集合名。
      skipInit
      是否跳过初始化，默认是false。*/
  
一旦把一个Schema对象编译成一个Model对象，你就完全准备好开始在模型中访问、添加、删除、更新和删除文档了。
  也就是说有了模型以后我们就可以操作数据库了。
  
  
模型对象的方法
  
- remove(conditions, callback) 删除满足条件的第一个文档或所有文档

- deleteOne(conditions, callback) 删除满足条件的第一个文档

- deleteMany(conditions, callback) 删除满足条件的所有文档

- find(conditions, projection, options, callback) 查询满足条件的所有文档

- findById(id, projection, options, callback) 根据id值查询文档

- findOne(conditions, projection, options, callback) 查询满足条件的第一个文档

- count(conditions, callback) 返回查询到结果的数量

- create(doc, callback) 创建一个文档并将其插入到数据库中

- update(conditions, doc, options, callback)修改满足条件的第一个文档或所有文档

  
### 创建文档对象（Document） ###

     var DocumentOdj = new Model({
     userName : "孙悟空"， 
     password ： "123456"，
     email : "123@123.com"
      });

通过Model对数据库进行查询时，会返回Document对象或Document对象数组。
  
Document继承自Model，代表一个集合中的文档。
  
Document对象也可以和数据库进行交互操作。
  
Document对象的方法
  
- update(update,[options],[callback]) 修改当前的文档

- save([callback]) 将文档保存到数据库中

- remove([callback]) 清除当前的文档
