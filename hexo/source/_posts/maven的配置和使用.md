---
title: maven的配置和使用
date: 2017-08-22 09:03:56
tags:
- java
- maven
categories:
- java
- maven
---

## maven介绍
### 使用需求
* 企业岗位需求
* 软件开发遇到的问题
    - jar包的依赖与管理
    项目总有很多jar包，不能确定jar包的完全正确性、不同技术框架版本的管理、jar包的依赖
    - 自动构建项目
        + 软件开发：可行性分析 -> 需求分析 -> 软件设计 -> 软件开发 -> 发布 -> 运维
        + 软件构建：软件已经开发完毕，需要构建成一个产品发布
        构建步骤：清除 -> 编译 -> 测试 -> 报告 -> 打包（jar\war） -> 安装 -> 部署到远程

### 引入maven
* maven介绍
    - 它是apache旗下的一款开源工具
    - 采用Project Object Model（POM）概念来管理项目
    - 软件构建生命周期：
    清除 -> 编译 -> 测试 -> 报告 -> 打包（jar\war） -> 安装 -> 部署到远程

* maven解决的问题
    - jar包的声明式依赖管理
    - 自动构建、发布项目
    
* maven、ant、svn的区别
    - maven与ant之间的区别
    都是软件构建工具、软件管理工具，maven比ant更加强大，已经取代了ant
        + jar包的声明式依赖管理
        + jar包仓库
    - maven与svn之间的区别 
        + maven是软件构建工具，源码已经开发完毕
        + svn是源码版本控制工具，是协同开发工具

## 体验maven
### 下载及安装Maven
* apache官网 {% link 下载 http://maven.apache.org/download.cgi %} maven（需要jdk的支持）

* maven 软件目录介绍
    - lib：共享库。maven软件依赖的lib
    - boot：plexus-classworlds-2.5.2.jar
    该文件是jar包下载引擎，通过该工具来下载jar包
        + 第三方项目依赖的jar包
        + maven本身软件构建的生命周期插件的jar包，默认是没有集成这些插件
    - conf：settings.conf
    maven配置文件：
        + 配置本地仓库的地址，以及服务器的地址
    - bin：maven可执行的命令

### 测试maven
* 首先需要安装jdk，这里不再赘述

* 配置环境变量
JAVA_HOME：jdk的安装目录
M2_HOME：maven的解压目录，我的是C:\apache-maven-3.5.0

* 测试 maven
在控制台输入：mvn -version
{% qnimg post4-1.png title:测试maven alt:测试maven %}
如果如上图所示，则maven已经安装完毕

### 配置maven
* maven 仓库：存放jar包的地方
可以分为三个级别
    - 本地仓库：即本地存放jar包的地方
    - 私服：一般是公司的内部服务器，用来存放整个公司的jar包
    - 中心仓库：用来存放所有开源的jar包
项目构建时，maven寻找jar包的顺序是：本地仓库 -> 私服 -> 中心仓库

* maven的核心配置文件一共有两个：
    - ${M2_HOME}\conf\settings.conf，这个是全局配置文件，应用于所有用户
    - ${user.home}\.m2\settings.conf，这个是用户配置文件，应用于该用户
    用户目录下的settings.conf需要自行创建，一般建议配置该文件，不建议直接配置全局，用户配置文件会与全局配置文件合并，并覆盖全局配置文件中的相同项

* 配置本地仓库：
maven本地仓库默认是在：${user.home}/.m2/repository
也可以自定义：配置文件中有一个localRepository标签，可以用来配置本地仓库的地址
{% qnimg post4-2.png title:配置本地仓库 alt:配置本地仓库 %}

* 配置私服地址（可选）
私服不一定需要配置，如果没有配置，本地仓库没找到的jar包，maven会直接到中心仓库的去找，关于私服配置我会另开一贴说明
* 配置中心仓库
中心仓库不用配置，默认即可

## maven的使用
### maven术语
* maven软件构建生命周期
清除 -> 编译 -> 测试 -> 报告 -> 打包（jar\war） -> 安装 -> 部署到远程
* maven生命周期命令插件
mvn命令，如mvn clean：
clean -> compile -> test -> package -> install -> deploy
* maven坐标（唯一标识一个jar/war包）
坐标的组成：groupId + artifactId + version
    - groupId：一般是公司标识，如：cn.jamesxia
    - artifactId：构建物id，一般是应用标识
    - version：版本号

### 一个maven项目的目录结构
在你要编写项目的地方，新建一个文件夹，名称作为你的项目名称，然后根据下图目录层级创建maven项目

{% qnimg post4-7.png title:目录结构 alt:目录结构 %}

* 在java文件夹中编写你的java包和java类，比如cn/james/demo/Hello.java
{% qnimg post4-8.png title:编写helloworld alt:编写helloworld %}
* resources文件夹可以先放空，反正现在也没啥资源
* target文件夹可以不创建，使用maven构建项目时会自动创建
* pom.xml，下一节会讲

### 配置pom.xml
上面说的maven坐标可以唯一标识一个jar/war包，那我们应该在哪里标识呢，答案是在整个项目的根文件夹下，新建一个pom.xml，下面是一份简单的pom文件以及一些标签的说明：
{% codeblock %}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <!--pom 版本-->
      <modelVersion>4.0.0</modelVersion>
      <!--组id  
         maven 用坐标概念来标识 jar包
          坐标=groupId+artifactId+version
      -->
      <groupId>cn.jamesxia.demo</groupId>
      <!--构建物id ：产品id-->
      <artifactId>Hello</artifactId>
      <!--版本 ：SNAPSHOT :测试版本 ，镜像版本   release ：发行版本，最终版本-->
      <version>0.0.1-SNAPSHOT</version>
      <!--发布的是jar包  ，默认是jar包，也可以使war包等-->
      <packaging>jar</packaging>
      <!--项目名称 ，可写可不写-->
      <name>Hello</name>
        <dependencies>
          <!--jar包声明式依赖  依赖  junit4.9jar包-->
            <dependency>
               <!--用坐标来标识jar包： 坐标=groupId+artifactId+version -->
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.9</version>
                <!--依赖的jar包的使用范围 ： 当测试时使用该jar包
                    test 、 compile（默认）  
                -->
                <scope>test</scope>
            </dependency>       
        </dependencies>
    </project>
{% endcodeblock %}

后面项目如果有其他需要引用的jar包，直接在dependencies标签下新建一个dependency标签，填好maven的坐标就行了，有没有不用自己填的方法，of course~

* 在maven中心仓库中拷贝依赖
    - 访问 {% link maven中心仓库 http://search.maven.org/ %}
    {% qnimg post4-3.png title:中心仓库 alt:中心仓库 %}
    - 在搜索框中搜索需要的jar包，比如spring
    {% qnimg post4-4.png title:搜索spring alt:搜索spring %}
    - 选择要使用的jar包，如果org.springframework.spring，点击all，可以看到所有版本
    {% qnimg post4-5.png title:spring所有版本 alt:spring所有版本 %}
    - 随便选择一个版本，点击Version，比如2.5.6
    {% qnimg post4-6.png title:复制依赖 alt:复制依赖 %}
    复制上图中红框中的内容到pom.xml中，保存，maven就会自动给我们下载spring以及其依赖的所有jar包

### 使用maven构建项目
软件构建步骤：清除 -> 编译 -> 测试 -> 报告 -> 打包（jar\war） -> 安装 -> 部署到远程

每个步骤都对应一个mvn命令（没有报告这个命令）：clean -> compile -> test -> package -> install -> deploy

下面来讲讲如果使用这些命令，在windows命令行中，cd进入刚才创建的项目文件夹中，然后：
{% codeblock %}
mvn clean
{% endcodeblock %}

`year`

