---
title: Windows下Python多版本共存
date: 2017-10-13 00:10:56
tags: 
- python
categories:
- python
- 环境搭建
---

刚开始接触python，只知道py有两个大版本：2.x和3.x，而且在语法上是有差别的，所以百度查了查，研究了两个py版本如何共存

## 下载python
{% link 下载地址 https://www.python.org/downloads/windows/ %}，进去之后选择2.x的某一个版本和3.x的某一个版本下载下来，我选择了当前最新的2.7.14和3.63

## 安装python
既然两个版本要共存，那我建议两个版本安装在同一个文件夹下，方便管理，我是直接将两个版本安装在``C:\python``下，分别为：
{% qnimg post6-1.png title:py安装目录 alt:py安装目录 %}

## 配置环境变量
在系统环境变量``path``中添加四个路径，分别是：
- 2.7.14版本的py目录和py目录中的Scripts
- 3.63版本的py目录和py目录中的Scripts
{% qnimg post6-2.png title:配置环境变量 alt:配置环境变量 %}

## 修改可执行文件的名称
选择当前要开发的主力版本，比如我现在要以2.7.14作为主力版本，则进入3.63的目录中，重命名目录中的``python.exe``和``pythonw.exe``为``python3.exe``和``pythonw3.exe``

## 测试
- python：
    + 在cmd下输入``python``会进入主力版本python
    + 输入``python3``会进入另一个版本的python
- pip：
    + 在cmd下直接输入pip命令，如安装request：``pip install request``会启动2.7.14的pip去下载包
    + 如果要使用3.63的pip，则要键入：``python3 -m pip install request``