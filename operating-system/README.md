## 操作系统



### 基本特征

**1、并发**

- 并发

  - 一段时间内同时运行多个程序
  - 通过引入进程和线程实现

- 并行

  - 同一时刻运行多个指令
  - 硬件支持，如多流水线、多处理器或分布式计算系统

  

**2、共享**

系统资源被多个并发进程共同使用

- 互斥共享：相当于争抢唯一资源，同步机制实现互斥访问
- 同时共享



**3、虚拟**

把一个物理实体转换成多个逻辑实体

主要有两种虚拟技术：

- 时（时间）分复用技术
  - 多个进程在同一个处理器中并发执行，让各个进程轮流使用处理器，每次只执行一小个时间分片
- 空（空间）分复用技术
  - 虚拟内存



**4、异步**

进程不是一次性执行完毕，而是走走停停，以不可知的速度执行。



### 基本功能

1、[进程管理](process.md)

> 进程控制、进程同步、进程通信、死锁处理、处理机调度等

2、内存管理

> 内存分配、地址映射、内存保护与共享、虚拟内存等

3、文件管理

> 文件存储空间管理、目录管理、文件读写管理和保护等

4、设备管理

> 缓冲管理、设备分配、设备处理、虚拟设备等



[Socket](socket.md)