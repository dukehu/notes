# 阿里云服务器（CentOS）安装java

## 卸载系统自带的OpenJDK以及相关java文件

1、`java -version`查看服务器再带的java版本，如提示`-bash: java: command not found`，说明服务器中没有安装jdk，就可以不用卸载，这届进行安装

2、`rpm -qa | grep java`，查询结果如下图：
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/centos_java_install_01.png)
> 命令说明：  
> rpm 管理套件  
> -qa 使用查询模式，查询所有套件  
> grep 查找文件中符合条件的字符  
> java 查找包含java字符串的文件