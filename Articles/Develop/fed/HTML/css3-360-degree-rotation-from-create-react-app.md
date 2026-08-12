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
