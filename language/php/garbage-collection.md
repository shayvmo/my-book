## 垃圾回收机制



**PHP 的垃圾回收机制是怎么样的？**

- PHP7 垃圾回收机制：定期遍历和标记若干存储对象的数组，再通过算法把将是垃圾的物理空间回收。
- PHP 可以自动进行内存管理，清除不需要的对象。 

- 使用了引用计数 (reference counting) GC 机制。

循环引用问题：垃圾收集器会将其收集到缓冲区，同时加入到 root 环。

每个对象都内含一个引用计数器 refcount，每个 reference 连接到对象，计数器加 1。当 reference 离开生存空间或被设为 NULL，计数器减 1。当某个对象的引用计数器为零时，PHP 知道你将不再需要使用这个对象，释放其所占的内存空间。