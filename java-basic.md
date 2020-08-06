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

