---
title: "用 Homebrew 释放你的 Mac"
date: 2018-09-01
draft: false
---

初次使用 macOS，免不了要一番探索，探索的过程中发现了一个叫 Homebrew 的工具。于是在搜索引擎和各类文章的指引下，折腾了许久，发现确实可以有效提高生产力，现在整理如下，以备以后查看。

Homebrew 也称 brew，是专门为 macOS 准备的包管理工具。brew 能方便地管理软件的安装、更新、卸载、依赖等。
类似的有

- CentOS 的 yum
- Ubuntu 的 apt-get
- Windows 的 chocolatey
- Node.js 的 npm
- Python 的 pip
- Ruby 的 gem
- Go 的 dep

等等。

## 安装 Homebrew

在终端中执行下面的命令即可：

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

这个命令会先下载 install 文件，然后用 ruby 执行。

如果遇到安装卡住，可能是网络问题，请参考 **解决网络问题** 章节完成安装。

## Homebrew 常用命令

- brew help：帮助信息
- brew help [COMMAND] 或 brew [COMMAND] -h：子命令帮助信息
- brew -v：查看 homebrew 版本
- brew doctor：诊断问题
- brew config：查看 homebrew 配置信息
- brew update：更新 homebrew 自身
- brew search：搜索软件
- brew info：查询软件信息
- brew install：安装软件
- brew upgrade：更新软件
- brew uninstall：卸载软件
- brew list：查询已安装的软件
- brew outdated：查询可更新的软件
- brew cask install：安装 GUI 软件
- brew cask upgrade：更新 GUI 软件
- brew cask uninstall：卸载 GUI 软件
- brew cask list：查询已安装的 GUI 软件
- brew cask outdated：查询可更新的 GUI 软件
- brew cleanup：清理软件
- brew services：管理服务
- brew services list：查询服务列表

## 日常升级流程

```bash
# 更新 Homebrew ，及软件列表
brew update
# 列出过期软件
brew outdated
# 升级所有过期软件或者指定的某个软件
brew upgrade
brew upgrade <formula>
# 清理旧版本的软件
brew cleanup
```

## 解决网络问题

由于多种多样的原因，安装和使用 Homebrew 的时候可能会遇到网络问题，可以通过下面的方法解决。

### 获取 install 文件

```
cd ~
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

### 编辑 brew_install 文件

```
#!/System/Library/Frameworks/Ruby.framework/Versions/Current/usr/bin/ruby
# This script installs to /usr/local only. To install elsewhere you can just
# untar https://github.com/Homebrew/brew/tarball/master anywhere you like or
# change the value of HOMEBREW_PREFIX.
HOMEBREW_PREFIX = "/usr/local".freeze
HOMEBREW_REPOSITORY = "/usr/local/Homebrew".freeze
HOMEBREW_CACHE = "#{ENV["HOME"]}/Library/Caches/Homebrew".freeze
HOMEBREW_OLD_CACHE = "/Library/Caches/Homebrew".freeze
#BREW_REPO = "https://github.com/Homebrew/brew".freeze
BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze
#CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze
CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze
```

注释掉 BREW_REPO = "https://github.com/Homebrew/brew".freeze 和 CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze

修改为 BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze 和 CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze

可以看出 Homebrew 本身是基于其 git 仓库的，修改镜像源的时候修改 remote 地址就可以了。

### 安装 Homebrew

```
/usr/bin/ruby ~/brew_install
```

运行修改了的 brew_install 文件。

### 修改 homebrew 源

```
cd "$(brew --repo)"
git remote set-url origin git://mirrors.ustc.edu.cn/brew.git
```

### 修改 homebrew-core 源

```
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git
```

### 修改 bintray 源

```
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```


## 参考链接

- [https://brew.sh/](https://brew.sh/)
- [用 Homebrew 带飞你的 Mac](https://www.jianshu.com/p/61f998d89c34)
- [Mac下使用国内镜像安装Homebrew](https://www.jianshu.com/p/6523d3eee50d)
- [卸载Macports，安装Homebrew](https://www.jianshu.com/p/f9b2c74cb519)
