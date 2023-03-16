# Java突围

## 一、Java基础语法

面向对象编程的概念和特性

Java中的关键字和修饰符



## 二、Java集合框架

ArrayList、LinkedList、HashSet、HashMap，它们的实现原理和区别等

> ArrayList、LinkedList、HashSet、HashMap是Java中常用的集合类，它们分别实现了List和Map接口，具有以下的实现原理和区别：
>
> - ArrayList是基于数组实现的，它可以动态地调整数组的大小，以适应元素的增加或删除。它支持随机访问，通过索引可以快速地获取或修改元素，但是插入或删除元素需要移动后面的元素，效率较低。
> - LinkedList是基于双向链表实现的，它由一系列节点组成，每个节点包含一个数据域和两个指针域。它不支持随机访问，通过索引获取或修改元素需要遍历链表，但是插入或删除元素只需要修改指针域，效率较高。
> - HashSet是基于哈希表实现的，它使用一个数组存储一组链表（或红黑树），每个链表（或红黑树）存储一组哈希值相同的元素。它不保证元素的顺序，并且不允许重复元素。它通过计算元素的哈希值来确定其在数组中的位置，并且在链表（或红黑树）中查找是否存在该元素，因此具有较高的查询效率。
> - HashMap也是基于哈希表实现的，但是它使用一个数组存储一组节点（或红黑树），每个节点包含一个键值对。它不保证键值对的顺序，并且不允许重复键。它通过计算键的哈希值来确定其在数组中的位置，并且在节点（或红黑树）中查找是否存在该键，并且返回对应的值。

## 三、Java异常处理机制

异常类的层次结构和常见的异常类型，以及如何正确地使用try-catch-finally和throw-throws等

> 异常类是Java中用来表示程序运行过程中出现的错误或异常情况的类，它们具有以下的层次结构和常见的类型：
>
> - 异常类的最顶层是Throwable类，它是所有异常类的父类，它有两个直接子类：Error和Exception[1](https://rollbar.com/blog/java-exceptions-hierarchy-explained/)
> - Error类表示系统级别的严重错误，如内存溢出、栈溢出等，这些错误通常无法被程序处理或恢复[1](https://rollbar.com/blog/java-exceptions-hierarchy-explained/)
> - Exception类表示程序逻辑或输入输出等方面的错误，如空指针、数组越界、文件未找到等，这些错误通常可以被程序捕获和处理[1](https://rollbar.com/blog/java-exceptions-hierarchy-explained/)
> - Exception类又分为两种：检查型异常（Checked Exception）和非检查型异常（Unchecked Exception）。检查型异常是指编译器要求必须处理的异常，如IOException、SQLException等；非检查型异常是指编译器不强制要求处理的异常，如RuntimeException及其子类
>
> 在Java中，使用try-catch-finally和throw-throws来进行异常处理：
>
> - try-catch-finally语句用于捕获和处理异常。try块包含可能抛出异常的代码；catch块包含处理特定类型异常的代码；finally块包含无论是否发生异常都要执行的代码
> - throw语句用于主动抛出一个异常对象。通常在方法内部使用throw语句来表明该方法遇到了一个无法解决的问题，并且将该问题交给该方法的调用者来处理
> - throws关键字用于声明一个方法可能抛出哪些类型的异常。通常在方法签名中使用throws关键字来表明该方法不会处理这些类型的异常，而是将它们传递给该方法的调用者来处理

## 四、Java多线程编程

Thread类和Runnable接口的创建和启动方式，以及synchronized、volatile、wait、notify等关键字的作用和用法等

> Thread类和Runnable接口的创建和启动方式如下：
>
> - 继承Thread类：定义一个类继承Thread类，重写run()方法，在run()方法中编写线程要执行的任务。然后创建该类的对象，调用start()方法启动线程。
> - 实现Runnable接口：定义一个类实现Runnable接口，实现run()方法，在run()方法中编写线程要执行的任务。然后创建该类的对象，再创建一个Thread对象，将Runnable对象作为参数传递给Thread构造器。最后调用Thread对象的start()方法启动线程。
>
> synchronized、volatile、wait、notify等关键字的作用和用法如下：
>
> - synchronized：用于实现同步代码块或同步方法，保证多个线程在同一时刻只能有一个线程执行该代码块或方法，从而避免数据不一致或并发问题。
> - volatile：用于修饰变量，保证变量在多个线程之间可见，即当一个线程修改了变量的值后，其他线程能够立即看到最新的值。
> - wait：用于让当前线程进入等待状态，并释放持有的锁。通常在同步代码块或同步方法中使用，并配合notify或notifyAll使用。
> - notify：用于唤醒一个在等待状态的线程，并不释放持有的锁。通常在同步代码块或同步方法中使用，并配合wait使用。

## 五、Java网络编程

Socket通信和HTTP协议的基本概念和流程，以及如何使用URL、URLConnection、HttpURLConnection等类进行网络请求和响应等

> Socket通信和HTTP协议是Java中进行网络编程的两种常用方式，它们具有以下的基本概念和流程：
>
> - Socket通信是指基于TCP/IP协议的，通过建立客户端和服务器端的套接字（Socket）来实现数据的传输。客户端和服务器端分别创建一个Socket对象，并且指定对方的IP地址和端口号。然后，客户端发起连接请求，服务器端监听并接受连接请求，建立连接后，双方可以通过输入输出流来进行数据的读写[1](https://blog.csdn.net/qq_41538097/article/details/123697432)
> - HTTP协议是指超文本传输协议（Hypertext Transfer Protocol），它是一种无状态的、应用层的、面向请求/响应的协议。客户端（如浏览器）向服务器发送一个HTTP请求，包含请求行、请求头和请求体；服务器收到请求后，根据请求内容进行处理，并返回一个HTTP响应，包含状态行、响应头和响应体[2](https://docs.oracle.com/javase/8/docs/api/java/net/HttpURLConnection.html)[3](https://www.cnblogs.com/caoweixiong/p/14716187.html)
>
> 在Java中，使用URL、URLConnection、HttpURLConnection等类来进行网络请求和响应：
>
> - URL类表示一个统一资源定位符（Uniform Resource Locator），它可以唯一地标识互联网上的一个资源，并且提供了访问该资源的方法[2](https://docs.oracle.com/javase/8/docs/api/java/net/HttpURLConnection.html)
> - URLConnection类表示一个与URL之间的连接，它可以获取URL相关的信息，如内容类型、长度、最后修改时间等，并且可以读写URL指向的资源[2](https://docs.oracle.com/javase/8/docs/api/java/net/HttpURLConnection.html)
> - HttpURLConnection类是URLConnection类的子类，它专门用于处理HTTP协议的连接，它可以设置HTTP方法（如GET或POST）、添加或获取HTTP头信息、获取HTTP状态码等。

## 六、Java数据库编程

JDBC技术和SQL语言的基本概念和操作，以及如何使用PreparedStatement、ResultSet、Connection等类进行数据库连接和数据操作



## 七、Spring或Spring Boot

核心组件和注解等



## Java新特性

### Java 10

#### var



## 参考

https://www.cxyxiaowu.com/21505.html