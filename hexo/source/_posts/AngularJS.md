---
title: AngularJS
date: 2017-09-28 16:17:51
author: James Xia
tags: 
- 前端
- JS
- AngularJS
categories:
- 前端
- JS
- 框架
- AngularJS
---

## 推荐工具

- 在线编辑器
  + http://codepen.io/
  + https://jsfiddle.net/

## Angular 简介

### 什么是 AngularJS

- 一款非常优秀的前端高级 JS 框架，使用AngularJS可以轻松构建 SPA 应用程序
- 其核心就是通过指令扩展了 HTML，通过表达式绑定数据到 HTML
- SPA（单一页面应用程序）
  + 只有一个页面（整个应用的一个载体）
  + 内容全部是由AJAX方式呈现出来的

### 为什么使用 AngularJS

- 更少的代码，实现更强劲的功能
- 将一些以前在后台开发中使用的思想带入前端开发
- 带领当前市面上的框架走向模式化或者架构化

### AngularJS 的核心特性

- MVC
- 模块化
- 自动化双向数据绑定
- 指令系统

### 相关链接

- [AngularJS中文网](http://www.angularjs.cn/)
- [中文API](http://docs.angularjs.cn/api)
- [AngularJS官网](https://angularjs.org)
- [AngularUI](http://angular-ui.github.io/)

## Angular 上手

### 安装 Angular

- 使用 git 安装
  ``` bash
  # 在终端进入项目的js文件夹中，运行下面命令
  git clone https://github.com/angular/angular.js.git
  ```
- 使用 CDN 上的 Angular.js
  + http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js
- 使用 Bower 安装
  ```bash
  bower install angular
  ```
- 使用 NPM 安装
  ```bash
  npm install angular
  ```
- 每种方式安装包，本质都是将angular的库下载到当前文件夹中

### 简单示例

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Angular Hello World</title>
  <script src="../node_modules/angular/angular.js"></script>
</head>
<!-- 使用ng-app圈定Angular的管辖范围 -->
<body ng-app>
  <h1>使用ng进行双边数据绑定</h1>
  <!-- 
  angular会在它的内存空间分钟分配一部分给一个$scope对象，这个对象就是所有ng-model的容器 
  使用ng-model指令绑定input->user.name<-strong，两个只有一个改变，另一个也会变
  -->
  <input type="text" placeholder="请输入你姓名" ng-model="user.name">
  <p>hello <strong>{{user.name}}</strong></p>
</body>
</html>
```

- angular中最重要的概念是指令（directive）

- ng-model 是双向数据绑定的指令，效果就是将当前元素的value属性和模型中的user.name建立绑定关系

- JS: BOM DOM ES

### 分析 Angular 示例

### 使用总结

### 运行官方文档


## CDN的优势

Content Dev

- 快
- 节省自己服务器的带宽压力和流量


## Angular 基础概念

### MVC 思想

#### 什么是 MVC 思想

- 将应用程序的组成划分为三个部分：Model View Controller
- 控制器的作用就是初始化模型用的；
- 模型就是用于存储数据的
- 视图用于展现数据


- 登陆案例
- 模型
  + 我们数据库中所有用户的信息
  + 接受控制器传来的用户名和密码进行校验的业务逻辑并返回true/false
- 控制器
  + 接受用户在界面上填写的用户名和密码
  + 将用户名和密码交给模型
- 视图
  + 给用户呈现一个表单
  + 接受用户输入内容，并将其提交给控制器
  + 根据控制器返回的数据，响应用户页面


### 模块（Module）

- 划分应用程序结构
- 我们可以通过angular.module创建一个模块
- angular.module方法传递两个参数才是创建模块，一个参数是获取模块

### 控制器（Controller）

- 通过$scope和视图关联
- 

### 视图模型（$scope）


### 表达式（Expression）


### 单向数据绑定


### 双向数据绑定


## Angular 指令系统
