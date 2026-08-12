# VSCode 让 JSX 后缀支持 Emmet

首选项 > 设置 > 用户设置

```javascript
{
  // 配置emmet是否启用tab展开缩写
  "emmet.triggerExpansionOnTab": true,

  // 配置emmet对文件类型的支持
  "emmet.syntaxProfiles": {
    "Typescript React": "tsx",
    "typescript": "typescriptreact",

    "JavaScript React": "jsx",
    "javascript": "javascriptreact",
  },
}
```
