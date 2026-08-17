# 从 create-react-app 学习 CSS3 360度旋转

## HTML

```html
<div className="firstScreen">
  <div className="brand" />
</div>
```

## CSS3

```scss
@mixin size($width, $height: $width) {
  width: $width;
  height: $height;
}

.firstScreen {
  @include size(100vw, 100vh);
  background-color: #222;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  .brand {
    @include size(30vmin);
    background-image: url('./../../assets/images/logo.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100%;
    animation: rotate infinite 20s linear;
  }
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

## 现代 CSS 等价写法

### SCSS 语法说明

上面的代码使用了两个 SCSS（Sass）特性：

- **`@mixin` / `@include` 带默认参数**：`size($width, $height: $width)` 定义了一个带有默认值的 mixin，当只传一个参数时 `$height` 自动等于 `$width`，实现正方形尺寸的简写。
- **嵌套规则**：`.firstScreen { .brand { ... } }` 是 Sass 的嵌套语法，编译后展开为 `.firstScreen .brand { ... }`，原生 CSS 不支持此写法。

### 原生 CSS 现状

**CSS 原生嵌套**已于 2023-12-11 成为 Baseline Newly Available，2026 年 6 月正式升级为 **Baseline Widely Available**（Chrome 112+、Firefox 117+、Safari 16.5+；宽松语法 Chrome 120+/Safari 17.2+ 起支持）。需注意：`&` 通过 `:is()` 语义解析，不支持 Sass 风格的 `&__element` 字符串拼接。

**`@scope`** 于 2025 年 12 月成为 Baseline Newly Available（Chrome 118+、Safari 17.4+、Firefox 146+），可用 `@supports at-rule(@scope)` 做特性检测。

### 转换后的纯 CSS 版本

用 `@scope` + 原生嵌套 + CSS 自定义属性替代 `size()` mixin：

```css
@scope (.firstScreen) {
  :scope {
    --brand-size: 30vmin;
    width: 100vw;
    height: 100vh;
    background-color: #222;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .brand {
    width: var(--brand-size);
    height: var(--brand-size);
    background-image: url('./../../assets/images/logo.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100%;
    animation: rotate infinite 20s linear;
  }
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
```

### 注意事项

- **CSS 变量 vs mixin 默认参数**：`--brand-size` 可复用值，但 CSS 变量无法像 Sass mixin 那样实现"仅传一个参数时自动推导另一个"的逻辑。
- **`@keyframes` 名称是全局的**：建议加前缀（如 `firstScreen-rotate`）避免页面级命名冲突。
- **旧浏览器回退**：不支持 `@scope` 时，可改用平铺的后代选择器 `.firstScreen .brand { ... }` 作为降级方案。

### 参考资料

- [CSS Nesting — web-platform-dx Web Features Explorer](https://web-platform-dx.github.io/web-features-explorer/features/nesting/)
- [@scope Browser Support — TestMuAI](https://www.testmuai.com/learning-hub/css-scope-browser-support/)
- [Baseline — web.dev](https://web.dev/baseline)
