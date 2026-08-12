## styled-components

@/global/styles.jsx

```javascript
import { createGlobalStyle } from 'styled-components';

const GlobalStyles = createGlobalStyle`
.fl { float: left }
.fr { float: right; }
.clearfix::after { display: block; content: ""; clear: both; }
.pointer:hover { cursor: pointer; }
`;

export default GlobalStyles;
```

App.jsx

```javascript
import React, { memo } from 'react';
import { Route, Switch } from "react-router-dom";

import GlobalStyles from '@/global/styles';

import ScrollTop from '@/components/common/ScrollTop';
import routes from "@/routes";

const App = memo(function App() {
  return (
    <>
      <GlobalStyles />

      <ScrollTop>
        <Switch>
            {routes.map(route => (
              <Route key={route.path} {...route} />
            ))}
          </Switch>
      </ScrollTop>
    </>
  )
});
```


## @emotion/core

@/global/styles.jsx

```javascript
import { css } from "@emotion/core";

const GlobalStyles = css`
.fl { float: left }
.fr { float: right; }
.clearfix::after { display: block; content: ""; clear: both; }
.pointer:hover { cursor: pointer; }
`;

export default GlobalStyles;
```


App.jsx

```javascript
import React, { memo } from 'react';
import { Route, Switch } from "react-router-dom";

import { Global } from '@emotion/core'
import GlobalStyles from '@/global/styles';

import ScrollTop from '@/components/common/ScrollTop';
import routes from "@/routes";

const App = memo(function App() {
  return (
    <>
      <Global styles={globalStyles} />

      <ScrollTop>
        <Switch>
            {routes.map(route => (
              <Route key={route.path} {...route} />
            ))}
          </Switch>
      </ScrollTop>
    </>
  )
});
```

## 参考

[Global Styles](https://emotion.sh/docs/globals)    
[styled-components API Reference](https://www.styled-components.com/docs/api#createglobalstyle)    
