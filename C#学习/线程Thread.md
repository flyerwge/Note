# 线程学习

**线程** 被定义为程序的执行路径，每个线程都定义了一个独特的控制流。

**线程生命周期**开始于 System.Threading.Thread 类的对象被创建时，结束于线程被终止或完成执行时。

线程各种状态：

- **未启动状态**：当线程实例被创建但 Start 方法未被调用时的状况。

- **就绪状态**：当线程准备好运行并等待 CPU 周期时的状况。

- **不可运行状态：**

  - 已经调用 Sleep 方法

  - 已经调用 Wait 方法
  - 通过 I/O 操作阻塞

- **死亡状态**：当线程已完成执行或已中止时的状况。

## 创建

1、创建执行静态方法的线程:

```c#
using System;
using System.Threading;

class Test
{
    static void Main() 
    {
        Thread newThread = new Thread(new ThreadStart(Work.DoWork));
        newThread.Start();
    }
}

class Work 
{
    Work() {}
    public static void DoWork() {}
}
```

创建执行实例方法的线程:

```c#
using System;
using System.Threading;

class Test
{
    static void Main() 
    {
        Work threadWork = new Work();
        Thread newThread = new Thread(new ThreadStart(threadWork.DoWork));//创建线程
        newThread.Start();//线程开启
    }
}

class Work 
{
    public Work() {}
    public void DoWork() {}
}
```

==注：==线程在创建时不会开始执行。若要安排线程执行，请调用[Start](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.start?view=netcore-3.1)方法。要将数据对象传递给线程，请使用[Start（Object）](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.start?view=netcore-3.1#System_Threading_Thread_Start_System_Object_)方法重载。

## 开启

通过提供一个代表该线程将在其类构造函数中执行的方法的委托来启动线程。然后，您调用[Start](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.start?view=netcore-3.1)方法开始执行。该[线程](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread?view=netcore-3.1)的构造函数可以采取以下两种委托类型，取决于你是否可以传递参数的方法来执行：

- 如果该方法没有参数，则将[ThreadStart](https://docs.microsoft.com/en-us/dotnet/api/system.threading.threadstart?view=netcore-3.1)委托传递给构造函数

```c#
Thread savetoDb = new Thread(new ThreadStart(SavetoDb));//savetoDb方法没有参数
savetoDb.Start();
```

- 如果方法具有参数，则将[ParameterizedThreadStart](https://docs.microsoft.com/en-us/dotnet/api/system.threading.parameterizedthreadstart?view=netcore-3.1)委托传递给构造函数

```c#
Thread SaveDatatoDb = new Thread(new ParameterizedThreadStart(SavetoDb));//savetoDb方法有参数
SaveDatatoDb.Start();
```



## 管理

- **AutoResetEvent**：线程通过调用 **AutoResetEvent** 上的 WaitOne 来等待信号，可以控制线程进行顺序。

```c#
 static void Main(string[] args)
        {
            AutoResetEvent autoEvent = new AutoResetEvent(false);
            ThreadPool.QueueUserWorkItem(new WaitCallback(ThreadMethod), autoEvent);//线程一
            autoEvent.WaitOne();
            ThreadPool.QueueUserWorkItem(new WaitCallback(WorkMethod), autoEvent);//线程二
            autoEvent.WaitOne();
            Console.ReadLine();
        }
```

- **sleep()** 方法用于在一个特定的时间暂停线程

```c#
 Thread.Sleep(5000);//线程暂停5000毫秒
```



## 销毁

**Abort()** 方法用于销毁线程。

通过抛出 **threadabortexception** 在运行时中止线程。这个异常不能被捕获，如果有 *finally* 块，控制会被送至 *finally* 块。

```c#
using System;
using System.Threading;

namespace MultithreadingApplication
{
    class ThreadCreationProgram
    {
        public static void CallToChildThread()
        {
            try
            {

                Console.WriteLine("Child thread starts");
                // 计数到 10
                for (int counter = 0; counter <= 10; counter++)
                {
                    Thread.Sleep(500);
                    Console.WriteLine(counter);
                }
                Console.WriteLine("Child Thread Completed");

            }
            catch (ThreadAbortException e)
            {
                Console.WriteLine("Thread Abort Exception");
            }
            finally
            {
                Console.WriteLine("Couldn't catch the Thread Exception");
            }

        }
       
        static void Main(string[] args)
        {
            ThreadStart childref = new ThreadStart(CallToChildThread);
            Console.WriteLine("In Main: Creating the Child thread");
            Thread childThread = new Thread(childref);
            childThread.Start();
            // 停止主线程一段时间
            Thread.Sleep(2000);
            // 现在中止子线程
            Console.WriteLine("In Main: Aborting the Child thread");
            childThread.Abort();
            Console.ReadKey();
        }
    }
}
```

当上面的代码被编译和执行时，它会产生下列结果：

```c#
In Main: Creating the Child thread
Child thread starts
0
1
2
In Main: Aborting the Child thread
Thread Abort Exception
Couldn't catch the Thread Exception 
```

   