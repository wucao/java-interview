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

## 重载（overload）和重写（override）的区别是什么？
- 重载（overload）：同一个类中可以有多个名称相同的方法，但这些方法的参数列表各不相同（即参数个数或类型不同）；
- 重写（override）：子类中的方法可以与父类中的某个方法的名称和参数完全相同（子类重写父类的方法）。

## 接口和抽象类的区别是什么？

## 你知道哪些对象序列化的方法？

## 
