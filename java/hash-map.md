# 简介

`HashMap`是一个我们使用非常多的用于存储Key-Value键值对的集合，根据hash算法来计算Key-Value的存储位置，我们总是可以通过`Key`快速地存取`Value`。

`HashMap`将两者结合在一起，发挥各自的优点，使得`HashMap`不仅可以快速查询结构中的元素，也可以快速对结构中的元素进行增加或者删除。

`HashMap`提供所有有关`Map`的操作，大致上相当于`Hashtable`，但是它并非线程安全，且允许使用`null`键和`null`值。`HashMap`不保证元素在集合中的顺序，即它是无序的，随着时间的不断推移，它并不保证元素仍然保持着插入时的顺序。

我们使用的数据结构中，有两个最基本的数据结构：`数组`和`链表`，它们的特点刚好相反：
* `数组`增加删除元素慢，查询元素快
* `链表`增加删除元素快，查询元素慢

# 数据结构

如下图：

![Image](https://chronosc.github.io/images/java-hash-map.png)

`HashMap`中定义了一个数组`table`，即为上图0-N的数据结构，数据类型为上图中的`NODE`
```
    /**
     * The table, initialized on first use, and resized as
     * necessary. When allocated, length is always a power of two.
     * (We also tolerate length zero in some operations to allow
     * bootstrapping mechanics that are currently not needed.)
     */
    transient Node<K,V>[] table;
```

