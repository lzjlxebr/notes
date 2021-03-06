# JVM

## JVM Data Types

### Primitive types
- 数字类型byte(8-bit), char(16-bit unsigned Unicode), short(16-bit), int(32-bit), long(64-bit), float(32-bit IEEE 754 single precision FP), double(64-bit IEEE 754 double precision FP)
- boolean
- returnAddress, 指令的地址指针
### Reference types
- Class types
- Array types
- Interface types

boolean类型在JVM中会被转换成int使用。

## Run-Time Data Areas

### The pc Register
JVM是支持同时运行多个线程的。每个JVM线程都有其自己的程序计数注册器。在任意时间点上，JVM线程都在执行单个方法的代码，也就是该线程的当前方法。如果被执行的方法不是一个本地方法，那么程序计数注册器会包含一个正在被执行的JVM指令的地址。如果不是，它的值为未定义。程序计数注册器有足够的宽度来持有```returnAddress```或者在指定平台上的一个本地方的指针。

### JVM Stacks
每个JVM线程都有一个*私有的*与其同时创建的*JVM栈*，一个JVM栈存放着一系列栈帧。JVM栈与常规的语言是类似的比如说C：JVM栈持有局部变量和一部分返回值，并且在方法调用和返回上起了一定作用。因为JVM栈不会被直接操作，除了推入栈帧和弹出栈帧，栈帧可能被堆分配。JVM栈的内存是彼此分开的，不必是相互毗邻的。

> *在Java虚拟机规范的第一版中，Java虚拟机堆栈称为Java堆栈。*

规范中允许JVM栈的大小是能够固定或者是被约定好的或者是程序计算时需要的动态分配的。如果JVM堆大小是固定的，那么每个栈被创建时会被独立的分配大小。

> *Java虚拟机实现可以为程序员或用户提供对Java虚拟机堆栈初始大小的控制，并且在动态扩展或收缩Java虚拟机堆栈的情况下，可以控制最大和最小大小。*

下面两个异常是和JVM栈相关联的：
- ```StackOverflowError```：如果一个线程的运算过程中需要的内存超过了JVM栈允许的大小，就会报着个错。
- ```OutOfMemoryError```：如果JVM栈能被动态扩展，当试图扩展时，但是由于没有足够的内存可用于扩展，或者如果在初始化JVM栈的某一线程时内存不足，JVM就会抛出这个异常。


### Heap
JVM中的被所有线程共享的内存区域叫做*堆*。堆内存存放运行时数据区域中的所有类实例和数组。

堆在JVM启动时被创建。自动存储管理系统（称为垃圾收集器）可以回收对象的堆存储； 对象永远不会显式释放。Java虚拟机不假定特定类型的自动存储管理系统，可以根据实现者的系统要求选择存储管理技术。堆的大小可以是固定的，也可以根据计算的需要进行扩展，如果不需要更大的堆，则可以将其收缩。 堆的内存不必是连续的。

> *Java虚拟机实现可以为程序员或用户提供对堆初始大小的控制，并且，如果可以动态扩展或收缩堆，则可以控制最大和最小堆大小。*

下面的异常是和JVM堆相关联的：
- ```OutOfMemoryError```：如果计算需要的堆多于自动存储管理系统可以提供的堆，则Java虚拟机将引发该异常。

### Method Area

Java虚拟机具有一个在所有Java虚拟机线程之间共享的方法区域。 该方法区域类似于常规语言的编译代码的存储区域，或者类似于操作系统过程中的“文本”段。 它存储每个类的结构，例如运行时常量池，字段和方法数据，以及方法和构造函数的代码，包括用于类和实例初始化以及接口初始化的特殊方法。

方法区域是在虚拟机启动时创建的。 尽管方法区域在逻辑上是堆的一部分，但是简单的实现可以选择不进行垃圾回收或压缩。 该规范没有规定方法区域的位置或用于管理已编译代码的策略。 方法区域可以是固定大小的，或者可以根据计算的需要进行扩展，如果不需要更大的方法区域，则可以缩小。 方法区域的内存不必是连续的。

> *Java虚拟机实现可以为程序员或用户提供对方法区域初始大小的控制，并且在方法区域大小可变的情况下，可以控制最大和最小方法区域大小。*

下面的异常是和方法区相关联的：
- ```OutOfMemoryError```：如果无法使方法区域中的内存可用以满足分配请求，则Java虚拟机将引发该异常。

### Run-Time Constant Pool

### Frames

1. Local Variables
2. Operand Stacks
3. Dynamic Linking
4. Normal Method Invocation Complete
5. Abrupt Method Invocation Complete

[Java SE Specifications - Chapter 2. The Structure of the Java Virtual Machine](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-2.html#jvms-2.5.5)
