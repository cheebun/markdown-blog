# 依赖倒置

> `「依赖倒置」`原则的英文翻译是 `Dependency Inversion Principle`，缩写为 `DIP`。中文翻译有时候也叫`「依赖反转」`原则。

「依赖倒置」是七大设计原则之二，在生产实际中应用的非常广泛，主要内容为:

1. 高层模块(high-level modules)不要直接依赖低层模块(low-level)；
2. 高层模块和低层模块应该通过抽象(abstractions)来互相依赖；
3. 抽象(abstractions)不要依赖具体实现细节(details)，具体实现细节(details)依赖抽象(abstractions)。

## 代码示例

陀螺研发了一套自动驾驶系统，在积极谈判之下和本田以及福特达成了合作协议，两个厂商各自提供汽车启动、转弯和停止的api供自动驾驶调用，系统就能实现自动驾驶。

代码如下

```typescript
/**
 * @author microld
 * @desc 福特汽车厂商提供的接口
 */
class FordCar {
  public run(): void {
    console.log("福特开始启动了");
  }

  public turn(): void {
    console.log("福特开始转弯了");
  }

  public stop(): void {
    console.log("福特开始停车了");
  }
}

/**
 * @author microld
 * @desc 本田汽车厂商提供的接口
 */
class HondaCar {
    public run(): void {
      console.log("本田开始启动了");
    }

    public turn(): void {
      console.log("本田开始转弯了");
    }

    public stop(): void {
      console.log("本田开始停车了");
    }
}

enum CarType {
  Ford, 
  Honda
}

/**
 * @author microld
 * @desc 自动驾驶系统
 */
class AutoDriver {    
  private hondaCar: HondaCar = new HondaCar();

  private fordCar: FordCar = new FordCar();

  public constructor(private type: CarType) {}

  public runCar(): void {
    if (this.type == CarType.Ford) {
      this.fordCar.run();
    } else {
      this.hondaCar.run();
    }
  }

  public turnCar(): void {
    if (this.type == CarType.Ford) {
      this.fordCar.turn();
    } else {
      this.hondaCar.turn();
    }
  }

  public stopCar(): void {
    if (this.type == CarType.Ford) {
      this.fordCar.stop();
    } else {
      this.hondaCar.stop();
    }
  }
}
```

自动驾驶系统运转良好，很快，奥迪和奔驰以及宝马纷纷找到陀螺寻求合作，陀螺不得不把代码改成这个样子。

```typescript
enum CarType {
  Ford, 
  Honda,
  Audi, 
  Benz, 
  Bmw
}

/**
 * @author microld
 * @desc 自动驾驶系统
 */
class AutoDriver {    
  private hondaCar: HondaCar = new HondaCar();

  private fordCar: FordCar = new FordCar();

  private audiCar: AudiCar = new AudiCar();
  
  private benzCar: BenzCar = new BenzCar();
  
  private bmwCar: BmwCar = new BmwCar();

  public constructor(private type: CarType) {}

  public runCar(): void {
    if (this.type === CarType.Ford) {
      this.fordCar.run();
    } else if (this.type === CarType.Honda) {
      this.hondaCar.run();
    } else if (this.type === CarType.Audi) {
      this.audiCar.run();
    } else if (this.type === CarType.Benz) {
      this.benzCar.run();
    } else {
      this.bmwCar.run();
    }
  }

  public turnCar(): void {
    if (this.type === CarType.Ford) {
      this.fordCar.turn();
    } else if (this.type === CarType.Honda) {
      this.hondaCar.turn();
    } else if (this.type === CarType.Audi) {
      this.audiCar.turn();
    } else if (this.type === CarType.Benz) {
      this.benzCar.turn();
    } else {
      this.bmwCar.turn();
    }
  }

  public stopCar(): void {
    if (this.type === CarType.Ford) {
      this.fordCar.stop();
    } else if (this.type === CarType.Honda) {
      this.hondaCar.stop();
    } else if (this.type === CarType.Audi) {
      this.audiCar.stop();
    } else if (this.type === CarType.Benz) {
      this.benzCar.stop();
    } else {
      this.bmwCar.stop();
    }
  }
}
```