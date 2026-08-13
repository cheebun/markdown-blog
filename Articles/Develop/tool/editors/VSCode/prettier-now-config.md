# VSCode Prettier Now 格式化配置（已废弃）

> `Prettier Now` 扩展已停止维护, 且下方配置项（`prettier.*` 系列设置）在当前 VSCode 中已全部失效。
> 请改用官方扩展 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)（`esbenp.prettier-vscode`）, 并通过项目根目录下的 `.prettierrc` 文件配置规则, 参见 [prettier-config.md](./prettier-config.md)。

## 迁移方式

1. 卸载 `Prettier Now`, 安装 `esbenp.prettier-vscode`（当前 Prettier 稳定版为 3.9.6, 来源: [npm](https://www.npmjs.com/package/prettier)）。
2. VSCode 设置中仅保留:

```javascript
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

3. 在项目根目录新增 `.prettierrc`, 按原配置意图迁移:

```json
{
  "printWidth": 140,
  "tabWidth": 2,
  "useTabs": false,
  "singleQuote": true,
  "semi": true,
  "trailingComma": "none",
  "arrowParens": "always",
  "bracketSpacing": false
}
```

字段与旧版 `prettier.*` 设置的对应关系: `printWidth` ← `prettier.printWidth`, `singleQuote` ← `prettier.singleQuote`, `trailingComma` ← `prettier.trailingComma`, `tabWidth`/`useTabs` ← `prettier.tabWidth`/`prettier.useTabs`, `semi` ← `prettier.semi`, `arrowParens` ← `prettier.arrowParens`, `bracketSpacing` ← `prettier.bracketSpacing`。
