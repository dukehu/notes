# IDEA中配置使用JRebel

> 1、在idea安装插件得地方安装，如下图：  
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/jrebel01.png)

> 2、激活，参考：https://my.oschina.net/bluell/blog/1796575  

> 3、配置，Ctrl+Alt+Shift+/,出现如下界面：  
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/jrebel03.png)  
选择Registry,出现如下界面：  
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/jrebel04.png)  
找到 compiler.automake.allow.when.app.running项，打勾

> 4、设置idea为自动编译，如下图所示，将标记中得勾选  
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/jrebel05.png)

> 5、在项目中配置JRebel（前面几部都没有问题得前提下），在项目得resources目录上点击右键,弹出菜单中点击JRebel->Enable JRebel,如下界面：  
![Image text](https://raw.githubusercontent.com/dukehu/notes/master/img/jrebel06.png)  
之后在resources文件加下出现rebel.xml文件

> 6、此时以JRebel Debug\Run启动项目，就实现了热部署得效果，可以进行测试