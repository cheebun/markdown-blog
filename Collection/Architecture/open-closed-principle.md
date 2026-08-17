# 开闭原则

> `「开闭原则」`英文 `Open-Closed Principle`，缩写 `OCP`。

「开闭原则」是七大设计原则之一，主要内容为：

1. 一个软件实体（模块、类、方法等）应该对扩展开放，对修改关闭。

## 代码示例

陀螺是个程序喵，创办了一个生产猫粮的公司——跑码场，手下有个小徒弟叫招财，写了一个下单的逻辑。

```typescript
const Flavor = {
  MAO_XUE_WANG: "mao_xue_wang",
  FISH: "fish",
} as const;

type Flavor = (typeof Flavor)[keyof typeof Flavor];

/**
 * 跑码场
 */
class PaoMaChang {
  public order(flavor: Flavor): void {
    if (flavor === Flavor.MAO_XUE_WANG) {
      console.log("售卖「毛血旺」风味猫粮");
    } else {
      console.log("售卖「鱼香肉丝」风味猫粮");
    }
  }
}
```

逻辑本身很简单，核心业务逻辑主要是 `order()` 函数，客户需要传入相应的猫粮口味 `flavor` 进行下单。

跑码场扩展了业务，新增「大肠刺身」口味，且支持用户自定义购买数量。招财对代码做了如下修改：

```typescript
const Flavor = {
  MAO_XUE_WANG: "mao_xue_wang",
  FISH: "fish",
  DACHANG: "dachang",
} as const;

type Flavor = (typeof Flavor)[keyof typeof Flavor];

/**
 * 跑码场
 */
class PaoMaChang {
  public order(flavor: Flavor, count: number = 1): void {
    if (flavor === Flavor.MAO_XUE_WANG) {
      console.log(`售卖${count}袋「毛血旺」风味猫粮`);
    } else if (flavor === Flavor.FISH) {
      console.log(`售卖${count}袋「鱼香肉丝」风味猫粮`);
    } else {
      console.log(`售卖${count}袋「大肠刺身」风味猫粮`);
    }
  }
}
```

这直接修改了已有方法的内部逻辑。每加一种口味都要改一次 `order()`，违背了开闭原则，也容易在改动过程中引入回归缺陷。

## 重构

引入抽象，将每种猫粮产品封装为独立的类：

```typescript
/**
 * 抽象的猫粮
 */
abstract class CatFood {
  public abstract order(): void;
}

/**
 * 「毛血旺」风味猫粮
 */
class MaoXueWangCatFood extends CatFood {
  public order(): void {
    console.log("售卖「毛血旺」风味猫粮");
  }
}

/**
 * 「鱼香肉丝」风味猫粮
 */
class FishCatFood extends CatFood {
  public order(): void {
    console.log("售卖「鱼香肉丝」风味猫粮");
  }
}

/**
 * 跑码场 V2
 */
class PaoMaChangV2 {
  public order(food: CatFood): void {
    food.order();
  }
}
```

重构后，`PaoMaChangV2.order()` 不再感知具体口味，它只依赖抽象 `CatFood`。

## 基于重构实现新需求

主要改动有两点：1) `CatFood` 基类添加属性 `count` 并提供构造函数；2) 添加新类 `DaChangCatFood`。

```typescript
/**
 * 抽象的猫粮
 */
abstract class CatFood {
  public constructor(protected count: number = 1) {}

  public abstract order(): void;
}

/**
 * 「毛血旺」风味猫粮
 */
class MaoXueWangCatFood extends CatFood {
  public order(): void {
    console.log(`售卖${this.count}袋「毛血旺」风味猫粮`);
  }
}

/**
 * 「鱼香肉丝」风味猫粮
 */
class FishCatFood extends CatFood {
  public order(): void {
    console.log(`售卖${this.count}袋「鱼香肉丝」风味猫粮`);
  }
}

/**
 * 「大肠刺身」风味猫粮
 */
class DaChangCatFood extends CatFood {
  public order(): void {
    console.log(`售卖${this.count}袋「大肠刺身」风味猫粮`);
  }
}
```

客户端代码：

```typescript
const paoMaChang = new PaoMaChangV2();

// 创建对应口味的猫粮
const dachang = new DaChangCatFood(2);
paoMaChang.order(dachang);
```

如果有了新口味的猫粮产品，只需新增一个类并实现 `order()` 方法，不需要改动其他任何代码；如果 `order` 需要其他参数，可以根据实际情况在 `CatFood` 中添加相关属性。

## 是不是修改代码就违背开闭原则？

细心的读者可能会发现，我们在重构时向 `CatFood` 基类添加了 `count` 属性和构造函数，这算不算"修改"？

添加新功能时不可能一点代码都不修改。开闭原则作用于不同粒度的软件实体：对 `count` 属性的添加，在模块或类的粒度下可以被认为是修改，但在方法的粒度下，我们并没有修改任何已有的方法，因此可以被认为是扩展。理解开闭原则，需要结合具体的粒度来判断，而不是机械地套用"改了就违背"。

下一篇可以结合[「依赖倒置」](./dependency-inversion.md)原则一起理解。
