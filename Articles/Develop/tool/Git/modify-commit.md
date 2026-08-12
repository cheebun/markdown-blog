# 修改 commit

## 第一步

### 未提交

```bash
git commit --amend
```

### 历史提交

```bash
git rebase -i HEAD~1
```

## 第二步

修改 pick 为 edit

```bash
git commit --amend
git rebase --continue
```
