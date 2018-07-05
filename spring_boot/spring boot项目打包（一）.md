# spring boot 项目打包（一）

最近做了一个像项目，也购买了阿里云的服务器（CentOS 7系统），想将项目打包部署在服务器上，
原以为很简单，实则发现自己竟然不会，所以在这里记录相关的学习笔记，方便以后进行查阅

### 将spring boot项目打成jar包

1、处理xxx.jar中没有主清单属性的问题，问题效果如下图：
![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/springboot_package_jar_problem_01.png)

问题描述：
> 直接使用maven的打包命令（`mvn clean package`）进行打包，然后在dos下使用`java -jar xxx.jar`
运行jar包，就会出现这个问题

解决问题：  
1、主清单属性是个什么东西？  
首先得知道主清单属性是个什么东西，才能去解决问题。  
要知道主清单属性是个什么东西，就必须的去了解spring boot项目打成jar包之后的目录，会发现spring boot项目打包之后会有两个jar文件，如下图：  
![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/springboot_package_jar_problem_02.png)  
这里先不关心xxx.jar.original文件是干什么的，后面用到的时候在做相关的学习记录,
打开xxx.jar包，会看到里面有三个文件夹：BOOT-INF、META-INF、org，如下图：  
![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/springboot_package_jar_problem_03.png)  
只需要关心META-INF文件加下面的MANIFEST.MF文件，该文件指明了程序的入口以及版本等相关信息，如下：  
![Image_text](https://raw.githubusercontent.com/dukehu/notes/master/img/springboot_package_jar_problem_03.png)  
* Main-Class：代表了Spring Boot中启动jar包的程序  
* Start-Class： 属性就代表了Spring Boot程序的入口类，这个类中应该有一个main方法  
* Spring-Boot-Classes： 代表了类的路径，所有编译后的class文件，以及配置文件，都存储在该路径下  
* Spring-Boot-Lib：表示依赖的jar包存储的位置  

**_这些值都是SpringBoot打包插件会默认生成的，如果没有这些属性，SpringBoot程序自然不能运行，就会报错：jar中没有主清单属性，也就是说没有按照SpringBoot的要求，生成这些必须的属性。_**  

解决办法：  
在pom.xml文件中加入SpringBoot的构建的插件，代码如下：  
 ```xml
<build>
  <plugins>
  	<plugin>
  		<groupId>org.springframework.boot</groupId>
 		<artifactId>spring-boot-maven-plugin</artifactId>
  	</plugin>
  </plugins>
 </build>
```

然后使用`java -jar xxx.jar`，运行此jar包