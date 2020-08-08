## Java 是编译型语言还是解释型语言？
什么是编译型语言和解释型语言：
- 编译型语言（compiled language）指通过编译器（compiler）将源代码编译为机器码（machine code）后运行的语言，例如C、C++；
- 解释型语言（interpreted language）指由解释器（interpreter）直接执行，不需要编译成机器语言，例如 PHP、JavaScript。

编译型语言和解释型语言的优点和缺点：
- 由于解释型语言会在运行时翻译源代码，一般情况下运行速度不如编译型语言；
- 解释型语言由解释器运行，而不是直接运行在操作系统上，所以一般有较强的跨平台能力。

Java 是编译型语言还是解释型语言：
- 为了兼顾跨平台和运行速度，Java 源代码首先会被编译为字节码文件（.class），但并非是机器语言，而是需要在 JVM 上运行，而 .class 文件在 JVM 上是解释执行的。所以 Java 兼具编译型语言和解释型语言的特点。
- 为了更高的效率，JVM 还引入了 JIT（just-in-time，即时编译）编译器，在 Java 程序运行时进一步编译，转换成高度优化的机器代码。
- 现在的很多语言以及不能以编译型语言和解释型语言来区分了，因为很多语言都兼具编译型语言和解释型语言的特点。

参考：
- https://en.wikipedia.org/wiki/Compiled_language
- https://en.wikipedia.org/wiki/Interpreted_language
- https://www.oracle.com/technical-resources/articles/java/architect-evans-pt1.html


## == 和 equals 的区别？
在 Java 中有两种类型：原始类型（primitive type）和引用类型（reference type）：
- 原始类型（primitive type）：包括 byte、short、int、long、char、float、double、boolean
- 引用类型（reference type）：对象、数组等

== 和 equals 的区别：
- ==：对于原始类型，用于判断两个值是否相等；对于引用类型，判断两个对象是否引用是一致的，即是否是同一个对象；
- equals：`equals` 是 `Object` 类中方法，用于判断两个对象是否相等，默认也是使用 == 来判断是否相等；
- `equals` 不能用于比较原始类型；
- `equals` 方法可以被重写，但是 Java 语言没办法重写运算符；
- 在比较 `String` 类型以及原始类型的包装类型（wrapper class）例如 `Integer`、`Long` 等，需要使用 `equals` 来比较，而不能使用 == 。

参考：
- https://docs.oracle.com/javase/specs/jls/se8/html/jls-4.html

## 重写 equals 方法和 hashCode 方法有什么规则？
- 当重写 `equals` 方法时，一般也要重写 `hashCode` 方法
- 两个用 `equals` 比较结果相等的对象的 hashCode 值必须要相等；
- 两个用 `equals` 比较结果不相等的对象，并不强制要求 hashCode 值必须不相等，也就是两个 hashCode 相等的对象不一定通过 `equals` 比较是相等的；
- 为了提高使用到 `hashCode` 方法的一些数据结构（例如 HashMap）的性能，应该尽量避免哈希冲突（即用 `equals` 比较不相等的两个对象 hashCode 一致）；
- 一些用到 `hashCode` 方法的数据结构（例如 HashMap），会先用 `hashCode` 方法缩小查找范围，再用 `equals` 方法对比是否相等。如果重写两个方法时出现 `equals` 比较相等的对象 hashCode 不一致，那么在 HashMap 查找时，可能会因此查找失败。

参考：
- https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html

## 以下代码的运行结果是什么？为什么？
```java
Integer i = 100;
Integer j = 100;
System.out.println(i == j);

Integer x = 1000;
Integer y = 1000;
System.out.println(x == y);
```

运行结果：true false

- `Integer i = 100` 是自动装箱（autoboxing）的语法，实际上相当于 `Integer i = Integer.valueOf(100)`；
- 通过 `Integer.valueOf(int i)` 方法的源码和文档可以发现，当数值范围在 -128 到 127 时，`Integer.valueOf(int i)` 方法会通过缓存获取到对应的 Integer 对象，不在这个范围则会通过 `new Integer(int value)` 创建新对象：
    ```java
    public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
    ```
    其中 `IntegerCache.low` 和 `IntegerCache.high` 的默认值分别是 -128 和 127；
- == 比较的是两个对象是否引用一致，即是否是同一个对象，所以会出现以上的结果；
- 最后要注意的是，Integer 对象不应该用 == 来比较，而应该用 `equals` 来比较。

参考：
- https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html
- https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html
