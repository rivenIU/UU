#### 在cmd文件里直接执行java程序
    java -jar E:\java-iu\iu_util_development\sentinel\sentinel-installed\sentinel-dashboard-1.8.1.jar
    若这种方式的运行退出进程就结束了；如果想在后台可以运行，则需要执行 java -jar demo.jar > log_demo.file 2>&1 & 即可在后台运行该服务了，log_demo.file是日志文件。如需停止该进程 执行ps -ef|grep java 找到对应的进程 kill 进程ID 即可。

#### 在sh文件里直接打开文件夹
    !#bin/bash   
    start "" "E:\java-iu\iu_util_development\nacos\nacos-installed\nacos-server-1.1.4\nacos\bin"
    
#### 在cmd文件里查找端口号为8081的服务
    netstat -ano|findstr "8081"
    
#### git相关命令
    在cmd里输入where git就可以查看git安装目录
    
#### 设置Sentinel端口号
     
    java  -jar .\sentinel-dashboard-1.6.3.jar  --server.port=9999