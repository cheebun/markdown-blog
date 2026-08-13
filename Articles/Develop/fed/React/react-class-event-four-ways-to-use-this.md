# React class 中的事件 4 种使用 this 的方法

> **⚠️ 内容已过时**：本文针对的是 React Class 组件中的 `this` 绑定问题。这是历史遗留（legacy）写法，现代 React 推荐使用**函数组件 + Hooks**，函数组件不存在 `this` 绑定问题，因此本文所述场景已不再适用于新项目。建议阅读：
> - [React 官方文档 - 组件与 Hooks](https://react.dev/learn)
> - [React 官方文档 - 使用状态响应输入](https://react.dev/learn/responding-to-events)

## React 两种 bind 方式

### 构造函数内绑定

一个两个事件, 这种方式书写, 倒是也无伤大雅, 如果是每个组件都有五个以上的事件绑定呢？我感觉这种写法就是地狱般的存在。

```javascript
export default class App extends Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind();
  }

  handleClick() {
    console.log(this);
  }

  render() {
    return (
      <div onClick={this.handleClick}>点我</div>
    );
  }
}
```

### JSX语句内绑定

这种方式省略了构造函数, 但是每个事件后面都要加bind, 最后依然是地狱的存在。

```javascript
export default class App extends Component {
  handleClick() {
    console.log(this);
  }

  render() {
    return (
      <div onClick={this.handleClick.bind(this)}>点我</div>
    );
  }
}
```

## 两种非箭头函数处理方式

### JSX 语句使用箭头函数

这种方式和第二种方式, 感觉差别不大。

```javascript
export default class App extends Component {
  handleClick() {
    console.log(this);
  }

  render() {
    return (
      <div onClick={() => this.handleClick}>点我</div>
    );
  }
}
```

### 使用class property 加 胖箭头方法

推荐

```javascript
export default class App extends Component {
  handleClick = () => {
    console.log(this);
  }

  render() {
    return (
      <div onClick={this.handleClick}>点我</div>
    );
  }
}
```
