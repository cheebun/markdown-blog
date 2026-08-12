# 调整 Launchpad 图标大小?

## 调整 Launchpad 图标大小

调整 Launchpad 行列数，就能放大缩小 Launchpad 图标大小。

我个人觉得看着最舒服的图标大小为行数为 8 行，列数为 6 列的时候。

调整 Launchpad 显示行数（系统默认为 7 行）

```bash
defaults write com.apple.dock springboard-columns -int 8
```

调整 Launchpad 显示列数（系统默认为 5 列）
```bash
defaults write com.apple.dock springboard-rows -int 6
```

调整后，需要重置 Launchpad
```
defaults write com.apple.dock ResetLaunchPad -bool TRUE;
killall Dock
```

&nbsp;

## 恢复 Launchpad 图标大小

恢复行

```bash
defaults write com.apple.dock springboard-columns Default
```

恢复列

```
defaults write com.apple.dock springboard-rows Default
```

重启 Launchpad

```
killall Dock
```
