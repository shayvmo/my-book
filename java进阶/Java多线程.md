### Java多线程



最近更新于：2020年12月15日



在 Java 中，创建线程有以下 3 种方式

1. 继承 `Thread` 类，重写 `run()` 方法，该方法代表线程要执行的任务；

   ```java
   /**
    * @author colorful@TaleLin
    */
   public class ThreadDemo2 {
   
       /**
        * 静态内部类
        */
       static class MyThread extends Thread {
   
           private int i = 3;
   
           MyThread(String name) {
               super(name);
           }
   
           @Override
           public void run() {
               while (i > 0) {
                   System.out.println(getName() + " i = " + i);
                   i--;
               }
           }
   
       }
   
       public static void main(String[] args) {
           // 创建两个线程对象
           MyThread thread1 = new MyThread("线程1");
           MyThread thread2 = new MyThread("线程2");
           // 启动线程
           thread1.start();
           thread2.start();
       }
   
   }
   
   ```

   

2. 实现 `Runnable` 接口，实现 `run()` 方法，该方法代表线程要执行的任务；

   ```java
   /**
    * @author colorful@TaleLin
    */
   public class RunnableDemo1 implements Runnable {
   
       private int i = 5;
   
       @Override
       public void run() {
           while (i > 0) {
               System.out.println(Thread.currentThread().getName() + " i = " + i);
               i--;
           }
       }
   
       public static void main(String[] args) {
           // 创建两个实现 Runnable 实现类的实例
           RunnableDemo1 runnableDemo1 = new RunnableDemo1();
           RunnableDemo1 runnableDemo2 = new RunnableDemo1();
           // 创建两个线程对象
           Thread thread1 = new Thread(runnableDemo1, "线程1");
           Thread thread2 = new Thread(runnableDemo2, "线程2");
           // 启动线程
           thread1.start();
           thread2.start();
       }
   
   }
   
   ```

   

3. 实现 `Callable` 接口，实现 `call()` 方法，`call()` 方法作为线程的执行体，具有返回值，并且可以对异常进行声明和抛出

   ```java
   import java.util.concurrent.Callable;
   import java.util.concurrent.ExecutionException;
   import java.util.concurrent.FutureTask;
   
   /**
    * @author colorful@TaleLin
    */
   public class CallableDemo1 {
   
       static class MyThread implements Callable<String> {
   
           @Override
           public String call() { // 方法返回值类型是一个泛型，在上面 Callable<String> 处定义
               return "我是线程中返回的字符串";
           }
   
       }
   
       public static void main(String[] args) throws ExecutionException, InterruptedException {
           // 常见实现类的实例
           Callable<String> callable = new MyThread();
           // 使用 FutureTask 类来包装 Callable 对象
           FutureTask<String> futureTask = new FutureTask<>(callable);
           // 创建 Thread 对象
           Thread thread = new Thread(futureTask);
           // 启动线程
           thread.start();
           // 调用 FutureTask 对象的 get() 方法来获得线程执行结束后的返回值
           String s = futureTask.get();
           System.out.println(s);
       }
   
   }
   
   ```

   

线程休眠

`sleep()` 静态方法，该方法可以使当前执行的线程睡眠（暂时停止执行）指定的毫秒数



#### 线程的状态和生命周期



`java.lang.Thread.Starte` 枚举类中定义了 6 种不同的线程状态：

1. `NEW`：新建状态，尚未启动的线程处于此状态；
2. `RUNNABLE`：可运行状态，Java 虚拟机中执行的线程处于此状态；
3. `BLOCK`：阻塞状态，等待监视器锁定而被阻塞的线程处于此状态；
4. `WAITING`：等待状态，无限期等待另一线程执行特定操作的线程处于此状态；
5. `TIME_WAITING`：定时等待状态，在指定等待时间内等待另一线程执行操作的线程处于此状态；
6. `TERMINATED`：结束状态，已退出的线程处于此状态。