# React 从 antd Menu 学习父组件获取子组件 key 研究

最近研究组件封装, 在参考 `antd` 的 [菜单](http://ant.design/components/menu-cn/) 组件时, 发现在他们案例中的 `Item` 大量使用了 `key`。

```
import React, { Component } from "react";
import { Menu, Icon } from 'antd';

class App extends React.Component {
  render() {
    return (
    <Menu selectedKeys={[this.state.current]} mode="horizontal">
      <Menu.Item key="home">Home</Menu.Item>
      <Menu.Item key="mail">Mail</Menu.Item>
    )
  }

}
```

而且所有事件和 `key` 有关, 于是就细细研究了一下。他们的菜单其实是对 `rc-menu` 的一个封装。

后来, 分析到了 `rc-menu` 中的 `SubPopupMenu.jsx` 文件。

还是不说了, 看例子吧。

下来, 我们来简单模拟一下, 如何获取子元素 `key`。

开始前, 我们来一个调用, 假设我有一个菜单, 菜单里有N个项目。

```javascript
import React, { Component } from "react";

import Menu from '@/components/Menu';

export default class App extends Component {
  render = () => (
    <Menu>
      <Menu.Item key="home">Home</Menu.Item>
      <Menu.Item key="mail">Mail</Menu.Item>
    </Menu>
  );
}
```

先来个菜单 `item` 元素组件

MenuItem.jsx

```javascript
import React, { Component } from "react";

export default class MenuItem extends Component {
  render = () => <li>{ this.props.children }<li>;
}
```

在来一个菜单 `menu` 元素组件

这里用到了两个React Api。 `Children` 和 `cloneElement`, 你们可以在 [这里](https://reactjs.org/docs/react-api.html) 查看 `React` 的 Api。

Menu.jsx

```javascript
import React, { Component, Children, cloneElement } from "react";
import MenuItem from './MenuItem';

export default class Menu extends Component {
  // 静态属性, 可以通过 Menu.Item 来创建 item 组件
  static Item = MenuItem;

  render = () => {
    const { props } = this;
    const { className, children } = props;

    return (
      <ul className={ className }>
        {
          // 通过 Children Api 的 map 方法, 遍历 children
          Children.map(children, (child) => {

            // 克隆元素, 并返回新的 React Element
            // cloneElement(elem, props)
            cloneElement(child, {

              // 从 children 里拿出 key, 赋值给eventKey, 经过 React 处理后, key 便不可以访问
              eventKey: child.key
            });
          });
        }
      </ul>
    );
  };
}
```

简单的来说, 就是把 `children` 的 `key` 赋予给 `props.eventKey`, 子组件然后对 `eventKey` 各种处理包装, 返回给父组件的一个过程。
