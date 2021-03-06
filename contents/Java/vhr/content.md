# 一步步跑起来个 Java 前后端分离的人力资源管理系统

> 本文适合刚学习完 Java 语言基础的人群，跟着本文可了解和运行项目，本示例是在 Windows 操作系统下演示。

![](./images/cover.jpg)

<p align="center">本文作者：HelloGitHub-<strong>秦人</strong></p>

大家好！这里是 HelloGitHub 推出的[《讲解开源项目》](https://github.com/HelloGitHub-Team/Article)系列，今天给大家带来一款基于 Java 语言的人力资源管理开源项目——**微人事** 

微人事是一个前后端分离的人力资源管理系统，项目采用 SpringBoot + Vue 架构。该系统是管理员对员工信息的一些列的操作。首先管理员需要登入系统，可对员工信息进行增删查改操作，也可以对员工进行奖罚，工资等信息的增删查改。然后实现对部门员工信息的统计和修改。所有的操作都在系统中有日志记录。下面是项目搭建完成的效果图：

> 微人事的项目地址：https://github.com/lenve/vhr

想要快速搭建一套微人事管理系统，那就跟着本文的步骤。你只需要花 10 分钟，就能拥有一个属于自己的微人事管理系统，并且可以对前后端分离的项目有一个完成的概念和感觉。下面是搭建完成的效果图：
![](./images/1.png)

## 一、技术栈

微人事这个项目采用：

### 1.1 后端技术栈

- **SpringBoot**：SpringBoot 是基于 Spring4 进行设计，目的是为了简化 Spring 应用的初始搭建以及开发过程。 该框架使用特定的方式(集成 starter，约定优于配置)来进行配置，从而使开发人员不需要再定义样板化的配置。  

- **SpringSecurity**：SpringSecurity 是一个强大的和高度可定制的身份验证和访问控制框架。它着重于为 Java 应用程序提供身份验证和授权。  

- **MyBatis**：MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。

- **MySQL**：MySQL 是一个轻量级关系型数据库管理系统，由瑞典 MySQL AB 公司开发，目前属于 Oracle 公司。

### 1.2 前端技术栈

- **Vue**：Vue 是一套构建用户界面的渐进式框架。 数据驱动，组件化是 Vue 的两大核心思想。

- **ElementUI**： ElementUI 时一套基于 Vue 2.0 的组件库，提供了配套设计资源。由饿了么公司前端团队开源。 

- **Axios**：Axios 是一个基于 Promise 的 HTTP 库，可以用在浏览器和 Node.js 中。

- **Vue-router**：Vue-router 是 Vue 的路由，根据不同的路径映射到不同的视图。 

## 二、项目结构

### 2.1 后端项目 hrserver 项目结构如下图：

![](./images/2.png)


后端项目采用 MVC 模式，使用现在流行的 SpringBoot 框架。SpringBoot 是基于 SpringMVC 衍生出来的框架。宗旨是较少配置，让开发者快速上手做项目。

目录说明：

1. bean：数据模型目录，包括数据库模型，参数模型，业务模型。 
2. common：基础工具包目录，包括日期工具类，邮件工具类等。
3. config：基础配置目录，包括权限认证，安全认证，菜单权限等类。
4. controller：业务的控制器目录，包括员工信息，工资，系统公共功能等控制器。 
5. exception：自定义异常目录。公用的异常处理实现类。
6. mapper：数据库操作层目录。包括数据接口的定义，查询 SQL 的业务实现。
7. service：业务层目录，包括部门、员工、菜单、角色、工资等业务的业务类。 
8. HrserverApplication：SpringBoot 框架的入口类，在 IDE 中可直接运行 main 方法。 
9. resources/static：静态资源存放目录
10. resources/templates：前台页面模板路径，包括 email 模板。
11. resources/application.properties：环境配置文件，包括关系型数据库 mysql 连接信息，mybatis 配置文件路径，非关系型数据 redis 的连接信息，邮件服务的配置等。
12. resources/mybatis-config.xml：mybatis 配置文件，目前包括日志带引的配置。
13. resources/vhr.sql：MySQL 数据库脚本，（注：数据库表有外键约束，适当修改sql遇见的执行顺序 ）

### 2.2 前端项目 vuehr 项目结构如下图：

![](./images/3.png)


前端项目采用 MVVM 架构，就是 MVC 架构中多了一个 ViewMode。它是 Model 和 Controller 之间的一座桥梁。

目录说明：

1. build：Vue 项目构建配置目录，包括vue加载器的基础配置，webpack 的环境配置。
2. config：Web 项目的环境配置目录，包括代理配置、开发环境配置、生成环境配置。
3. node_modules：第三方依赖目录，包括项目引用的三方依赖模块。
4. src/components：前端组件目录，包括聊天组件、员工组件、个人组件、统计组件等。
5. src/lib：三方依赖目录，包括 SockJS，SockJS 是一个浏览器 JavaScript 库，提供类似 WebSocket 的对象。
6. src/router：路由目录，包括项目前端路由的配置信息。
7. src/store：全局数据商店，存放供全局使用的一些数据。
8. src/utils：工具包路径，包括前台 API 接口和常用的工具类。
9. src/App.vue：Vue 前端的入口组件。
10. src/main.js：Vue 前端入口 JS 事件定义的文件。
11. src/index.html：微人事前端首页。
12. src/package*.json：Vue 前端项目打包的配置文件，类似于 maven 项目的 pom.xml 文件。声明了项目需要的三方依赖。

## 三、实战操作

### 3.1  准备工作

1.确保本地已安装 Java8 开发环境；

![](./images/4.png)

2.确保本地以安装 maven 工具；

![](./images/5.png)

3.确保本地以安装 Node.js；

![](./images/6.png)


### 3.2 下载项目

```bash
git clone https://github.com/lenve/vhr.git
```

### 3.3 运行项目

#### 3.3.1 初始化数据库

数据库脚本存放的路径在：hrserver\src\main\resources\vhr.sql，我本地使用的可视化工具 Navcat。新建一个名称为 vhr 的数据库。

![](./images/7.png)


导入 vhr.sql 文件数据到 mysql 数据库。

![](./images/8.png)


#### 3.3.2 修改后台项目的环境配置文件

修改后台项目的环境配置文件 hrserver\src\main\resources\application.properties

```
# MySQL 配置
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
spring.datasource.url=jdbc:mysql://IP:3306/vhr?useUnicode=true&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=root
```

#### 3.3.3 IDE里运行项目

1. 运行后端项目

   a.导入后端项目到 IDEA 开发工具

   ![](./images/9.png)

   b.运行后端项目

   打开后台项目的入口类 HrserverApplication.java 
   
   ![](./images/10.png)

   c.项目启动成功如下图
   
   ![](./images/11.png)

2. 运行前端项目

   a.导入前端项目到 VSCode 开发工具
   ![](./images/12.png)

   b.运行前端项目

   c.在 VSCode 左侧导航栏，NPM SCRIPTS中直接运行 dev。
   
   ![](./images/13.png)

   d.Ctrl+shift+Y 呼出控制台，在控制台终端依次执行如下命令：

   ```bash
   # 安装依赖
   npm install
   
   # 在 localhost:8080 启动项目
   npm run dev
   ```

   ![](./images/14.png)

3. 项目运行成功如下图

   ![](./images/15.png)



#### 3.3.4 命令行运行项目

Win + R 打开 Wndows 命令行窗口

1. 运行后端项目

   a.切换目录到 vhr\hrserver\ 下

   ![](./images/16.png)

   b.打包后台项目

   ```bash
   mvn clean package
   ```

   c.命令行运行微人事后台项目

   切换目录到 hrserver\target\，执行如下命令可启动项目

   ```bash
   java -jar hrserver-0.0.1-SNAPSHOT.jar
   ```

   d.项目运行成功成功入下图

   ![](./images/17.png)

2. 运行前端项目

   a.切换目录到 vhr\vuehr\ 下

   ![](./images/18.png)

   b.在命令行依次执行如下命令

   ```bash
   # 安装依赖
   npm install
   
   # 在 localhost:8080 启动项目
   npm run dev
   ```

   c.项目运行成功成功入下图

   ![](./images/19.png)

### 3.3.5 项目启动成功效果
1. 员工基本信息维护

   ![](./images/20.png)

2. 基础信息设置

   ![](./images/21.png)

## 四、最后

教程至此，你应该对前后端分离的项目有了一些简单的认识。并且你也已经在本地将项目跑起来了。所谓前后端分离，其实你也可以搞定的！项目涉及的技术比较多，你可以选择感兴趣的技术去学习。后面怎么玩就看你自己了：部署到服务器正式上线、定制自己专属的功能、给项目贡献代码等，都是可以的。

本教程是针对有一定 Java 编程基础，但又不知道如果运行本项目的小伙伴。如果你是老手欢迎直接阅读项目的说明文档，获取更多更详细的资料。

## 五、参考文章：

- [SpringBoot wiki](https://www.jianshu.com/p/350972a3a258)

- [Spring Security wiki](https://blog.51cto.com/favccxx/1606179) 

- [MyBatis wiki](http://www.mybatis.org/mybatis-3/zh/index.html)

- [MVVM框架 wiki](https://zhuanlan.zhihu.com/p/59467370)



