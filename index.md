## 欢迎来到我的博客

以下是各个文章的目录

- [nginx服务启动](nginx/nginx服务.md)
- [mongodb](mongodb/mongodb相关.md)
- [搭建nodejs服务器环境](nodejs/搭建nodejs服务器环境.md)
- [搭建oracledb服务器环境](oracledb/搭建oracledb服务器环境.md)
- [正则验效规则](regular/正则验效规则.md)
- [程序员中英文词汇文档](Dictionary/程序员中英文词汇文档.md)




### pm2命令
     查询列表：pm2 ls                           
     启动文件：pm2 start app.js             
     重启项目：pm2 restart app              
     监听日志：pm2 logs app                 
     停止执行：pm2 stop app                 
     删除项目：pm2 delete app               
     清除日志：pm2 flush                        
     启动监听：pm2 start app.js &&  pm2 logs app
     重启监听：pm2 flush && pm2 restart app &&  pm2 logs app


### 端口查询
    netstat -tunlp                  // 用于查看端口号的进程情况
    netstat -tunlp |grep 80         // 查看80端口的情况

### linux压缩解压命令

    压缩 tar -zcvf /website2018/node_modules.tar.gz   node_modules
                压缩生成的目标文件                    被压缩的原文件
    解压 tar  zxvf /website2018/node_modules.tar.gz   node_modules
             被解压目标文件                         解压后的文件

    进入 要解压的目标文件夹，执行上面要解压的文件，并将文件进行命名

### n模块的使用
    nodejs的版本管理,几个命令就可以完成nodejs的升级操作。仅仅只有下面几个简单的步骤就可以完成：
    1、首先安装n模块别看它名字很短，用途却很大，可以用短小精悍来形容。n模块是专门用来管理nodejs版本的。这里需要全局安装，命令如：npm install -g n
    2、升级node.js到最新稳定版命令如：n stable
    没错，就这么简单！！！当然，也可以利用它升级到指定版本。比如：n v10.13.0




### 测试嵌入链接1


<video id="video" controls="" preload="none" poster="http://media.w3.org/2010/05/sintel/poster.png">
<source id="mp4" src="http://media.w3.org/2010/05/s...; type="video/mp4">
<source id="webm" src="http://media.w3.org/2010/05/s...; type="video/webm">
<source id="ogv" src="http://media.w3.org/2010/05/s...; type="video/ogg">
<p>Your user agent does not support the HTML5 Video element.</p>
</video>


### 测试嵌入链接2
   <video controls="" preload="none" poster="http://media.w3.org/2010/05/sintel/poster.png"><source src="http://media.w3.org/2010/05/sintel/trailer.mp4" type="video/mp4"><source src="http://media.w3.org/2010/05/sintel/trailer.webm" type="video/webm"><source src="http://media.w3.org/2010/05/sintel/trailer.ogv" type="video/ogg"><p>Your user agent does not support the HTML5 Video element.</p></video>









