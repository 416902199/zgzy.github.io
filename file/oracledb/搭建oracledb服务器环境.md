


      yum install libaio*
      yum -y install gcc gcc-c++
      http://ahk2016.oss-cn-shenzhen.aliyuncs.com/docker/instantclient-basic-linux.x64-12.2.0.1.0.zip  下载到/soft
      http://ahk2016.oss-cn-shenzhen.aliyuncs.com/docker/instantclient-sdk-linux.x64-12.2.0.1.0.zip     同上

      unzip instantclient-basic-linux.x64-12.2.0.1.0.zip
      unzip instantclient-sdk-linux.x64-12.2.0.1.0.zip
      mv instantclient_12_2 instantclient
      cd instantclient
      ln -s libclntsh.so.12.1 libclntsh.so
      # 设置环境变量
      vi /etc/profile
      #编辑添加内容如下

      export LD_LIBRARY_PATH=/soft/instantclient:$LD_LIBRARY_PATH
      export OCI_LIB_DIR=/soft/instantclient
      export OCI_INC_DIR=/soft/instantclient/sdk/include

      #保存退出

      #重启用profile文件
      source /etc/profile
      2.4 安装oracledb
      　　之前安装都已经完成了，这一步会非常简单。
       npm install oracledb