# WebStorm操作mongodb数据库 #

利用mongoose模块实现WebStorm对mongodb数据库的操作。模块化操作分为：主模块 index. js、连接模块 connect.js、模型模块 model.js
    
    // 下载mongoose模块及添加依赖  - npm install mongoose --save
    
## 主模块 index. js ##
    // 引入connect模块 连接mongodb数据库
    require("./connect_mongodb/connect");//connect模块保存到同一目录下connect_mongodb文件夹中
    
    // 引入model模块
    var Model = require("./Schema_model/model");//model模块保存到同一目录下Schema_model文件夹中
    
    // 使用model方法create添加文档
    Model.create({
    username : "孙悟空",
    password : "111111",
    email : "123@123.com"
    },function(err){
    if(!err){
    console.log("成功插入");
    }
    });
    
    
## 连接模块 connect.js ##
    // 引入mongoose模块
    var mongoose = require("mongoose");
    
    // 连接mongodb数据库
    //  连接路径 "mongodb://自计算机IP：端口号（默认27017，可省略不写）/数据库名"
    mongoose.connect("mongodb://127.0.0.1:27017/mg_test");
    
    // 监听连接状态绑定一个open事件
    mongoose.connection.once("open",function(){
    console.log("成功连接mongodb数据库");
    });
    
    
## 模型模块 model.js ##
    // 引入mongoose模块
    var mongoose = require("mongoose");
    
    // 调用mongoose对象中Schema方法为一个构造函数保存到变量中
    var Schema = mongoose.Schema;
    
    // 定义一个构造函数的事例对象限定数据类型
    var SchemaObj = new Schema({
    username : {
    type : String,
    unique : true
    },
    password : String,
    email : String,
    date : {
    type : String,
    default : Date.now
    }
    });
    
    // 定义模型
    var model = mongoose.model("test",SchemaObj);
    // "test"参数相当于模型的名字(集合的名字)，SchemaObj参数为限定事例对象
    
    // 暴露模型外部可以引入
    module.exports = model;
    
    
    
    

###  代码英语 ###
    
mongoose    英 ['mɒŋɡuːs]
install    英 [ɪnˈstɔ:l]    vt. 安装
save    英 [seɪv]    vt. 保存
require    英 [rɪ'kwaɪə]    vt. 需要；要求；命令
create    英 [kriː'eɪt]    vt. 创造，创作；造成
open      英 ['əʊp(ə)n]    vt. 公开；打开
Schema    英 ['skiːmə]    n. [计] 模式
Model    英 ['mɒdl]    n. 模型
connect    英 [kə'nekt]    vt. 连接；联合；关连
unique    英 [juː'niːk]    [数] 唯一的，独一无二的
default    英 [dɪ'fɔːlt; 'diːfɔːlt]    n. 系统默认值
module    英 ['mɒdjuːl]    n. [计] 模块
exports    英 ['ekspɔ:rts]    n. 输出额

    