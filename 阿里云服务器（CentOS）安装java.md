# 阿里云服务器（CentOS）安装java

版本：java1.8 安装目录：/usr/local/java

## 卸载系统自带的OpenJDK以及相关java文件

1、`java -version`查看服务器再带的java版本，如提示`-bash: java: command not found`，说明服务器中没有安装jdk，就可以不用卸载，这届进行安装

2、`rpm -qa | grep java`，查询结果如下图：
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/centos_java_install_01.png)
> 命令说明：  
> rpm 管理套件  
> -qa 使用查询模式，查询所有套件  
> grep 查找文件中符合条件的字符  
> java 查找包含java字符串的文件

3、删除套件，`rpm -e --nodeps java-1.7.0-openjdk-1.7.0.111-2.6.7.8.el7.x86_64`，需要使用su用户进行操作，删除的方法有很多（使用yum命令，`yum -y remove`），
这只是一种，使用此命令对其他java文件进行删除，删除完成之后执行命令`java -version`出现`-bash: java: command not found`，或者
使用`rpm -qa | grep java`，查看是否删除
> 命令说明：  
> rpm 管理套件  
> -e 删除指定套件  
> --nodeps 不验证套件档的相互关联性


## 下载想要安装的JDK

1、下载地址：[jdk下载](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)，下载到windows系统，使用
如下方式上传到服务器：
> 1、检查[sshd](https://blog.csdn.net/csl_compy/article/details/54965320)服务是否开启，命令：`systemctl status sshd.service`,
> 如下图：如果服务没有启动使用下述命令进行启动：  
> * `systemctl start sshd.service` 启动sshd服务  
> * `systemctl restart sshd.service` 重启sshd服务
> * `systemctl enable sshd.service`  设置服务开机自启![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/centos_java_install_02.png)
       
> 2、传文件（使用的putty，一下命令实在putty的安装下在windows的dos窗口下输入）  
> 语法：pscp　文件路径+文件名　root@+公网地址:/存放的位置，会提示处输入密码，输入服务器密码即可  
> 示例：pscp　D:\work\code\duke\test.sql　root@dukehu.top:/usr/local/java  

> 3、下载文件（CentOS到windows）  
> 语法：pscp root@120.76.137.194:/home/love.png E:/pic/

2、解压java压缩包，使用命令`tar -zxvf jdk-8u144-linux-x64.tar.gz`，此时在/usr/local/java文件加下面就会有java1.8.0_xxx的文件夹
> 命令说明:
> tar 备份文件  
> -z 通过gzip指令处理备份文件  
> -x 从备份文件中还原文件  
> -v 显示指令执行过程  
> -f 指定备份文件

3、删除java压缩包，使用命令`rm -f jdk-8u144-linux-x64.tar.gz`
> 命令说明:
> rm 删除文件或目录  
> -f 强制删除文件或目录

## 配置jdk环境变量

1、编辑全局变量，使用命令`vim /etc/profile`，出现如下结果：![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/centos_java_install_03.png),
对文件进行如下[编辑]()，   
> JAVA_HOME=/usr/local/java/jdk1.8.0_171  
> CLASSPATH=.:{$JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar  
> PATH=$PATH:${JAVA_HOME}/bin  
> export JAVA_HOME CLASS_PATH PATH  

2、是配置文件生效，使用命令`source /etc/profile`

3、查看是否安装成果，使用命令`java -version`，出现如下界面说明安装成功![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/centos_java_install_04.png)
