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

    {% qnimg hello-world-1.png title:install alt:install %}

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

    {% qnimg hello-world-2.png title:version alt:version %}

## 安装 Hexo
重头戏来了，安装完 git 和 Node.js 后，就要来安装我们的博客系统了，附上[官方文档](https://hexo.io/zh-cn/docs/)

### 什么是 Hexo
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 克隆远程仓库到本地
刚才我们创建了两个仓库，现在只需要克隆hexo-source一个就行，剩下那个不需要在本地管理。

* 打开git bash（必须先配置好自己的登录信息），cd进入你的本地仓库文件夹，比如我的是用户目录下的Documents/GitHub：

    {% qnimg hello-world-3.png title:本地仓库 alt:本地仓库 %}

* 运行 git 命令，克隆仓库：

    ```git bash
    git clone https://github.com/用户名/仓库名.git
    ```

    {% qnimg hello-world-4.png title:克隆仓库 alt:克隆仓库 %}

    之后你的本地仓库文件夹下就会多了一个文件夹，名称就是你的仓库名：

    {% qnimg hello-world-5.png title:本地仓库 alt:本地仓库 %}

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

    {% qnimg hello-world-6.png title:初始化 alt:初始化 %}

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

{% qnimg hello-world-7.png title:发布到github alt:发布到github %}

显示上述图片，说明发布成功，直接打开浏览器试试：github用户名.github.io，网站就搭建完毕了

### 绑定个人域名

刚才我们已经搭建了可以外网访问的博客，但是域名是github给的，如果我们想要使用自己的域名访问怎么办呢？

1. 注册自己的域名，我选择在[阿里云](https://wanwang.aliyun.com/domain)上买，其实其他云上面也可以买

   {% qnimg hello-world-8.png title:域名搜索 alt:域名搜索 %}

2. 搜索自己喜欢的域名，只要还没被注册就可以买了，购买也很简单，用支付宝付款就行了

   {% qnimg hello-world-9.png title:域名搜索结果 alt:域名搜索结果 %}

   购买的时候记得买一下域名解析的服务

   {% qnimg hello-world-10.png title:域名解析 alt:域名解析 %}

3. 付款之后会让你做实名认证，也是按照提示来就行，一般1个小时内就给你批下来了

4. 批下来后，在自己阿里云控制台就可以看见域名了

   {% qnimg hello-world-11.png title:阿里云控制台 alt:阿里云控制台 %}

5. 点击域名后面的管理—域名解析

   {% qnimg hello-world-12.png title:域名解析 alt:域名解析 %}

6. 添加一条记录

   {% qnimg hello-world-13.png title:添加域名解析 alt:添加域名解析 %}

   添加后就会出现一条域名解析记录了

7. 接下来在hexo的source文件夹下面新建一个文件`CNAME`，注意名称一定要大写，而且不能有后缀，然后在文件里面输入刚才配的域名

   {% qnimg hello-world-14.png title:CNAME alt:CNAME %}

   保存，退出

8. 然后使用刚才的万能命令，将文件发布到github的博客那个仓库里面去

   ```
   hexo clean && hexo g -d
   ```

9. 访问试试看：`blog.jamesxia.cn`，看到博客就说明成功了~~~

## 图床

### 什么是图床

图床一般是指储存图片的服务器 ，就是说我们可以把博客里面的图片存储在别的服务器上，这样做可以节省访问git page的带宽，毕竟GitHub在国外，把图片放在单独的cdn服务器上会使你的博客加载起来更快速

### 七牛云

其实七牛云不只是可以做图片服务器，现在也有的云主机等云服务，选择它是因为注册并实名认证之后，将免费享有10GB存储空间，用来存图片刚刚的，下面介绍一下怎么使用七牛云

1. 首先要先[注册](https://portal.qiniu.com/signup/choice)一个账户

   {% qnimg hello-world-15.png title:七牛云注册 alt:七牛云注册 %}

   点击申请个人用户，然后按照要求一步一步来就行了

2. 登录之后，点击首页管理控制台，来到自己的控制台

   {% qnimg hello-world-16.png title:七牛控制台 alt:七牛控制台 %}

   点击添加对象存储

   {% qnimg hello-world-17.png title:新建存储空间 alt:新建存储空间 %}

   自定义存储空间名称（记下来，后面插件会用到），这样空间就创建好了

3. 点击内容管理，获取外链默认域名（如：`xxxxxx.bkt.clouddn.com`），记下来等会插件要用到

4. 点击个人面板---密钥管理，记下当前使用的AK和SK，等会插件要用到

### hexo-qiniu-sync 插件 

这个是为了你可以方便的同步本地的图片与引用七牛云上的图片的插件，安装配置步骤如下：

1. 使用git bash或者cmd进入hexo主目录，运行

   ```git bash
   npm install hexo-qiniu-sync --save
   ```

2. 在站点的配置文件 `_config.yml`中添加如下配置：

   ```yml
   qiniu:
     offline: false // 是否离线，true时，在本地预览时使用本地资源，省流量；false时，本地预览也走云端，可以验证能否正确访问
     sync: true // 是否同步
     bucket: 存储空间名称
     access_key: 刚才保存的AK
     secret_key: 刚才保存的SK
     dirPrefix: // 文件夹前缀，可以为空
     urlPrefix: http://xxxxxx.bkt.clouddn.com（刚才保存的外链默认域名）
     local_dir: cdn // 本地静态资源路径，与source文件夹同级
     update_exist: true // 是否更新已经存在的静态文件
     image:
       folder: images // 图片存放目录，在local_dir下面，如：cdn/images
       extend:
     js:
       folder: js // js文件存放目录，同上
     css:
       folder: css // css文件存放目录，同上
   ```

   上述提到的所有文件夹都需要自己建立完后，目录结构如下：

   ```explorer
   |...
   ├─cdn
   │ ├─css
   │ ├─images
   │ └─js
   ├─source
   |...
   ```

3. 引用图片，如果你想引用`cdn/images`下面的`demo.jpg`，只需要在文章插入：

   ```markdown
   {% qnimg demo.jpg %}
   ```

   加入title和alt：

   ```
   {% qnimg demo.jpg title:demo alt:demo %}
   ```

   更多参数命令可以看这个插件的[官方文档](https://github.com/gyk001/hexo-qiniu-sync)

4. 同步到七牛云，git bash进入hexo文件夹，运行：

   ```git bash
   hexo qiniu s
   ```

   记住，图片只有同步到七牛云之后，在博客才能引用到，所以在使用上面的一键发布命令之前，必须先使用同步命令将图片同步到七牛云

## 结语

到这里，一个比较完整的博客算是搭完了，剩下的什么换主题，加emoji表情之类的我就不详细说了，都很简单，这里就不说了，希望可以作为自己一个好的开始吧，最近太懒了，要振奋起来了:fried_shrimp: