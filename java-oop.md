## 类变量、实例变量、局部变量有什么区别？
- 类变量（class variable），也就是静态变量（static field），即用 `static` 修饰的成员变量，使用类变量不需要创建类的实例就可以使用，即时创建了多个实例也是共享同一个类变量；
- 实例变量（instance variable），非 static 成员变量，必须通过类的实例来使用，每个实例都对应一个实例变量；
- 局部变量（local variable），在方法中创建的变量，只能在当前方法中使用。

JVM 内存位置：
- 类变量保存在方法区（Method Area）
- 实例变量保存在堆（Heap）
- 局部变量保存在虚拟机栈（Java Virtual Machine Stack）

参考：
- https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html
- https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5

## Java 中有哪些方式可以创建一个对象？
- 使用 `new` 创建对象
- 通过反射（Reflection）来创建对象
- 通过反序列化创建对象
- 通过 `Object` 类的 `clone` 方法克隆创建对象

## 重载和重写的区别是什么？
- 重载（overload）：同一个类中可以有多个名称相同的方法，但这些方法的参数列表各不相同（即参数个数或类型不同）；
- 重写（override）：子类中的方法可以与父类中的某个方法的名称和参数完全相同（子类重写父类的方法）。

## 接口和抽象类的区别是什么？
语法上的区别：
- Java 中一个类可以实现多个接口，但无法继承多个父类；
- 在 Java 8 之前，接口只能包含抽象方法和 `static final` 修饰的类变量；
- 在 Java 8 中，接口允许 default 方法和静态方法；
- 在 Java 9 中，接口允许包含 private 修饰的私有方法和私有静态方法；
- 抽象类没有以上这些限制。


设计上的区别：
- 接口设计的目的是制定规范和抽象行为
- 抽象类设计的目的是代码复用
- 接口优于抽象类

## 序列化是什么？你知道哪些序列化的方法？
序列化是什么：

将 Java 对象转化成字节序列的过程

序列化有什么作用：
- 对象存储，例如 Spring Session 将对象保存到 Redis 或数据库中
- 对象传输，例如 Dubbo、gRPC 等 RPC 框架

序列化的方法：
- Java 自带的序列化
- Hessian 序列化
- Protobuf
- JSON 序列化，如 Fastjson、Jackson、Gson 等
