# 基本类型

## 布尔值
```javascript
let isDone: boolean = false;
let name: string = "name";
```

&nbsp;

## 数字
```javascript
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```

&nbsp;

## 字符串
```javascript
let name: string = "microld";
let name: string = 'microld';
let name: string = `microld`;
```

### 字符串模板
```javascript
let name: string = 'microld';
let age: number = 29;
let sentence: string = `你好, 我叫${ name }.

我差1个月，就${ age + 1 }岁了。`
```

&nbsp;

## 数组
`元素类型[]`
`Array<元素类型>`

### 数字数组
```javascript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

### 字符串数组
```javascript
let list: string[] = ["a", "b", "c"];
let list: Array<string> = ["a", "b", "c"];
```

### 混合数组
```javascript
let list: (number|string)[] = [1, 2, "a"];
let list: Array<number|string> = [1, 2, "a"];
```

### 任意值数组
```javascript
let list: Array<any> = [1, "a", true];
```

&nbsp;

## 元组 Tuple
```javascript
let x: [number, string] = [10, 'hello'];  // OK
x = ['hello', 10]; // Error
```

### 获取类型
```javascript
console.log(x[0].substr(1)); // Error, 'number' does not have 'substr'
console.log(x[1].substr(1)); // OK
```

### 跨界
```javascript
x[3] = 'world'; // OK

console.log(x[3],toString());

x[4] = true; // Error, 布尔不是(string | number)类型
```

&nbsp;

## 枚举
```javascript
enum Color { Red, Green, Blue }
let c: Color = Color.Green; // 1
```

### 手动赋值
```javascript
enum Color { Red = 1, Green = 2, Blue = 9 };
let c: Color = Color.Green; // 2

enum Color {
  Red = "#F00",
  Green = "#0F0",
  Blue = "#00F"
}

let c: Color = Color.Green; // #0F0
```

### 获取枚举名(限枚举值为数字的枚举)
```javascript
enum Color { Red = 1, Green, Blue };
let colorName: string = Color[2];
```

&nbsp;

## 任意值
```javascript
let notSure: any = 4;
notSure = "string";
notSure = false;
```

### 任意值的数组
```javascript
let list: any[] = [1, true, "free"];

list[1] = 100;
```

&nbsp;


## 空值
```javascript
function warnUser(): void {
  alert("This is my warning message");
}
```

### 赋值
```javascript
let unusable: void = undefined;
```

&nbsp;

## Null 和 Undefined

```javascript
let u: undefined = undefined;
let n: null = null;
```

&nbsp;

## Never
永不存在的值的类型
```javascript
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message);
}

// 推断的返回值为never
function fail() {
  return error("Something failed");
}

function infiniteLoop(): never {
  while (true) {
    // ...
  }
}
```
