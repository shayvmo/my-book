### Socket

一个输入操作通常包括两个阶段：

- 等待数据准备好
- 从内核向进程复制数据

对于一个套接字上的输入操作，第一步通常涉及等待数据从网络中到达。当所等待数据到达时，它被复制到内核中的某个缓冲区。第二步，把数据从内核缓冲区复制到应用进程缓冲区。

#### I/O 模型

- 阻塞式 I/O
- 非阻塞式 I/O
- I/O复用（select 和 poll）
- 信号驱动式 I/O （SIGIO）
- 异步 I/O （AIO）

#### I/O复用

- select

- poll

  

