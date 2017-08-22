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

## maven管理jar包依赖
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