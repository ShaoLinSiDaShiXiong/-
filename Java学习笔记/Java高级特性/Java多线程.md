# Java多线程

**多线程面试题：https://blog.csdn.net/JAYU_37/article/details/106321844**

## 线程的基本概念

**我们每次在电脑上打开一个程序，就会出现一个进程，一个进程可以包括多个线程，每个线程之间都是独立的，相互之间互不干扰。**

**线程是进程中 执行运算的最小单位，是进程中的一个实体，是被系统独立调度和分派的基本单位，线程自己不拥有系统资源，只拥有一点在运行中必不可少的资源，但他可与同属一个进程的其他线程共享进程所拥有的全部资源，一个线程可以创建撤销另一个线程，同一进程中的多个线程可以并发执行。**

- 进程：

  进程可以理解为一运行中的程序，而进程中每一个执行的任务都是一个线程。每个进程都有独立的代码和数据空间，进程间切换会有较大的开销，一个进程包含1~n个线程。

- 线程：

  线程是进程中的一个个小任务，一个进程中的多个线程之间互不干扰，但线程之间可以进行信息交换。进程中都会有一个主线程，但是也会有主线程执行完 其余线程还在执行的情况。同一类线程共享代码和数据空间，每一个线程有独立的运行栈和程序计数器（PC），线程切换开销小。（线程是cpu调度的最小单位）

## 线程的几个主要概念

- 线程同步
- 线程通信
- 线程死锁
- 线程控制：挂起、停止和恢复

## 并发与并行的区别

**在普通的电脑上，cpu都是单线程的，也就是以并发的形式来完成任务。**

1. 并发：线程的并发可以理解为同一个人不间断的完成多个任务。

   多个任务在同一个cpu上，按照细分的时间片进行轮流交替执行，由于时间很短，看上去好像是同时进行的。

2. 并行：线程的并行可以理解成有三个不同的人，每个人同时开始，各自完成自己的任务。

   单位时间内，多个处理器或多核处理器同时处理多个任务，是真正意义上你的同时进行。

## Java多线程编程

### 线程的生命周期

**一个线程的生命周期大致来看有五个部分**

1. 新建状态 new：

   使用new关键字创建一个新的线程对象之后，该线程就处于新建状态。他保持这个状态直到程序start()这个程序。

2. 就绪状态 start：

   当线程调用了start()方法之后，该线程就进入就绪状态，就绪状态的线程处于就绪队列中，要等待JVM虚拟机里线程会给你调度器的调度。

3. 运行状态

   如果就绪状态的线程获取cpu资源，就可以执行run()方法，此时线程便处于运行状态。处于运行装的线程最为复杂，它可以变为阻塞状态，就绪状态和死亡状态。

4. 阻塞状态

   如果一个线程进行了sleep（睡眠），suspend（挂起）等方法,失去占用资源之后，该线程就从运状态进入到阻塞状态，在睡眠时间已到或获得设备资源后可以重新进入就绪状态。可分为三种：

   - 等待阻塞：运行状态中的线程执行wait()方法，使线程进入到等待阻塞状态。
   - 同步阻塞 ：线程在获取synchronized同步锁失败（因为同步锁被其他线程占用）。
   - 其他阻塞：通过调用线程的sleep()或join()发出了I/O请求时，线程就会进入到阻塞状态。当sleep()状态超时，join()等待线程终止或超时，或I/O处理完毕，线程重新转入就绪状态。
   - 

5. 死亡状态：

   一个运行状态的线程完成任务或者其他终止条件发生时，该线程就会切换到终止状态。

![ae305b4e9751c0f3a203e01ea2daead](G:\笔记\Java学习笔记\img\ae305b4e9751c0f3a203e01ea2daead.jpg)

![ae305b4e9751c0f3a203e01ea2daead](E:\笔记\Java学习笔记\img\ae305b4e9751c0f3a203e01ea2daead.jpg)

#### 线程同步

**在现实生活中有一个银行账户，有两个人同一时刻同时往这个账户中存钱，如果没有线程同步，可能会出现三种情况：1.存进去两百。2.存进去一百。3.没有存进没去。**

**synchroized线程同步是保证了某个资源在某个时刻只会被一个线程访问（可以理解为synchronized是保护一部分资源不被同时调用而导致程序出错），线程同步通常采用三种方式：同步代码块，同步方法，同步锁。**

**synchronized锁定的是对象，而不是代码块，synchronized也可以修饰类，被修饰的类里面的方法都会变成synchronized方法。**

1. 同步代码块：就是使用synchronized关键字的代码块，作用的范围是{}内所有的内容，作用的对象是调用这个代码块的对象。任何时刻只能又一个线程可以获得对同步监视器的锁定，当同步代码块执行完之后，该线程会释放对该同步监视器的锁定，此时如果还有其他的线程需要获得代码块中的资源，则需要去抢夺同步监视器。
2. 同步方法:   就是被synchronized关键字修饰的方法（在访问修饰符之后，返回类型之前），作用范围是整个方法，作用的对象是调用这个方法的对象。
2. 同步静态方法：就是被synchronized关键字修饰的静态方法，作用的范围是整个静态方法，作用的对象是这个类的所有对象。
3. 同步锁:

### Java中使用多线程的方式

**基本的Java线程模型：**

- Thread类
- Runnable接口（常用）
- Callable接口
- Futuer接口

我们可以使用继承Thread类，或者实现Runnable，Callable和Futuer接口来进行线程的创建。

#### 实现Runnable接口创建线程

我们可以通过实现 Java API提供的Runnable接口来创建线程。Runnable接口只有一个run方法，我们每次实现接口的时候都需要重写run方法。

```java
public class Test implements Runnable{
    public void run(){
        System.out.println("hello");
    }
    public static void main(String[] args){
        Thread thread = new Thread(new Test());
        thread.start();
    }
}
```

**Java提供的Thread方法中有一个构造方法：public Thread(Runnable targer)。**

**此方法可以接受Runnable接口的子类实例，也就是说可以通过Thread类来启动Runnable实现多线程。**

#### 通过Thread来创建线程

创建一个线程的一个方法是，创建一个新的类继承Thread类。新的类必须重写run( )方法，该方法是线程的入口点。它必须调用start( )方法才能执行。该方法尽管被列为一种多线程的实现方式，但本质上也是实现了Runnable接口的一个实例。

##### Thread类中的常用方法

|    名称     | 返回类型 | 参数列表 |                             作用                             | 实例代码                                    |
| :---------: | :------: | :------: | :----------------------------------------------------------: | ------------------------------------------- |
|     run     |   void   |          |                       线程的执行方法。                       | public void run ()                          |
|    start    |   void   |          | 启动线程的方法，启动线程后会自动执行run( )方法。Java虚拟机调用该线程的run( )方法。 | public synchronized void start ()           |
|    stop     |   void   |          |          线程停止，该方法已过期，可以使用但不推荐。          |                                             |
|   setName   |   void   |  String  |               改变线程名称，使之与参数name相同               | public final void setName (String name)     |
| setPriority |   void   |   int    |                       更改线程的优先级                       | publi final void setPriority (int priority) |
|  setDaemon  |   void   | boolean  |               将该线程标记为守护线程或用户线程               | public final void setDaemon (boolean on)    |
|    join     |   void   |   long   |             等待该线程终止的时间最长为millis毫秒             | public final void join (long millisec)      |
|  interrupt  |   void   |          |                           中断线程                           | public void interrupt ()                    |
|   isAlive   | boolean  |          |                   测试线程是否属于活动状态                   | public final boolean isAlive ()             |

**Thread类的静态方法：**

|      方法名       | 返回类型 | 参数列表 |                             作用                             | 实例代码                                   |
| :---------------: | :------: | :------: | :----------------------------------------------------------: | ------------------------------------------ |
|       yield       |   void   |          |         暂停当前正在执行的线程对象，并执行其他线程。         | public static void yield ()                |
|     **sleep**     |   void   |   long   | 在指定的毫秒数内让当前正在执行的线程休眠（暂停执行），此操作收到系统计时器和调度程序精度和精确性的影响。 | public static void sleep (long millisecc)  |
|     holdsLock     | boolean  |  Object  | 当且仅当当钱线程在指定的对象上保持监视器锁定时，才返回true。 | public static boolean holdsLock (Object x) |
| **currentThread** |  Thread  |          |            返回对当前正在被执行的线程对象的信息。            | public static Thread currenThread ()       |
|     dumpStack     |   void   |          |            将当前线程的堆栈跟踪打印至标准错误流。            | public static void dumpStack ()            |



##### Thread类的使用

```java
public class MyThread extends{
    //重写继承Thread类的run方法。
    public void run(){
        System.out.println("线程启动");
    }
}
public class Main{
    public static void main(String[] args){
        MyThread thread1 = new MyThread();
        MyThread thread2 = new MyThread();
        thread.start1();
        thread.start2();
    }
}
```

因为这里使用的是Thread类中的start方法所以运行程序之后，两个线程的出现顺序是不固定的，但是如果使用的是run方法的话就会像正常的代码执行顺序，从上到下依次运行。

###### Thread类中start()方法和run()的区别



**start()方法用于启动线程，run()方法用于执行线程运行的代码，run()方法可以反复调用，而start()方法只能被调用一次。**



**start()方法用于启动一个线程，真正的实现了多线程的运行。调用start()方法不用等待run()方法执行结束，可以直接执行其他的代码。**



**虽然使用start方法和run方法的本质都是执行run方法，但是start方法执行run方是虚拟机进行执行的，所以顺序是不固定的**



**当我们new了一个Thread对象，线程就进入了新建状态。start方法的作用是使线程进入就绪状态，当分配到cpu的时间片之后就可以运行了，然后在执行run方法 运行线程体，这才是真正的多线程工作。**



1. start()：

   API介绍	使该线程开始执行，Java虚拟机调用该线程的run方法。

   多次启动一个线程是非法的，特别是当线程已经结束执行后，不能再重新启动，用start方法来启动线程，真正实现了多线程运行，这是无需等待run()方法体中的代码执行完毕而直接继续执行后续代码。**通过调用Thread类的start()方法来启动一个线程，这时此线程处于“就绪”状态（可运行状态）。并没有运行，一旦得到cpu时间片，就开始执行run()方法。**这里run()方法称为线程体，它包含了要执行的这个线程的内容，run()方法运行结束，此线程随即终止。

2. run()：

   API介绍	如果该线程是独立的Runnable运行对象构造的，则调用该Runnable对象的run方法，否则该方法不执行任何操作并返回。**Thread的子类应该重写run方法。**

   run方法只是一个类的普通方法而已，如果直接调用run方法，程序中依然只有主线程这一个线程，其程序执行路径还是只有一条，还是哟啊顺序执行，还是要等待run方法体执行完毕之后才可以继续执行下面的代码，这样就没有达到写线程的目的。

3. **总结：调用start方法可以启动线程，而run方法只是thread类中的一个普通方法调用，还是在主线程里执行的。**

