## 欢迎来到我的博客

以下是各个文章的目录


- linux压缩解压[>>>](nginx/nginx.md)
- mongodb服务启动[>>>](nginx/nginx.md)
- nginx服务启动[>>>](nginx/nginx.md)
- n模块的使用[>>>](nginx/nginx.md)
- 搭建nodejs服务器环境[>>>](nginx/nginx.md)
- 搭建oracledb服务器环境[>>>](nginx/nginx.md)
- 证照验效规则[>>>](nginx/nginx.md)
- mongodb聚合查询[>>>](nginx/nginx.md)
- 程序员中英文词汇文档[>>>](nginx/nginx.md)




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
