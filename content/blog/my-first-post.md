---
title: "Hugo+Github Page搭建静态博客"
date: 2022-09-05T11:57:00+08:00
draft: false
---

图片保存文件名不允许包含数字，否则无法显示

环境：Windows11 专业工作站版
工具：git，choco，hugo
主题：Codex
背景：已经在Github建立过基于Hexo的静态博客


注意：请注意，此主题仅支持 Hugo 版本 82 及更高版本。

# 一、搭建环境

## 1.1 安装Chocolatey

Chocolatey有点类似ubuntu当中的apt，在Windows下安装后可作为Windows的“包管理器”，这里安装Chocolatey是根据Codex主题文档当中的要求。

注意，在安装使用Chocolatey时需要全程科学上网。

打开Poewershell,输入以下命令：

```bash
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

安装完成后可再输入“choco”，返回版本号说明安装成功。

## 1.2 准备所需文件

### 1.2.1 准备Hugo

到Hugo项目的官方页面下载已经编译好的程序：https://github.com/gohugoio/hugo/releases

![](/blog/q/1.png)

建议下载该“拓展版本”，以用于Codex主题的Sass/SCSS支持。

下载完成后解压文件，在电脑当中创建新目录用于存放Hugo文件，并将解压后的.exe后缀文件放入该目录中。

在当前目录打开cmd命令行，输入命令新建站点：
```bash
hugo new site new_site #"new_site"是你站点文件夹的名字，自己改
```

### 1.2.2 准备Codex主题

进入Codex的项目主页https://github.com/jakewies/hugo-theme-codex
接下来的操作就依从Readme文件走就好了。

进入站点文件夹的根目录，用git运行：
```bash
git submodule add https://github.com/jakewies/hugo-theme-codex.git themes/hugo-theme-codex
```

打开下载下来的主题文件，将exampleSite下的config.toml复制并覆盖到站点根目录

打开在站点根目录下刚刚被覆盖的config.toml配置文件，删除以下一行即可：
```bash
themesDir = "../../" 
```
下面贴出我用Deepl翻译的配置文件：

```bash
# DO NOT REMOVE THIS
theme = "hugo-theme-codex" 

# Override these settings with your own
# 用你自己的设置覆盖这些设置
title = ""
languageCode = ""
baseURL = "http://example.com/"
# baseURL = "https://jmzdd.github.io/iksrr.github.io/"
copyright = "© "

# Add your Disqus shortname here.
# 在这里添加你的Discuz短名
# disqusShortname = ""

# Add your Google Analytics identifier: UA-XXXXXXXX-X
# 添加你的谷歌分析标识符
# googleAnalytics = "" 

# Optional params
# 可选参数
[params]
  # Follow the Hugo date/time format reference here: 
  # https://gohugo.io/functions/format/#gos-layout-string
  # 按照Hugo的日期/时间格式,参考这里
  dateFormat = "Jan 2 2006"

  # Links to your social accounts, comment/uncomment as needed. Icons will be displayed for those specified.
  # 链接到你的社交账户，根据需要评论/取消评论。图标将显示为指定的那些。
  # twitter = "https://twitter.com/<your handle>"
  github = "https://github.com/xxxxx"
  email = "mailto:xxxxx@xxx.xxx"
  zhihu = "https://www.zhihu.com/people/xxxxx"
  bilibili = "https://space.bilibili.com/xxxxx"
  wymusic = "https://music.163.com/#/user/home?id=xxxxx"
  # 这里我自己添加了一些图标，后面会讲到

  # mastodon = "https://mastodon.social/@nickname"
  # facebook = "https://facebook.com/<your handle>"
  # gitlab = "https://gitlab.com/<your handle>"
  # instagram = "https://instagram.com/<your handle>"
  # linkedin = "<link to your profile>"
  # youtube = "https://www.youtube.com/channel/<your channel>"
  
  # Titles for your icons (shown as tooltips), and also their display order.
  # 你的图标的标题（作为工具提示显示），以及它们的显示顺序
  # Currently, these icons are supported: 
  #   "Twitter", "GitHub", "Email", "Mastodon", "Facebook", "GitLab", "Instagram", "LinkedIn", "YouTube"
  iconOrder = ["gitHub","email","zhihu","bilibili","wymusic"]

  # Metadata for Twitter cards, defaults to params.twitter
  # twitter卡片的元数据，默认为params.twitter
  # twitterSite = "@<your handle>"
  # twitterAuthor = "@<your handle>"

  # Set to true to display page title in table of contents in blog posts.
  # 设置为 "true"，在博客文章的目录中显示页面标题。
  showPageTitleInTOC = true

# This disables Hugo's default syntax highlighting in favor
# of prismjs. If you wish to use Hugo's default syntax highlighting
# over prismjs, remove this. You will also need to remove the prismjs
# vendor script in layouts/blog/single.html.
# 这将禁用Hugo的默认语法高亮，而采用
# 语法高亮。如果你想使用Hugo的默认语法高亮
# 而不是Prismjs，请删除此项。你还需要删除 prismjs
# 厂商的脚本。
[markup]
  [markup.highlight]
    codeFences = false
    
  # Set to false to disallow raw HTML in markdown files
  # 设置为false以禁止在markdown文件中使用原始HTML
  [markup.goldmark.renderer]
      unsafe = true

# Controls the navigation
[[menu.main]]
  identifier = "about"
  name = "about"
  title = "About"
  url = "/"

[[menu.main]]
  identifier = "blog"
  name = "blog"
  title = "Blog"
  url = "/blog"

```

### 1.2.3 新建文章

在站点根目录打开命令行并输入命令：
```bash
hugo new blog/blogpost.md #blogpost是文章文件名，新文件会生成在content\blog当中
```
下面贴出我用Deepl翻译的文章配置文件：

```bash
---
# 文章标题
title: "Blog Post"
# 文章生成时间
date: 2022-09-04T21:29:20+08:00
# 文章文件名
slug: "1111"
# 用于文章seo的描述词
description: ""
# 用于文章seo的关键词
keywords: []
# 选择当前文章是否包含在构建当中，选择“false”则包含
draft: false
# 文章标签
tags: []
# 选择启用数学排版
math: false
#  在>1024px的屏幕上包含一个目录
toc: true
---
```

简单地填写修改配置文件后，就可以开始在本地测试站点了。

在站点根目录打开命令行，输入一下命令以查看效果。

```bash
hugo server -D
```

确认没问题后，按Ctrl+c结束并退出本地预览。

输入一下命令生成站点文件：

```bash
hugo
```

生成的文件都会出现在站点根目录的public文件夹当中。

# 二、新建仓库并上传至Github

## 2.1 修改配置文件

在上传至Github之前，我们还需要简单修改一下配置文件的内容。

打开站点根目录下的config.toml文件，修改以下文字：
```bash
# baseURL = "http://example.com/"
baseURL = "https://jmzdd.github.io/接下来要新建的仓库名称/"
```

## 2.2 上传至Github

在Github新建一个仓库，并且在public文件夹当中运行以下命令以连接远程仓库：
```bash
git init
git remote add origin git@github.com:<USERNAME>/<USERNAME>.github.io.git
```

将public当中的内容推送至Github上：
```bash
git add .                # 加入所有更改过的文件
git commit -m "update"   # 简单说明更新了啥
git push -u origin main  # 将更改推送至主分支
```

之后到仓库的设置看看page选项打开了没，打开后等待几分钟就行了，到这里已经基本搭建完成。

# 三、自定义主题

虽然网站已经配置完成了，但是原来的主题看起来有点简洁，我们可以稍微修改一下主题文件让网站变得稍微花里胡哨一点。




# 四、注意事项