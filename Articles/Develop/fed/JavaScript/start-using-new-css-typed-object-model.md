# 开始使用新的 CSS Typed Object Model

```javascript
const element = document.getElementById("app");
```

## CSS OM

全称 CSS Object Model (CSSOM)

```javascript
// Element styles
element.style.opacity = 0.3;

// Stylesheet rules
document.style.styleSheets[0].cssRules[0].style.opacity = 0.3;

```

&nbsp;

## CSS Typed OM
全称 CSS Typed Objcet Model

### 规范与草案
> [W3C CSS Typed OM Level 1](https://www.w3.org/TR/css-typed-om-1/)    
> [CSS Typed OM Level 2](https://drafts.css-houdini.org/css-typed-om-2/)



### 浏览器支持和功能检测
```javascript
if (window.CSS && CSS.number) {
    console.log("Supports CSS Typed OM")  
}
```

### API 基础

#### 访问样式
```javascript
/**
 * Element styles
 */
// .attributeStyleMap.set
element.attributeStyleMap.set('opacity', 0.3);
element.attributeStyleMap.set('opacity', '0.3');
element.attributeStyleMap.set('opacity', CSS.number(0.3));
element.attributeStyleMap.set('margin-top', CSS.px(10));
el.attributeStyleMap.set('display', new CSSKeywordValue('initial'));

// .attributeStyleMap.get
element.attributeStyleMap.get('margin-top').value; // 10
element.attributeStyleMap.get('margin-top').unit;  // px

// .attributeStyleMap.has
element.attributeStyleMap.has('opacity') // true

// .attributeStyleMap.delete
element.attributeStyleMap.delete('margin-top'); // remove margin-top.

// .attributeStyleMap.clear()
element.attributeStyleMap.clear(); // remove all styles

// 遍历
for (const [prop, val.value, val.unit] of el.attributeStyleMap) {
    console.log(prop, val.value, val.unit);
}


/**
 * Stylesheet rules
 */
document.styleSheets[0].cssRules[0].styleMap.set('background', 'blue');
```

#### 计算样式
##### 计算
```javascript
element.attributeStyleMap.set('opacity', 0.5);
element.computedStyleMap().get('opacity').value // 0.5
```

##### 数值范围限制
```javascript
element.computedStyleMap().get('opacity').value === 1 // computed style clamps value.

```

##### 舍入
```javascript
element.attributeStyleMap.set('z-index', CSS.number(15.4));
element.attributeStyleMap.get('z-index').value  === 15.4 // val not rounded.
element.computedStyleMap().get('z-index').value === 15   // computed style is rounded.
```

### CSS数值
#### 单位值
```javascript
const {value, unit} = CSS.number('10');
// value === 10, unit === 'number'

const {value, unit} = CSS.px(42);
// value === 42, unit === 'px'

const {value, unit} = CSS.vw('100');
// value === 100, unit === 'vw'

const {value, unit} = CSS.percent('10');
// value === 10, unit === 'percent'

const {value, unit} = CSS.deg(45);
// value === 45, unit === 'deg'

const {value, unit} = CSS.ms(300);
// value === 300, unit === 'ms'
```

#### 数学值
##### 基础运算
```javascript
new CSSMathSum(CSS.vw(100), CSS.px(-10)).toString(); // "calc(100vw + -10px)"

new CSSMathNegate(CSS.px(42)).toString() // "calc(-42px)"

new CSSMathInvert(CSS.s(10)).toString() // "calc(1 / 10s)"

new CSSMathProduct(CSS.deg(90), CSS.number(Math.PI/180)).toString();
// "calc(90deg * 0.0174533)"

new CSSMathMin(CSS.percent(80), CSS.px(12)).toString(); // "min(80%, 12px)"

new CSSMathMax(CSS.percent(80), CSS.px(12)).toString(); // "max(80%, 12px)"
```

##### 嵌套表达式
```javascript
// calc(1px - 2 * 3em) 将被构造为：
new CSSMathSum(
  CSS.px(1),
  new CSSMathNegate(
    new CSSMathProduct(2, CSS.em(3))
  )
);


// calc(1px + 2px + 3px) 将被构造为：
new CSSMathSum(CSS.px(1), CSS.px(2), CSS.px(3));


// calc(calc(1px + 2px) + 3px) 将被构造为：
new CSSMathSum(
  new CSSMathSum(CSS.px(1), CSS.px(2)),
  CSS.px(3)
);
```


### 算术运算


#### 基本操作
```javascript
CSS.deg(45).mul(2) // {value: 90, unit: "deg"}

CSS.percent(50).max(CSS.vw(50)).toString() // "max(50%, 50vw)"

// Can Pass CSSUnitValue:
CSS.px(1).add(CSS.px(2)) // {value: 3, unit: "px"}

// multiple values:
CSS.s(1).sub(CSS.ms(200), CSS.ms(300)).toString() // "calc(1s + -200ms + -300ms)"

// or pass a `CSSMathSum`:
const sum = new CSSMathSum(CSS.percent(100), CSS.px(20)));
CSS.vw(100).add(sum).toString() // "calc(100vw + (100% + 20px))"
```

#### 转变
```javascript
// Convert px to other absolute/physical lengths.
el.attributeStyleMap.set('width', '500px');
const width = el.attributeStyleMap.get('width');
width.to('mm'); // CSSUnitValue {value: 132.29166666666669, unit: "mm"}
width.to('cm'); // CSSUnitValue {value: 13.229166666666668, unit: "cm"}
width.to('in'); // CSSUnitValue {value: 5.208333333333333, unit: "in"}

CSS.deg(200).to('rad').value // "3.49066rad"
CSS.s(2).to('ms').value // 2000
```

#### 等值判断
```javascript
const width = CSS.px(200);
CSS.px(200).equals(width) // true

const rads = CSS.deg(180).to('rad');
CSS.deg(180).equals(rads.to('deg')) // true
```








## 参考

[开始使用新的 CSS Typed Object Model](https://segmentfault.com/a/1190000014037586)

[CSS 魔術師 Houdini API 介紹](https://blog.techbridge.cc/2017/05/23/css-houdini/)

[Houdini：CSS 领域最令人振奋的革新](http://top.css88.com/archives/854)

[和 Houdini, CSS Paint API 打个招呼吧](https://zhuanlan.zhihu.com/p/35410151)
