# 前端开发者 Mac OS X 设置指南

## 前言

最新换了新的电脑, MacBook Pro (2022, 14-inch, M1 Pro).。

程序员的电脑装机意味着大量的配置、软件、插件都要进行设置，还很容易遗漏。

在装完机器后，专门整理了一下，并分享出来给大家参考。

## 配置

### XCode Command Line Tools

在 Mac OS X 终端中使用 `git` 命令会提示你安装 `xcode`。

但是我们前端开发并不需要完整的 `xcode`。

我们只需要安装 `Xcode Command Line Tools` 就可以了。

请使用下面命令安装:

```bash
xcode-select --install
```

### Homebrew

如果我们使用 `Homebrew` 官方提供的方法来安装 `Homebrew`。

可能会很慢，或者，根本无法安装。

你可以通过我提供的命令来安装。

```bash
HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git" \
HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git" \
HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles" \
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/Homebrew/install@master/install.sh)"
```

您需要将 `Homebrew` 添加到 `PATH`。

```bash
echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> $HOME/.zprofile
eval $(/opt/homebrew/bin/brew shellenv)
```

增加 Taps

```bash
brew tap --custom-remote --force-auto-update homebrew/core         https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
brew tap --custom-remote --force-auto-update homebrew/cask         https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
brew tap --custom-remote --force-auto-update homebrew/cask-fonts   https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-fonts.git
brew tap --custom-remote --force-auto-update homebrew/cask-drivers https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask-drivers.git
brew tap --custom-remote --force-auto-update homebrew/services     https://hub.fastgit.xyz/Homebrew/homebrew-services.git
```

### nvm

在之前版本，如果使用 `Homebrew` 安装 `nvm` 会出现各种提示。在新的版本，已经修复了。

这里我们使用 `Homebrew` 来安装 `nvm`。

```bash
brew install nvm
```

安装完毕，需要配置 `nvm` 添加到 `PATH`。

```bash
cat << EOF >> $HOME/.zprofile

# NVM
export NVM_NODEJS_ORG_MIRROR="https://npmmirror.com/mirrors/node/"
export NVM_DIR="\$HOME/.nvm"
[ -s "\$(brew --prefix nvm)/nvm.sh" ] && . "\$(brew --prefix nvm)/nvm.sh"
[ -s "\$(brew --prefix nvm)/etc/bash_completion.d/nvm" ] && . "\$(brew --prefix nvm)/etc/bash_completion.d/nvm"
EOF

source $HOME/.zprofile
```

安装 `node`。

```bash
nvm install --lts
nvm install stable
nvm alias default lts/krypton
```

### 字体

```bash
brew install --cask font-fira-code font-meslo-for-powerline font-sarasa-gothic
```

### 常用软件安装

```bash
brew install \
  wechat dingtalk \
  google-chrome microsoft-edge \
  visual-studio-code \
  iterm2 \
  docker
```
