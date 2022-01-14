# 队列

> 先进先出 First In First Out



- 顺序队列
- 链队



### 单队列

- 顺序队列（数组）
- 链式队列（链表）

顺序队列或存在「假溢出」问题，明明数组还有空间，却无法入队。

> 为了避免当只有一个元素的时候，队头和队尾重合使处理变得麻烦，所以引入两个指针，front 指针指向对头元素，rear 指针指向队列最后一个元素的下一个位置，这样当 front 等于 rear 时，此队列不是还剩一个元素，而是空队列。——From 《大话数据结构》





### 循环队列

> 通过模运算方式 Q.rear = (Q.rear + 1) % Q.maxsize 建立循环队列，解决「假溢出」问题和越界问题

顺序队列中，front 等于 rear 时，队列为空。但是在循环队列中，有可能是队列满了。

解决方式：

- 增加一个标识flag变量，标识队列是否满了
- ( rear + 1) % Q.maxsize = front ，如果相等，说明队列已满



### 常用场景

当我们需要按照一定顺序处理数据时可以考虑使用队列。

- 阻塞队列
- 线程池中的请求/任务队列
- Linux内核进程队列
- 播放列表
- 消息队列
- 等等...