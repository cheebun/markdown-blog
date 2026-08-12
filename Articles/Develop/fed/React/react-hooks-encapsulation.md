```javascript
import { useState, useCallback } from 'react';

/**
 * 多层嵌套的状态
 *
 * @params initialState - 状态初始
 */
export function useLegacyState(initialState) {
  const [state, setState] = useState(initialState);
  const setLegacyState = useCallback((nextState) => setState({ ...state, ...nextState}), []);
  return [state, setLegacyState];
}
```

```javascript
import { useEffect } from 'react';

/**
 * Did Mount
 * @param {() => void} mount - Mount Function
 */
function useDidMount(effect) {
  useEffect(effect, []);
}
```

```jsx
import { useEffect } from 'react';

/**
 * Will Unmount
 * @param {() => void} unmount - Unmount Function
 */
function useUnmount(effect) {
  useEffect(() => () => {
    if (effect) effect();
  }, [])
}
```

```jsx
import { useEffect, useRef, useCallback } from 'react';

/**
 * Component Did Update
 * @param {() => void} effect - Effect Callback
 * @param {Array} deps - 依赖数组
 */
export function useDidUpdate(effect, deps) {
  const isInitialMount = useRef(true);
  
  const setIsInitialMount = useCallback(() => {
    isInitialMount.current = false  
  });

  useEffect(isInitialMount.current ? setIsInitialMount : effect, deps);
}
```

```jsx
import { useState, useCallback } from 'react';

/**
 * 强制更新
 */
export function useForceUpdate() {
    const [, setState] = useState(0);
    const forceUpdate = useCallback(() => setState(x => x + 1), []);
    return forceUpdate;
}
```

```jsx
import { useEffect, useRef } from 'react';

/**
 * 组件挂载前
 * @param {() => void} func - handleWillMount Function
 */
export function useWillMount(effect) {
    const isWillMount = useRef(true);

    if (isWillMount.current && effect) {
      effect();
    }

    useDidMount(() => {
        isWillMount.current = false;
    });
}
```

```jsx
import { useEffect, useRef } from 'react';

/**
 * state与props上次值
 * @param {*} value
 */
export function usePrevious(value){
    const ref = useRef(null);

    useEffect(() => {
      ref.current = value
    });

    return ref.current;
}
```
