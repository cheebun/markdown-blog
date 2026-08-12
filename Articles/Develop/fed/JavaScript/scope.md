
# 作用域（scope）

执行上下文(execution context)
AO: Activation Object
GO: Global Object

## 作用域

其实每个JavaScript函数都是一个对象，对象中有些属性我们可以访问，但是有的不可以，这些属性仅供JavaScript引擎存取，[[scope]]就是其中一个。

[[scope]]指的就是我们所说的作用域，其中存储的就是执行期上下文的集合。

## 作用域链

[[scope]]所存储的执行期上下文对象的集合，这个集合呈链式链接，我们把这种链式链接叫做作用域链。

## 执行期上下文

当函数执行时，会创建一个称为执行期上下文的内部对象。一个执行期上下文定义了一个函数执行时的环境，函数每次执行时对应的执行上下文都是独一无二的，所以，多次调用一个函数会导致创建多个执行上下文，当函数执行完毕，它所产生的执行上下文被销毁。

```javascript
// func被定义时
// 产生作用域(定义期)
// 它所在环境的执行期上下文
// func.[[scope]] -> scope chain -> 0: GO
function func() {
  // func执行时, 产生执行期上下文
  // func.[[scope]] -> scope chain -> 0: func AO
  // func.[[scope]] -> scope chain -> 1: GO

  // func执行时
  // 触发funA定义期, 产生作用域
  // 它所在环境的执行期的上下文
  // func环境内部, 它也就有func的执行期上下文。
  // funcA.[[scope]] -> scope chain -> 0: AO func AO
  // funcA.[[scope]] -> scope chain -> 1: GO
  function() funcA {
    // funcA执行时, 产生执行期上下文
    // funcA.[[scope]] -> scope chian -> 0: funcA AO
    // funcA.[[scope]] -> scope chain -> 0: func AO
    // funcA.[[scope]] -> scope chain -> 1: GO
  }


  funcA(); // funcA执行时, 产生 funcA AO
  // funcA执行完毕,销毁 funcA AO

}

func(); // func执行时, 产生 func AO
// func执行完毕, 销毁 func AO


func(); // func再次执行时, 重新产生 func AO
// func执行完毕, 销毁 func AO
```


## 查找变量

从作用域链的顶端依次向下查找。

## 闭包

```javascript
// func被定义时
// 产生作用域(定义期)
// 它所在环境的执行期上下文
// func.[[scope]] -> scope chain -> 0: GO
function func() {

  // func执行时, 产生执行期上下文
  // func.[[scope]] -> scope chain -> 0: func AO
  // func.[[scope]] -> scope chain -> 1: GO


  let num = 1;

  // func执行时
  // 触发funA定义期, 产生作用域
  // 它所在环境的执行期的上下文
  // func环境内部, 它也就有func的执行期上下文。
  // funcA.[[scope]] -> scope chain -> 0: AO func AO
  // funcA.[[scope]] -> scope chain -> 1: GO
  function funcA() {
    // funcA执行时, 产生执行期上下文
    // funcA.[[scope]] -> scope chian -> 0: funcA AO
    // funcA.[[scope]] -> scope chain -> 0: func AO
    // funcA.[[scope]] -> scope chain -> 1: GO

    return num;
  }

  return funcA;
}

let demo = func();  // func 执行时, 产生 func AO
                    // func 产生的结果,
                    // funcA 返回给 demo
                    // 同时也返回 func AO 给demo

// func 执行完毕, 销毁 func 自身 AO
// 但是 demo 还保存着, func 产生的结果, 包含 func 产生的 AO

// 闭包
demo(); // 1;
        // 执行的是 demo 下 funcA
        // funcA 里的执行期的上下文, 是 func 返回给 demo 的
        // 所以, demo 里的执行期上下文, 还是 func 的执行期上下文
```
