# React Router 404 错误拦截处理

我们先定义两个页面, 一个 Home 页和一个 NotFound 页面。

Home.jsx

```javascript
import React, { Component } from 'react';

export default class Home extends Component {
  render() {
    return {
      <div>
        <h1>Hello Home!</h1>
      </div>
    }
  }
}
```

404页面

```javascript
export default class NotFound extends Component {
  render() {
    const { pathname } = this.props.location;

    return (
      <div>
        <div style={{'color':'#000'}}>404未找到<code>{ pathname }</code>页面</div>
      </div>
    )
  }
}
```

## 方法一

重定向

```javascript
import React, { Component } from 'react';
import { BrowserRouter as Router, Route, Switch, Redirect } from 'react-router-dom';

class Routers extends Component {
  render() {
    return (
      <Router basename="/">
        <Switch>
          <Route exact path="/" component={ Home }/>

          <Route path='/404' component={ NotFound } />
          <Redirect from='*' to='/404' />
        </Switch>
      </Router>
    )
  }
}

export default Routers;

```

## 方法二

路由匹配

```javascript
import React, { Component } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

class Routers extends Component {
  render() {
    return (
      <Router basename="/">
        <Switch>
          <Route exact path="/" component={ Home }/>
          <Route path='*' component={ NotFound } />
        </Switch>
      </Router>
    )
  }
}

export default Routers;
```
