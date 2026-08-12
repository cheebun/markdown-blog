## Java 枚举

```java
public enum ClassroomBehavior {
    START_CLASSROOM(1, "上课"),

    FINISH_CLASSROOM(2, "下课"),

    private Integer value;

    private String description;

    ClassroomBehaviorTypeEnum(Integer value, String description) {
        this.value = value;
        this.description = description;
    }

    public Integer getValue() {
        return value;
    }

    public String getDescription() {
        return description;
    }
}
```

## TypeScript 实现

```Typescript
class ClassroomBehavior {
  public static valueOf(value: number, description: string) {
    return new this(value, description);
  }

  public static START_CLASSROOM = this.valueOf(1, "上课");

  public static FINISH_CLASSROOM = this.valueOf(2, "下课");

  public constructor(private readonly value: number, private readonly description: string) {
    this.value = value;
    this.description = description;
  }

  public getValue() {
    return this.value;
  }

  public getDescription() {
    return this.description;
  }
}
```
