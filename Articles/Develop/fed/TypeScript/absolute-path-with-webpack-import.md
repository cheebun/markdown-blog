在 TypeScript 中使用 Webpack 导入的绝对路径

## webpack Configuration

```javascript
var path = require('path');

module.exports = {
  // ...

  resolve: {
    alias: [
      "@": path.resolve('./src'),
    ],
  },
};
```

现在, 不在是这样导入的

```javascript
import Header from './src/components/Header';
```

你可以像这样导入

```javascript
import Header from '@/components/Header';
```

## TypeScript Compiler

TypeScript 想要类似这样的功能, 就需要使用 baseUrl + paths 来实现了

```javascript
{
  compilerOptions: {
    // ...

    "baseUrl": "./src",
    "paths": {
      "@/*": ["*"],
    }
  }
}
```
