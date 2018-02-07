# 什么是HashMap

`HashMap`是一个我们使用非常多的用于存储Key-Value键值对的集合,它是基于哈希表的Map接口的实现。在`HashMap`中，Key-Valuee总是会当做一个整体来处理，根据hash算法来来计算Key-Value的存储位置，我们总是可以通过`Key`快速地存取`Value`

# 为什么会有HashMap

我们使用的数据结构中，有两个最基本的数据结构：`数组`和`链表`。
`数组`