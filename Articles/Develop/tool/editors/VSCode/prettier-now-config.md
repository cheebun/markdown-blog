# VSCode Prettier Now 格式化配置

## 规则读取顺序

直接读取 `VSCode Prettier Setting`, 可能, 不会读取 `.editorconfig`.

目前所知道, Prettier Now 是根本不会去读取 `.prettierrc` 的。

## 配置

```javascript
{
  // 保存格式化
  "editor.formatOnSave": true,

  // 140 个字符后折行
  "prettier.printWidth": 140,

  // 单引号
  "prettier.singleQuote": true,

  // 尾随逗号 <none, es5, all>
  "prettier.trailingComma": "none",

  // Tab 宽
  "prettier.tabWidth": 2,

  // 使用制表符 true 制表符 / false 空格
  "prettier.useTabs": false,

  // 括号添加空格
  "prettier.bracketSpacing": false,

  // 箭头函数参数始终放置圆括号
  "prettier.arrowParens": false,  

  // JSX. 把>放置在最后一行末尾
  "prettier.jsxBracketSameLine": false,

  // 语句末尾添加分号
  "prettier.semi": true,

  // 箭头函数参数始终放置圆括号 <true|false>
  "prettier.arrowParens": true,

  // 括号
  "prettier.bracesSpacing": true,

  // 数组展开
  "prettier.arrayExpand": false,                                                                
  // JSX 单引号
  "prettier.jsxSingleQuote": true,

  // 更好的错误信息输出
  "prettier.openOutput": true，

  // 匿名函数省略空格
  "prettier.noSpaceEmptyFn": false,

  // 函数括号前始终插入空格
  "prettier.spaceBeforeFunctionParen": false,

  // 三元运算
  "prettier.flattenTernaries": false,

  // 允许属性名和值断行
  "prettier.breakProperty": false,

  // else放置在新行
  "prettier.breakBeforeElse": false,

  // 滚动到错误行
  "prettier.autoScroll": true,

  // 对齐冒号
  "prettier.alignObjectProperties": false,

  // 样式文件启用
  "prettier.cssEnable": ["css", "less", "scss", "postcss"],

  // GraphQL
  "prettier.graphqlEnable": ["graphql"],

  // JavaScript 启用
  "prettier.javascriptEnable": [],

  // JSON启用
  "prettier.jsonEnable": ["json"],

  // TypeScript
  "prettier.typescriptEnable": [],  
}
```
