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
- 现在的很多语言已经不能以编译型语言和解释型语言来区分了，因为很多语言都兼具编译型语言和解释型语言的特点。

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
- 当重写 `equals` 方法时，一般也要重写 `hashCode` 方法，两个用 `equals` 比较结果相等的对象的 hashCode 值必须要相等；
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

## String、StringBuffer、StringBuilder 的区别是什么?
- `String` 是不可变的，一旦创建其值就无法改变，它是一个 `final` 类，不可以被继承，内部使用了一个不可变的 `final char value[]` 数组来保存字符串内容；
- `StringBuilder`、`StringBuffer` 都是可变的字符串，都是继承自 `AbstractStringBuilder`，内部包含一个字符数组 `char[] value`，数组由于没有使用 `final` 修饰，所以在长度不够时，可以重新创建一个长度更长的新的数组用于扩容；
- `StringBuffer` 是线程安全的，内部通过 `synchronized` 来实现线程安全，`StringBuilder` 是非线程安全的；

使用场景：
- 在需要大量字符串拼接的场景下，使用 `StringBuilder`、`StringBuffer` 的 `append` 性能会优于直接用 `String` 和 `+` 运算符来拼接字符串，因为 `String` 是不可变的，只能通过大量创建新的 `String` 实例来实现大量的字符串拼接；
- 在无需考虑线程安全的情况下，`StringBuilder` 性能会优于 `StringBuffer`，因为 `StringBuffer` 内部需要通过 `synchronized`  来保证线程安全。

## 以下代码的运行结果是什么？为什么？
```java
ArrayList<Integer> l1 = new ArrayList<>();
ArrayList<String> l2 = new ArrayList<>();
System.out.println(l1.getClass() == l2.getClass());
```

运行结果：true

Java 通过类型擦除（type erasure）的方式来实现泛型。Java 语言中引入泛型是为了在编译时提供更严格的类型检查，在编译完成后的 .class 文件中以及运行时并不包含泛型信息。

在以上程序中，由于类型擦除的原因，两个 `ArrayList` 对象对应的类型是同一个 `ArrayList.class`，

- https://docs.oracle.com/javase/tutorial/java/generics/erasure.html

## Java 中 final、finally、finalize 分别是什么意思？
- final 用来修饰类、变量、方法
    - final 修饰类，表示这个类不可以被继承
    - final 修饰变量，表示这个变量不能被修改
    - final 修饰方法，表示这个方法不能被重写
- finally 用于异常处理中，表示一段代码最终一定会被执行，不管有没有抛出异常，经常被用在需要释放资源的情况下；
- finalize 是 Object 类的一个方法，会在一个对象被垃圾回收之前调用

## Integer.MAX_VALUE + 1 的结果是的？为什么？
Java 使用补码（two's complement）来表示有符号的数值。

Integer.MAX_VALUE 对应的二进制补码是：01111111 11111111 11111111 11111111，其中最左边一位 0 是符号位，表示正数；

在此基础上加1的结果是：10000000 00000000 00000000 00000000，得到的结果符号位变成了 1，表示负数，该结果是 Integer.MIN_VALUE 的二进制补码值。
