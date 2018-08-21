---
layout: post
title: "hexo + github pages建立个人博客"
author: James Xia
date: 
---

之前就一直有写博客的冲动，苦于懒癌，一直没有实际行动。最近开始上班，觉得以前的东西都差不多忘光了，这样下去是会被开除的，所以“无奈”抓紧行动:confounded:。话不多说，本文会以我自己的实际操作为基础，写一篇建站引导，也算是将经验持久化吧，不然过两天，就又没了，有着鱼的记性真的不适合干这一行啊。。。。

## 需要的东东

### git and github

- git：版本控制工具，[下载地址]( https://git-scm.com/downloads ) （外网，有科学上网会快一点），关于git的配置请看[官方文档](https://git-scm.com/book/zh/v2) 

- github：代码托管仓库，我们要将建站的文件以及我们的博客文件分别托管到两个仓库中。
    - [注册](https://github.com/join) & [登录](https://github.com/login) github
    - 创建两个仓库：
		- hexo-source：名称可以任意取，用来管理建立的网站文件
		- 账号名.github.io：其中账号名就是你的github账号的名称

### sublime text 3

博客编写使用的语言是markdown，所以我选择了sublime(ST3)作为编辑器。
- [下载](https://www.sublimetext.com/3)，安装ST3

- 安装packet control(ST3安装插件的工具)
  使用快捷键ctrl + `，调出sublime的控制台，在控制台中输入以下代码，回车，等待。。。

  ```console
  import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
  ```

- 安装markdown相关插件
    - 装完packet control后，在ST3中使用快捷键ctrl + shift + p ，输入install，选择install package：

    {% qnimg post1-1.png title:install alt:install %}

    - 搜索 MarkdownEditing 安装

        MarkdownEditing是Markdown写作者必备的插件，它可以不仅可以高亮显示Markdown语法还支持很多编程语言的语法高亮显示，安装完成后要重启sublime

    - 搜索 OmniMarkupPreviewer 安装

        OmniMarkupPreviewer用来预览markdown编辑的效果，同样支持渲染代码高亮的样式

        快捷键：

        - control + alt + o : 在浏览器中预览
        - control + alt + x : 导出为html

### Node.js
安装 Hexo 之前需要安装Node.js，Node.js是什么可以参考我的另一篇[文章](https://jamesxia23.github.io/2017/09/25/%E6%9E%84%E5%BB%BA%E5%89%8D%E7%AB%AF%E8%87%AA%E5%8A%A8%E5%8C%96%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%8E%AF%E5%A2%83/)，这里不再赘述，直接上安装步骤：
1. 安装nvm
- Mac&linux安装nvm
    - 首先确保你的用户主目录下有.bash_profile文件，没有就创建一个：
    ```bash
    touch .bash_profile
    ```
    - 然后运行curl命令
    ```bash
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.4/install.sh | bash
    ```
    - 最后验证是否安装成功：
    {% qnimg post5-1.png title:mac验证nvm安装 alt:mac验证nvm安装 %}
- Windows安装nvm
    - 下载 [nvm](https://github.com/coreybutler/nvm-windows/releases)
    {% qnimg post5-2.png title:windows上下载nvm alt:windows上下载nvm %}
    - 下载完解压，双击nvm-setup安装，一直下一步就行了
    - 安装完在cmd中键入``nvm version``验证是否安装成功

2. 安装Node.js
+ 打开终端，运行命令 `` nvm install node版本号 `` ，如： `` nvm install 8.4.0 ``

+ 待到安装完成后，运行 `` nvm list `` 可以查看系统中所有存在的node版本

+ 使用 `` nvm use 版本号 `` 可以切换当前使用的nvm的版本

+ 最后在命令行验证是否配置成功：

    ```console
    node --version
    ```

    {% qnimg post1-3.png title:version alt:version %}

## 安装 Hexo
重头戏来了，安装完 git 和 Node.js 后，就要来安装我们的博客系统了，附上[官方文档](https://hexo.io/zh-cn/docs/)

### 什么是 Hexo
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 克隆远程仓库到本地
刚才我们创建了两个仓库，现在只需要克隆hexo-source一个就行，剩下那个不需要在本地管理。

* 打开git bash（必须先配置好自己的登录信息），cd进入你的本地仓库文件夹，比如我的是用户目录下的Documents/GitHub：

    {% qnimg post1-4.png title:本地仓库 alt:本地仓库 %}

* 运行 git 命令，克隆仓库：

    ```git bash
    git clone https://github.com/用户名/仓库名.git
    ```

    {% qnimg post1-5.png title:克隆仓库 alt:克隆仓库 %}

    之后你的本地仓库文件夹下就会多了一个文件夹，名称就是你的仓库名：

    {% qnimg post1-6.png title:本地仓库 alt:本地仓库 %}

    PS：这里说明一下为什么要搞个仓库来保存网站的文件，这是为了以后迁移方便，即使你网站文件放在服务器上，难保永远都在这台服务器写博客，后面会再讲如何迁移。

### 安装 Hexo
* 在 git bash 中，进入仓库 hexo-source，运行命令，安装 hexo 命令行：

    ```git bash
    npm install -g hexo-cli
    ```

* 之后，初始化 hexo：

    ```git bash
    hexo init folder
    ```

    这里folder名称任取，最好不要是中文，我就取hexo：

    {% qnimg post1-7.png title:初始化 alt:初始化 %}

    看到 start blogging with Hexo！就说明你成功了。。。。一大半~

* 接下来，进入hexo文件夹，运行命令：

    ```git bash
    cd hexo
    npm install
    ```

    做完之后，你的本地 hexo 就搭建好了，在hexo文件夹中运行：

    ```git bash
    hexo server
    ```

    然后使用浏览器进入：localhost:4000，就可以看到你的网站了
    当然，我们要的是不只是本地访问，我们要部署到github我们创建的第二个仓库中

## 部署到github

### 配置_config.yml
进入hexo文件夹，里面就会是这样的：

```explorer
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

这些文件夹和文件分别有什么用， [官方文档](https://hexo.io/zh-cn/docs/setup.html )都有说，这里说一下 ``_config.yml``，这个是全站的配置文件，说几个必须配置的：

```sublime
title: Hexo  #网站标题
subtitle:    #网站副标题
description: #网站描述
author:      #网站作者
url: # http://你的github用户名.github.io (重要) 
deploy: #这个是为了发布到github上去，所以要配置仓库
  type: git
  repo: https://github.com/你的github用户名/你的github用户名.github.io.git
  branch: master
```

PS：需要注意的一点是，所有配置项的值跟冒号之间一定要用空格隔开，如："title: Hexo"

### 常用命令
这些命令都是在 hexo 主目录运行的，就是我的hexo-source/hexo

* hexo clean

    清除缓存文件 (db.json) 和已生成的静态文件 (public)。
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

* hexo server

    启动本地服务器。默认情况下，访问网址为： http://localhost:4000/ ，当我们配置了提交到github之后，就可以丢掉这个命令了哈哈哈哈

* hexo generate

    将我们写的markdown文件编译为html文件

* hexo deploy

    将本地静态文件发布到远程（github）

* hexo clean && hexo g -d

    清除缓存，生成文件，发布到远端，一站式搞定。居家旅行，必备命令~

    其余命令可以看[官方文档]( https://hexo.io/zh-cn/docs/commands.html )

### 部署到github

使用刚才的命令：

```git bash
hexo clean && hexo g -d
```

{% qnimg post1-8.png title:发布到github alt:发布到github %}

显示上述图片，说明发布成功，直接打开浏览器试试：github用户名.github.io，网站就搭建完毕了

## 图床

### 什么是图床

未完待续。。。。。。明天更新啦啦啦啦