# VSCode Prettier 格式化配置

## 规则读取顺序

`.prettierrc > .editorconfig`, 如果 `.prettierrc` 不存在, 则 `.editorconfig > VSCode Prettier Setting`

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

  // 箭头函数参数始终放置圆括号 <avoid|always>
  "prettier.arrowParens": "always",

  // 多行 (Markdown) <always|never|preserve>
  "prettier.proseWrap": "preserve",
}
```
