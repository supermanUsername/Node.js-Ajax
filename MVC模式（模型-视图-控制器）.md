# MVC模式（模型-视图-控制器） #

## MVC模式将一个项目分成了三个部分： ##

### Model ###
- 模型
- 模型用来保存数据，和数据库进行交互
- 模型：UserModel ItemModel 。。。

                        
###  View ###
- 视图
- 视图负责将数据呈现给用户，用户通过视图来使用软件
- 视图：ejs html
             
 ### Controller ###
- 控制器
- 控制器负责调用模型处理用户的请求，并且选择相应的视图来呈现结果
- 控制器：Router
                        
## Express的项目生成器 ##

###  1.安装 ###

        npm install express-generator -g        
        C:\Users\Administrator\AppData\Roaming\npm\express -> C:\Users\Administrator\App
        Data\Roaming\npm\node_modules\express-generator\bin\express-cli.js

###  2.使用 ###
         express 项目名 -e
