---
title: tomcat配置笔记
date: 2017-04-12 21:23:21
tags:
  - tomcat
categories: tomcat相关
---

### tomcat目录
1. webapps：tomcat默认部署路径。
2. wtpwebapps： eclipse默认部署路径。
3. 两者同时存在，运行bin中的startup.bat,运行wtpwebapps中部署的项目。

### conf目录
1. server.xml：tomcat的主配置文件。
2. context.xml：所有host的默认配置信息。
3. web.xml：为所有tomcat内的web应用程序提供默认配置信息。
4. tomcat-users.xml：tomcat的角色配置文件。

### server.xml配置
1. 顶层元素<Server>: port--指定一个端口，这个端口负责监听关闭tomcat的请求。
2. 顶层元素<Service>: name--指定service的名字。
3. 连接器类元素<Connector>: port--指定服务器要监听的端口，并在这个端口监听来自客户端的请求。
4. 容器类元素<Context>: 代表运行在虚拟主机上的单个web应用:
> `<Context path="bbs" docBase="bbs" debug="0" reloadable="true"/>`
> 1. path:指定访问该Web应用的URL入口.
> 2. docBase:指定Web应用的文件路径，可以给定绝对路径，也可以给定相对于<Host>的appBase属性的相对路径，如果Web应用采用开放目录结构，则指定Web应用的根目录，如果Web应用是个war文件，则指定war文件的路径。
>3. reloadable:如果这个属性设为true，tomcat服务器在运行状态下会监视在WEB-INF/classes和WEB-INF/lib目录下class文件的改动，如果监测到有class文件被更新的，服务器会自动重新加载Web应用。

### web.xml
* tomcat config 目录下的web.xml为服务器全局作用域，一般用来配置全局设置；
* java项目中WEB-INF目录下的web.xml为局部作用域。

### Web应用的目录结构
* 假设在$CATALINA_HOME/webapps下有helloapp的web应用。
* /helloapp：Web应用的根目录，所有的jsp文件和html文件都在此目录下
* /helloapp/WEB_INF：存放该web应用发布时的描述文件web.xml
* /helloapp/WEB_INF/class：存放各种class文件，Servlet文件也存放于此目录下
* /helloapp/WEB_INF/lib：存放各钟Web应用所需要的jar文件。比如可以存放JDBC驱动程序的JAR文件

### tomcat8管理页面配置
* 修改tomcat-users.xml如下：
```
<role rolename="manager"/>
<role rolename="manager-gui"/>
<role rolename="admin"/>
<user username="user" password="password" roles="admin,manager,manager-gui"/>
```
* 同时还要修改conf/Catalina/localhost/manager.xml 内容如下：
```
<Context privileged="true" antiResourceLocking="false"
         docBase="${catalina.home}/webapps/manager">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
```

### tomcat项目部署的三种方式
1. 将 Web 项目文件【同样也可以复制生成的war】拷贝到Webapps目录中。
2. 在Tomcat中的Conf目录中，在Server.Xml中的，<Host/>节点中添加：
`<Context Path="/Hello"Docbase="D:\Users\WebProject\WebContent" Debug="0" Privileged="True" Reloadable="True"></Context>`
3. 创建一个Context文件,在conf目录中，新建 Catalina＼localhost目录，在该目录中新建一个xml文件，名字不可以随意取，要和path后的那个名字一致，按照下边这个path的配置，xml的名字应该就应该是hello（hello.xml），该xml文件的内容为：
`<Context path="/hello" docBase="E:\workspace\hello\WebRoot" debug="0" privileged="true"></Context>`

### tomcat启动脚本
1. startup.bat 是tomcat的启动选项。
2. catalina.bat 是tomcat的配置项，里面可以对tomcat的虚拟内存的大小等，startup.bat最后调用 catalina.bat run。
3. CATALINA_HOME和CATALINA_BASE概念是为了解决这样的场景：
> 你需要在一台机器上面部署多个Tomcat实例，但是你又不想创建多个Tomcat的副本，换句话说就是让这些Tomcat副本拥有自己的工作目录但是共享Tomcat的代码。
> **catalina.home(安装目录)**：指向公用信息的位置，就是bin和lib的父目录。
> **catalina.base(工作目录)**：指向每个Tomcat目录私有信息的位置，就是conf、logs、temp、webapps和work的父目录。

---

### Idea与Tomcat的配置
##### 一、先说一下与Tomcat相关的两个配置：
1. 配置默认端口
 在tomcat安装目录的conf目录下的server.xml文件中，以下内容中的port属性指定了默认端口：
 `<Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>`

2. 将url与web程序目录绑定
 默认的根目录是tomcat7\webapps\ROOT，我们可以在conf\server.xml文件Host标签中指定根目录和其他目录，例如：
 ```
 <Host appBase="webapps" autoDeploy="true" name="localhost" unpackWARs="true">
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" pattern="%h %l %u %t &quot;%r&quot; %s %b" prefix="localhost_access_log." suffix=".txt"/>

        <Context docBase="F:\aaa" path="/aaa" reloadable="true"/>
        <Context docBase="F:\bbb" path="/bbb" debug="0"
reloadable="true" crossContext="true" />
      </Host>
 ```
 **根据上面的配置，我们访问 http://127.0.0.1/aaa 时候，使用F:\aaa目录中的web程序，bbb同理。根路径不变。**

 _在Tomcat默认安装后，tomcat的主目录是webapps/root目录，所以如果想改变tomcat的主目录的话可以如下所做:_
 > **方法一**：
 打开C:/Tomcat/conf/server.xml，在<host></host>之间加入下面代码：
 ```
 <Context docBase="d:/Tomcat 5.5/webapps/medi" path="" debug="0"  reloadable="true"/>
 ```

 >**方法二**：
  将tomcat安装目录下的ROOT下的所有文件全部删除，然后将工程的解压后的文件全部拷进去。

 >**方法三**：
 Tomcat5.0以下版本在d:/Tomcat/conf/Catalina/localhost目录下会自动生成了一个ROOT.Xml，
 但是5.0以上版本不再生成此文件，所以可以新建个ROOT.xml,在里面加入如下代码：
 ```
 <?Xml version='1.0' encoding='utf-8'?>
  <Context crossContext="true" docBase="d:/Tomcat 5.5/webapps/medi" path="" reloadable="true">
</Context>
 ```

##### 二、Idea运行Tomcat的问题：
IDEA运行tomcat时候重新设置了变量，以下是其启动tomcat时候的部分输出：
```
Using CATALINA_BASE:   "C:\Users\suyf\.IntelliJIdea2016.3\system\tomcat\Unnamed_ssm_3"
Using CATALINA_HOME:   "D:\tomcat\apache-tomcat-8.0.36"
Using CATALINA_TMPDIR: "D:\tomcat\apache-tomcat-8.0.36\temp"
Using JRE_HOME:        "D:\Java\jre1.8.0"
Using CLASSPATH:       "D:\tomcat\apache-tomcat-8.0.36\bin\bootstrap.jar;D:\tomcat\apache-tomcat-8.0.36\bin\tomcat-juli.jar"
```
我们打开目录C:\Users\suyf\.IntelliJIdea2016.3\system\tomcat\Unnamed_ssm_3，可以看到在conf\Catalina\localhost目录里面生成了ROOT.xml文件，使用了上述**修改tomcat主目录的方法三**，内容如下：
```
<?xml version="1.0" encoding="UTF-8"?>
<Context path="" docBase="C:\Users\suyf\IdeaProjects\ssm\target\ssm" />
```
