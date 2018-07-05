# spring boot 项目打包（一）

最近做了一个像项目，也购买了阿里云的服务器（CentOS 7系统），想将项目打包部署在服务器上，
原以为很简单，实则发现自己竟然不会，所以在这里记录相关的学习笔记，方便以后进行查阅

### 将spring boot项目打成jar包

1、处理xxx.jar中没有主清单属性的问题，问题效果如下图：
![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/springboot_package_jar_problem_01.png)