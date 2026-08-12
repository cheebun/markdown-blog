TypeScript 配置选项

tsconfig.json

```javascript
{
  //
  // 编译选项
  //
  "compilerOptions": {

    // 解析非相对模块名的基准目录
    "baseUrl": "./src",

    // 模块名到基于 baseUrl的路径映射的列表
    "paths": {
      "render": ["../node_modules/render/src/render"], // 此处映射是相对于"baseUrl"
      "@/*": ["./*"]
    },

    // 编译指定目录下的工程
    "project": "",



    //
    // 文件输出
    //

    // 将输出文件合并为一个文件
    "outFile": "",

    // 重定向输出目录
    "outDir": "./dist",

    // 不生成输出文件
    "noEmit": false,

    // 报错时不输出文件
    "noEmitOnError": true,

    // 删除所有注释，除了以 /!*开头的版权信息
    "removeComments": false,

    // 不对具有 /** @internal */ JSDoc注解的代码生成代码
    "stripInternal": true,

    // 生成模块解析日志
    "traceResolution": false,



    //
    // JavaScript
    //

    // 是否编译 JS 文件
    "allowJs": false,

    // 在 JS 中报告错误
    "checkJs": true,

    // node_modules依赖的最大搜索深度并加载JavaScript文件, 仅适用于 allowJs.
    "maxNodeModuleJsDepth": 0,

    // 禁用 JavaScript 工程体积大小限制
    "disableSizeLimit": true,



    //
    // React
    //

    // 生成 JSX 代码种类 <preserve|react-native|react>
    "jsx": "react",

    // JSX 工厂函数
    "jsxFactory": "React.createElement",

    // 当目标为生成 "react" JSX时，指定 createElement和 __spread的调用对象
    "reactNamespace": "react",


    //
    // .d.ts
    //

    // 生成对应的 .d.ts 文件
    "declaration": true,

    // 为 .d.ts 文件生成sourceMap
    "declarationMap": false,

    // 生成 .d.ts 文件输出目录
    "declarationDir": "./lib",

    // 忽略 库的默认声明文件的类型检查
    "skipDefaultLibCheck": false,

    // 忽略所有的声明文件（ *.d.ts）的类型检查
    "skipLibCheck": false,

    // 只生成 .d.ts 文件
    "emitDeclarationOnly": false,

    // 要包含的类型声明文件路径列表, 只有该目录下的才会被包含进来
    "typeRoots": [],

    // 要包含在编译中的类型声明文件
    "types": [],

    // 不包含默认的库文件（ lib.d.ts）
    "noLib": false,

    // 不把 /// <reference``>或模块导入的文件加到编译文件列表
    "noResolve": false,



    //
    // 检查
    //

    // 严格检查
    "strict": true,

    // 以严格模式解析并为每个源文件生成 "use strict"语句
    "alwaysStrict": true,

    // 隐式 "any" 类型输出错误
    "noImplicitAny": true,

    // 严格 NULL 检查
    "strictNullChecks": true,

    // 禁用函数参数双向协变检查
    "strictFunctionTypes": true,

    // 类中初始化属性严格检查
    "strictPropertyInitialization": true,

    // 带隐式 "any" 的 "this" 表达式输出错误
    "noImplicitThis": true,

    // 若有未使用的局部变量则抛错
    "noUnusedLocals": true,

    // 若有未使用的参数则抛错
    "noUnusedParameters": true,

    // 不是函数的所有返回路径都有返回值时报错
    "noImplicitReturns": true,

    // 报告 switch 语句中遇到 fallthrough 情况的错误
    "noFallthroughCasesInSwitch": true,

    // 不报告执行不到的代码错误
    "allowUnreachableCode": false,

    // 不报告未使用的标签错误
    "allowUnusedLabels": false,

    // 禁止对同一个文件的不一致的引用
    "forceConsistentCasingInFileNames": false,

    // 禁用在函数类型里对泛型签名进行严格检查
    "noStrictGenericChecks": false,

    // enusre非未定义的类属性在构造函数初始化
    "strictPropertyInitialization": true,

    // 阻止对对象字面量的额外属性检查
    "suppressExcessPropertyErrors": false,

    // 阻止 --noImplicitAny 对缺少索引签名的索引对象报错
    "suppressImplicitAnyIndexErrors": false,



    //
    //  编码
    //

    // 输出编码
    "charset": "utf8",

    // 添加 BOM 头
    "emitBOM": false,

    // 生成文件指定结束换行符 <LF|CRLF>
    "newLine": "LF",



    //
    // ES 7 装饰器特性
    //

    // 给源码里的装饰器声明加上设计类型元数据
    "emitDecoratorMetadata": true,

    // 启用实验性的ES装饰器
    "experimentalDecorators": true,



    //
    // 模块
    //

    // 目录 ECMAScript 版本 <ES3|ES5|ES2015|ES2016|ES2017|ES2018|ESNEXT>
    "target": "ES5",

    // 生成指定模块种类 <none|commonjs|amd|system|umd|es2015|ESNext>
    // 默认根据 target 而定, 如果没有指定 target, 则为 commonjs
    "module": "none",

    // 决定如何处理模块 <node|classic>
    "moduleResolution": "classic",

    // 允许从没有设置默认导出的模块中默认导入
    "allowSyntheticDefaultImports": true,

    // 通过为所有导入创建命名空间对象来启用 CommonJS 和 ES 模块之间的发出互操作性。表示 "allowSyntheticDefaultImports"。
    "esModuleInterop": false,

    // 导入辅助函数
    "importHelpers": false,

    // 将每个文件作为单独的模块（与“ts.transpileModule”类似）。
    "isolatedModules": false,

    // 2.9+
    // 包含以'.json'扩展名导入的模块
    "resolveJsonModule": false,



    //
    // sourceMap
    //

    // 生成源码地图
    "sourceMap": true,

    // 生成单个sourcemaps文件，而不是将每sourcemaps生成不同的文件。
    "inlineSourceMap": false,

    // 将代码与sourcemaps生成到一个文件中，要求同时设置了 --inlineSourceMap 或 --sourceMap属性
    "inlineSources": false,

    // 为调试器指定指定sourcemap文件的路径
    "mapRoot": "",


    //
    // 信息输出
    //

    // 显示诊断信息
    "diagnostics": true,

    // 错误信息显示语言
    "locale": "zh-cn",

    // 不截短错误信息
    "noErrorTruncation": false,

    // 打印出编译后生成文件的名字。
    "listEmittedFiles": true,

    // 编译过程中打印文件名。
    "listFiles": true,

    // 更漂亮的错误输出
    "pretty": true,


    //
    // 兼容性
    //
    
    // 包含库文件
    // ['es5' 'es6' 'es2015' 'es7' 'es2016' 'es2017' 'es2018' 'esnext' 'dom' 'dom.iterable' 'webworker' 'scripthost' 'es2015.core' 'es2015.collection' 'es2015.generator' 'es2015.iterable' 'es2015.promise' 'es2015.proxy' 'es2015.reflect' 'es2015.symbol' 'es2015.symbol.wellknown' 'es2016.array.include' 'es2017.object' 'es2017.sharedmemory' 'es2017.string' 'es2017.intl' 'es2017.typedarrays' 'es2018.promise' 'es2018.regexp' 'esnext.array' 'esnext.asynciterable']
    "lib": ["dom", "es7"],

    // 模块输出中不包含 "use strict"指令
    "noImplicitUseStrict": false,

    // 让 ES3, ES5 支持 for of
    "downlevelIteration": false,

    // 将'keyof'解析为字符串赋值的属性名称（无数字或符号）。   
    "keyofStringsOnly": false,

    // 保留 const 和 enum 声明
    "preserveConstEnums": false,

    // 不把符号链接解析为其真实路径
    "preserveSymlinks": false,

    // 不在输出文件中生成用户自定义的帮助函数代码
    "noEmitHelpers": false,


    // 指定TypeScript源文件的路径，以便调试器定位
    "sourceRoot": "",

    // 仅用来控制输出的目录结构 --outDir
    "rootDir": "",

    // 根（root）文件夹列表，表示运行时组合工程结构的内容。
    "rootDirs": [],

    // 保持过时的控制台输出处于“监视”模式，而不是清除屏幕。
    "preserveWatchOutput": false,

    // 插件
    "plugins": [],

    // 监听文件
    "watch": false,
  },

  // 文件路径列表
  "files": [],

  // 包含文件或目录
  "include": [],

  // 排除目录或文件
  "exclude": [],

  // extends 继承配置
  "extends": "",

  // 此项目的自动类型（.d.ts）采集选项。
  "typeAcquisition": {},

  // 可以让IDE在保存文件的时候根据tsconfig.json重新生成文件
  "compileOnSave": false,

}
```
