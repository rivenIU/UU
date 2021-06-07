#### 在cmd文件里直接执行java程序

test111

test 222
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
    
    merge和rebase区别
    https://www.jianshu.com/p/4079284dd970
    
    
    idea使用git
    访问git官网下载git，安装。
    找到你的项目目录，右键git gui here，创建一个git仓库叫local——rep，那么你的项目就在你的本地仓库，
    然后在idea里右键此项目就可以看到Git选项，注意我们在commit directory之前必须填写commit message信息，
    message的第一行是HEAD信息，
    如果第二次提交该文件时修改了message的HEAD信息则会无法push，可通过右键该文件reset HEAD即可更新远程仓库的HEAD。就可以把此项目提交到本地仓库。
    然后右键此项目选择repository-》remotes，选择添加，输入你远程仓库的名称例如main，然后输入仓库地址如
    https://github.com/rivenIU/UU，这里本地仓库名称是settings-》git里面配置的，默认为master。
    然后我们右键要上传的文件或目录，选择git-》push，就可以上传到远程仓库了，
    远程仓库本来只有main仓库，现在就会自动新增一个master仓库，上传的文件就在那里。
    
    commit message格式
    https://blog.csdn.net/alnorthword/article/details/88537561
    https://blog.csdn.net/qq_27445903/article/details/78092757?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control
