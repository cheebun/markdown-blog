# VSCode : JavaScript 语法开启智能提示

之前写 `React` 写的时候, 用得是 `TypeScript` 有语法提示。

后来写 `JavaScript` 的时候, 没有语法提示, 不过可能写多了, `React` 的方法, 倒是记得一清二楚的。

最近, 在 `React` 交流群的时候, 有群友问到, 所以, 简单的查了一下。

网上说用 `typings`, 就在 `2017` 年的时候, 我还折腾过这东西, 这个东西其实也过时了。

后来, 想了一下, `typings` 下载的定义文件, 不就是现在 `TypeScript` 使用的定义文件是一样的吗？

## 安装定义文件

```bash
yarn add @types/node @types/react @types/react-dom
```

OR

```bash
npm install @types/node @types/react @types/react-dom
```

## 开启智能提示

在代码编辑区里，使用 `Ctrl + Space` 快捷键 或使用 `Ctrl + Alt + Space` 就可以有提示了。
