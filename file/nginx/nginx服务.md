
    启动服务:   /usr/local/nginx/sbin/nginx
    重启服务:   /usr/local/nginx/sbin/nginx  -s  reload
    停止服务:   /usr/local/nginx/sbin/nginx  -s  stop
    编辑配置:   vi  /usr/local/nginx/conf/nginx.conf
    查看配置:   cat  /usr/local/nginx/conf/nginx.conf

```nginx
按键 i 进入编辑模式
完成编辑后,先按 Esc 键 然后同时按 Shift 和 ：号键 然后 wq 保存（w 写入 q 推出） （q!立即退出）

      <hr>
          proxy_pass   设置动态文件端口，唯一           //http://127.0.0.1:8080;

          #开发版
          server{
          listen 80;                                    #统一用 80 端口
          server_name dev.abcde.cn;                     #这里配置二级域名
          client_max_body_size 100M;
          charset utf-8;
          location ~* ^.+.(html)$ {
          proxy_pass http://127.0.0.1:8888;            #这里指向代码中监听的端口
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header REMOTE-HOST $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      }
          location ~* ^.+.(htm|js|css|ico|gif|bmp|jpg|jpeg|png|swf|apk|xls|xlsx|woff|ttf|eot|otf|svg|json|manifest|mp3|apk)$ {
          root   /website/dev/web;                  #这里指向开发版文件夹
          access_log off;
          expires 8h;
      }
          location /{
          proxy_pass http://127.0.0.1:8888;           #这里指向代码中监听的端口
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header REMOTE-HOST $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          client_max_body_size 100M;
      }
      }
```