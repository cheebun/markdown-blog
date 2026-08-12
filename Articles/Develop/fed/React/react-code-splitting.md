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

## Loadable

```javascript
import React, { memo } from 'react';

const Loading = memo(function Loading({ error, retry, pastDelay, timedOut }) {
  if (error) {
    return <div>Error! <button onClick={retry}>Retry</button></div>;
  }

  if (pastDelay) {
    return <div>Loading...</div>;
  }

  if (timedOut) {
    return <div>Taking a long time... <button onClick={retry}>Retry</button></div>;
  }

  return null;
});

export default Loading;
```

```javascript
import ReactLoadable from 'react-loadable';
import Loading from '@/components/Loading';

function Loadable(options) {
  const defaultOptions = {
    loading: Loading,
    delay: 200,
    timeout: 10000,
  }

  return ReactLoadable({ ...defaultOptions, ...options });
}

export default Loadable;
```

```javascript
import Loadable from '@/components/helpers/Loadable';
import Home from "@/pages/home";

const routes = [
  {
    name: "首页",
    path: "/",
    component: Home,
    exact: true, // 精确匹配
    strict: true, // 严格路由
    tabbar: true, // 标签栏
  },
  {
    name: "发现",
    path: "/discover",
    component: Loadable({ loader: () => import('@/pages/discover') }),
    exact: true, // 精确匹配
    strict: true, // 严格路由
    tabbar: true, // 标签栏
  },
];

export default routes;
```

## 参考

[How do I avoid repetition?](https://github.com/jamiebuilds/react-loadable#how-do-i-avoid-repetition)    
[Route-based code splitting](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting)    
[React 16的异常处理 - componentDidCatch](https://github.com/Acgsior/Acgsior/blob/master/source/_posts/react-16-error-handling.md)    
[react v16.6 动态 import，React.lazy()、Suspense、Error boundaries](http://www.ptbird.cn/react-lazy-suspense-error-boundaries.html)    
