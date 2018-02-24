# JAVA内存模型 - `JAVA MEMORY MODEL`

![Image](https://chronosc.github.io/images/java-memory-model.png)


## 堆(Heap Space)

所有new出来的对象内存都分配在堆中，堆被分成年轻代`YongGeneration`和老年代`OldGeneration`,新生代又分成`Eden`和两个`Survivor`区。

### MinorGC

年轻代是所有新对象产生的地方。
当年轻代内存空间被用完时，就会触发垃圾回收。这个垃圾回收叫做`MinorGC`。
年轻代被分为3个部分——`Enden`区和两个`Survivor`区`From`区和`To`区。

新对象在年轻代产生，当年轻代空间占满后，会触发`MinorGC`开始垃圾回收，大多数新建对象位于`Eden`区，`Eden`区满后触发一次`MinorGC`，存活下来的对象转到`From`区，`From`区满后触发执行`MinorGC`，然后`From`区和`To`区角色对换，这样保证一段时间内总有一个`Survivor`区为空。经过多次`MinorGC`仍然存活的对象会转入老年代，这是由设定的年龄阈值来决定的。

### MajorGC

老年代空间存储长期存活的对象，老年代占满时会触发`MajorGC`，花费时间较长，由于垃圾回收会导致`StopTheWorld`事件，即所有线程都会停下来等待垃圾回收执行完成，所以对响应要求高的应用应尽量减少发生`MajorGC`。

在分代收集算法中，由于年轻代中对象的存活率低，通常使用复制算法进行垃圾回收，老年代一般使用”标记-清理”或”标记-整理”算法回收存活率较高的对象。

## 永久代(Permanent Generation / Metaspace)

用来保存程序运行时长期存活的对象，如类的元数据、全局静态变量等。
但是Java8中已经用`Metaspace`完全替代了永久代。
jvm参数-XX:PermSize和-XX:MaxPermSize选项会被忽略。

## 本地区(Native Area)

### 程序计数器

程序计数器用来为线程独立拥有，线程间互不影响，保证线程切换后能准确恢复到执行位置，线程执行指令的跳转、循环、分支都要依赖计数器来完成。

### 本地方法栈

Java栈也是线程独立的，每个线程建立一个Java栈存储数据，所以不需要关心其数据一致性，也不会存在同步锁的问题。每个Java栈存在多个栈帧`StackFrame`,栈帧与方法一一对应，在HotSpot虚拟机中，使用-Xss参数来设置栈的大小，栈的大小直接决定了函数调用的可达深度。

