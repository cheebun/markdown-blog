# Mac OS 下有什么好用的软件包管理工具?

在 Mac OS X 下，我推荐使用 Homebrew + Cakebrew 来管理安装包。

## Homebrew

Mac OS X 缺失软件包管理器

### 安装 Homebrew

安装 `Homebrew` 前, 需要安装 `Command Line Tools (CLT) for XCode`。

在命令行输入 `xcode-select --install` 安装 `Command Line Tools (CLT) for XCode` 即可

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

在国内环境, 请使用以下命令安装。

```bash
HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git" \
HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git" \
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/Homebrew/install@master/install.sh)"
```

### 卸载

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall.sh)"
```

&nbsp;

### 增加 Taps

```
brew tap homebrew/core
brew tap homebrew/cask
brew tap homebrew/cask-drivers
brew tap homebrew/cask-fonts
brew tap homebrew/services
```

在国内环境, 请使用以下命令安装。

```bash
brew tap --custom-remote --force-auto-update homebrew/core         https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
brew tap --custom-remote --force-auto-update homebrew/cask         https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
brew tap --custom-remote --force-auto-update homebrew/cask-fonts   https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-fonts.git
brew tap --custom-remote --force-auto-update homebrew/cask-drivers https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-drivers.git
brew tap --custom-remote --force-auto-update homebrew/services     https://github.com/Homebrew/homebrew-services.git
```

（`hub.fastgit.xyz` 镜像已失效，`homebrew/services` 暂无可用国内镜像，直接使用官方地址即可。）

&nbsp;

### 使用方法

#### 安装包

```bash
brew install wget
```

#### 卸载包

```bash
brew remove wget
```

#### 搜索包

```bash
brew search wget
```

&nbsp;

## Cakebrew

Homebrew 管理 App, 一个图形化的 Homebrew 管理工具。

> 注意：Cakebrew 已停止维护，最后一个版本发布于 2021 年，仅作为可选的图形化工具参考。

### 安装 Cakebrew

```bash
brew install --cask cakebrew
```

&nbsp;

### 安装常用软件

#### 浏览器

```bash
brew install --cask google-chrome microsoft-edge vivaldi
```

#### 聊天

```bash
brew install --cask qq wechat
```

#### 音乐

```bash
brew install --cask qqmusic neteasemusic
```

#### 办公

```bash
brew install --cask dingtalk wechatwork wechatwebdevtools
```

#### Code

```bash
brew install --cask visual-studio-code intellij-idea sublime-text macvim
```

#### Other

```bash
brew install --cask iterm2 \
  upic \
  switchhosts \
  docker \
  cheatsheet \
  cakebrew \
  postman \
  keycastr
```

#### 付费应用

```bash
brew install --cask \
  bartender \
  mindjet-mindmanager \
  xmind-zen \
  navicat-premium \
  tower \
  alfred \
  betterzip \
  sip \
  ssh-config-editor
```
