# 16.4.0 生命周期一览和旧的生命周期回顾

React 在 16.4.0 版本更新了两个生命周期, `getSnapshotBeforeUpdate` 和 `getDerivedStateFromProps`。

在使用这两个生命周期时, 需要注意：

在 `getSnapshotBeforeUpdate` 或 `getDerivedStateFromProps` 时，需要移除下列生命周期

- componentWillMount
- UNSAFE_componentWillMount
- componentWillUpdate
- componentWillReceiveProps
- UNSAFE_componentWillReceiveProps
- UNSAFE_componentWillUpdate

## 生命周期

### 组件挂载

#### 16.4.x
- static getDerivedStateFromProps
- render
- componentDidMount

#### 16.3.x
- componentWillMount
- UNSAFE_componentWillMount
- render
- componentDidMount

### 组件更新

#### 16.4.x
- static getDerivedStateFromProps
- shouldComponentUpdate
- getSnapshotBeforeUpdate
- render
- componentDidUpdate

#### 16.3.x
- componentWillUpdate
- componentWillReceiveProps
- UNSAFE_componentWillReceiveProps
- shouldComponentUpdate
- UNSAFE_componentWillUpdate
- render
- componentWillUnmount

### 组件卸载
- componentWillUnmount

### 错误捕捉
- componentDidCatch

&nbsp;

## 代码演示

```javascript
import React, { Component } from 'react';

export default class App extends Component {

  /**
   * 在 DOM 更新之前
   * 该方法在 `DOM` 更新发生前的 “瞬间” 被调用, 返回值将作为 `componentDidUpdate` 的第三个参数。
   * 与 `componentDidUpdate` 一起使用，这个新的生命周期应该覆盖旧版 `componentWillUpdate` 的所有用例
   *
   * @param nextProps 修改后的Props
   * @param prevState 修改前的State
   * @returns * 返回值将作为 `componentDidUpdate` 的第三个参数
   */
  public getSnapshotBeforeUpdate(nextProps: object, prevState: object): void {
    return null;
  }

  /**
   * getDerivedStateFromProps
   * 该方法在组件实例化以及接收新 Props 后调用。 它可以返回一个对象来更新状态，或者返回null来表示新的 Props 不需要任何状态更新。
   * 与 `componentDidUpdate` 一起使用，这个新的生命周期应该覆盖传统 `componentWillReceiveProps` 的所有用例。
   *
   * @param props Props
   * @param state State
   * @returns 状态或null
   */
  public static getDerivedStateFromProps(props: object, state: object): void {
    return null;
  }

  public componentWillMount(): void {
    // 组件挂载前
  }

  public UNSAFE_componentWillMount(): void {
    // 组件挂载前
  }

  // 常用
  public componentDidMount(): void {
    // 组件挂载后
  }





  public shouldComponentUpdate(nextProps: object, nextState: object, nextContext: any): boolean {
    // 组件是否应该更新
    return true;
  }

  public componentWillUpdate(nextProps: object, nextState: object, nextContext: any): void {
    // 组件更新前
  }

  public UNSAFE_componentWillUpdate(nextProps: object, nextState: object, nextContext: any): void {
    // 组件更新前
  }

  public componentDidUpdate(): void {
    // 组件更新后
  }

  public componentWillReceiveProps(nextProps: object, nextContext: any): void {
    // 组件获得Props前
  }

  public UNSAFE_componentWillReceiveProps(nextProps: object, nextContext: any): void {
    // 组件获得Props前
  }

  public componentDidCatch(error: Error, errorInfo: ErrorInfo): void {
    // 错误处理
  }

  public componentWillUnmount(): void {
    // 组件卸载前
  }

  public render(): React.ReactNode {
    // 渲染
    return (
      true
    )
  }
}
```

## 参考链接

[React.Component](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)    

[Update on Async Rendering]( https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html)    

[讲讲今后 React 异步渲染带来的生命周期变化]( https://juejin.im/post/5abf4a09f265da237719899d)    

[React的生命周期]( https://www.cnblogs.com/yangzhou33/p/8799278.html)
