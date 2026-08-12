公司项目依赖 `package.json` 中的 `version` 属性。

每次编译时, 都要手动更改版本, 后来, 是通过一个脚本更新版本。

## Npm

后来发现 `npm` 提供了一个方法来更新版本。

```
npm version <newversion>
```

在后来, 发现 `npm` 能自动增长版本。

```
npm version patch
```

但是, 有个问题, 就是会自己给 `git` 增加一个 `tag`。

然后, 发现了 `--no-git-tag-version` 和 `--no-commit-hooks` 参数

```
npm version patch --no-git-tag-version --no-commit-hooks
```

## Yarn

在 `npm` 和 `yarn` 之间, 我更喜欢 `yarn`, 那能不能通过 `yarn` 命令行来更新版本呢？

```
yarn version --patch --no-git-tag-version --no-commit-hooks
```

## 参考

[yarn version](https://yarnpkg.com/lang/en/docs/cli/version/)
