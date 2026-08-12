# 使用 window.crypto.getRandomValues 取代不安全的 Math.random

最近在使用 `TSLint` 规范代码的时候, 使用了微软的规则, 它提示 `Math.random` 不安全的伪随机数字。

建议使用 `crypto.randomBytes()` 或 `window.crypto.getRandomValues()` 代替。

下面我们来看一下, `window.crypto.getRandomValues()` 的实现。

```javascript
/**
 * 随机生成一个 0 到 1 之间的浮点数
 *
 * @returns 返回一个随机数
 */
function getRandom(): number {
  const randomBuffer: Uint32Array = new Uint32Array(1);
  window.crypto.getRandomValues(randomBuffer);

  return randomBuffer[0] / (0xFFFFFFFF + 1);
}

/**
 * 生成一个随机整形数
 *
 * @param max 最大值
 * @param min 最小值
 * @returns 返回一个随机整形数
 */
function getRandomIntInclusive(max: number = 10, min: number = 0): number {
  const minValue: number = Math.ceil(min);
  const maxValue: number = Math.floor(max);

  return Math.floor(getRandom() * (maxValue - minValue + 1)) + minValue;
}
```

## 参考

[Javascript: Generate a random number within a range using crypto.getRandomValues](https://stackoverflow.com/questions/18230217/javascript-generate-a-random-number-within-a-range-using-crypto-getrandomvalues)
