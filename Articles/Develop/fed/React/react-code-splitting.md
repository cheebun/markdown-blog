## Suspense + Lazy

```javascript
import React, { memo } from 'react';

const Loading = memo(function Loading() {
  return (
    <div>Loading...</div>
  )
});

export default Loading;
````

```javascript
import { lazy } from 'react';

const routes = [
  {
    name: "首页",
    path: "/",
    component: lazy(() => import('@/pages/home')),
    exact: true, // 精确匹配
    strict: true, // 严格路由
    tabbar: true, // 标签栏
  },
  {
    name: "发现",
    path: "/discover",
    component: lazy(() => import('@/pages/discover')),
    exact: true, // 精确匹配
    strict: true, // 严格路由
    tabbar: true, // 标签栏
  },
];

export default routes;
```

```javascript
import React, { memo, Suspense, lazy } from 'react';
import Loading from "@/components/loading";
import routes from "@/routes";

const App = memo(function App() {
  return (
    <>
      <Suspense fallback={<Loading />}>
        <Switch>
          {routes.map(({ name, tabbar, ...route }) => (
            <Route key={route.path} {...route} />
          ))}
        </Switch>
      </Suspense>
    </>
  );
});

export default App;
```

> 注：`react-loadable` 已于 2020 年停止维护（archived），已被 `React.lazy` + `Suspense` 取代，无需再引入该第三方库。

## 参考

[Route-based code splitting](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting)    
[React 16的异常处理 - componentDidCatch](https://github.com/Acgsior/Acgsior/blob/master/source/_posts/react-16-error-handling.md)    
[react v16.6 动态 import，React.lazy()、Suspense、Error boundaries](http://www.ptbird.cn/react-lazy-suspense-error-boundaries.html)    
