---
title: "使用 Hugo 构建个人 Blog"
date: 2018-08-11T08:39:13+08:00
draft: false
---

最开始接触静态网站生成器是在用 Github Pages 搭建个人博客的时候，折腾的是 Github Pages 默认的静态网站构建工具 [Jekyll](https://jekyllrb.com/)，Jekyll 使用 Ruby 语言开发。后来接触了使用 Node.js 开发的静态网站构建工具 [Hexo](https://hexo.io/)。使用过程中都有不顺手的地方，但博客也没怎么写，所以也没去纠结。

最近重新整理博客，决定尝试使用 Hugo 作为静态网站构建工具，相关内容记录如下。

# Hugo

Hugo 是一个开源、免费的静态网站生成器，用 Go 语言编写，使用简单方便，快速高效。

Hugo 的官网地址：https://gohugo.io/

## 安装 Hugo

首先是安装 Hugo，以 macOS 为例，使用 Homebrew 安装。更多安装请参考 https://gohugo.io/getting-started/installing/

```bash
brew install hugo
```

验证 Hugo 是否安装成功

```bash
hugo version
# 或者
hugo help
```

## 新建一个网站项目

```bash
hugo new site quickstart
```

这个命令会新建一个叫 quickstart 的文件夹，项目代码都在这个文件夹中。

目录结构如下：

```bash
├── archetypes
├── content
├── data
├── layouts
├── resources
├── static
├── themes
└── config.toml
```

其中

- content: 网站内容
- static: 静态资源，如 image 等，static 目录下的文件会被全部拷贝到网站生成的目录
- themes: 主题
- config.toml: 配置文件

更多目录结构信息，参考 https://gohugo.io/getting-started/directory-structure/

## 增加一个主题

```bash
cd quickstart
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke

# 修改 config.toml 文件，增加 Ananke 主题
echo 'theme = "ananke"' >> config.toml
```

官方示例用的 Ananke 主题挺不错的。另外有一款非常简洁的主题 black-and-light，但功能略显不足，因此 fork 了一个准备空闲时调教一下，https://github.com/gitjcc/hugo-blight-theme。

## 书写内容

```bash
hugo new posts/my-first-post.md
```

这个命令会在 content/posts 目录下新建一个名为 my-first-post.md 的 MarkDown 文件。用编辑器打开文件，尽情地书写吧。

## 本地预览

```bash
hugo server -D
```

打开 http://localhost:1313/ 即可预览网站，Hugo 会监测本地文件的变化，重新构建网站，并刷新浏览器。

## 自定义配置

config.toml

```bash
baseURL = "https://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```

更多配置项，参考 https://gohugo.io/getting-started/configuration/

## 生成静态网站

```bash
hugo
```

静态网站内容默认会生成到 public 目录下，可以通过 config.toml 来配置。

## 部署

至此，静态网站内容已准备就绪，只需要将这些静态内容部署到服务器上即可。

有些服务商提供在线构建服务，比如 [Netlify](https://www.netlify.com/)，只需要通过简单的配置即可享受，当然可以享受的不止在线构建。

更多部署方案，参考 https://gohugo.io/hosting-and-deployment/

## 后记

博客重要的是内容，生成器只是工具，选择一个用得顺手的就好。更多静态网站生成器见 https://www.staticgen.com/，总有一款适合你。

## 相关链接

- https://gohugo.io/
- https://www.staticgen.com/
- https://jamstack.org/
- https://headlesscms.org/
- https://github.com/netlify
