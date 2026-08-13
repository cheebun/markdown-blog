## 问题

默认情况下，通过 Vue CLI 4 启动的开发服务器只能通过 `localhost` 访问，局域网内其他设备（如手机、其他电脑）无法通过本机 IP 地址访问该服务。

## Vue CLI 4 的解决方式（已过时）

> **⚠️ Vue CLI 已停止维护（EOL）**，现代 Vue 项目请使用 [Vite](https://cn.vitejs.dev/)（截至本文更新时最新大版本为 **Vite 8**，参见 [Vite Releases](https://vite.dev/releases)）。以下方案仅供维护遗留 Vue CLI 项目时参考。

在根目录建立 `vue.config.js`，加入：

```javascript
module.exports = {
  devServer: {
    disableHostCheck: true,
  },
}
```

## Vite 的解决方式（推荐）

Vite 默认同样只监听 `localhost`，允许局域网 IP 访问需要开启 `host` 选项。

### 方式一：命令行参数

```bash
vite --host
```

### 方式二：配置文件

在 `vite.config.js` 中设置：

```javascript
import { defineConfig } from 'vite';

export default defineConfig({
  server: {
    host: true, // 等价于 --host，监听所有地址，包括局域网和公网地址
  },
});
```

设置后，启动开发服务器时终端会额外打印出局域网可访问的 `Network` 地址，使用该地址即可在同一局域网内的其他设备上访问。

## 参考

[Vite - Server Options](https://vite.dev/config/server-options.html#server-host)    
[Vite Releases](https://vite.dev/releases)    
