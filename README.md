# code-interview-selft
给自己找工作用的


## 微服务
###dubbo
1.dubbo如何一条链接并发多个调用。Dubbo的原理，序列化相关问题。

###spring boot 相关面试题




## 1
1. 线程池的一些原理，锁的机制升降级
2. Hadoop底层调度
3. threadLocal 底层
3. 秒杀系统的设计
4. 一个整形数组，给定一个数，在数组中找出两个数的和等于这个数，并打印出来，我写的时间复杂度高，要求O(n)
5. n个整数，找出连续的m个数加和是最大
6. 数据库锁隐原理
7. 1000个线程同时运行，怎么防止不卡
8. 高并发量大的话怎么处理热点，数据等
9. 如何获取一个本地服务器上可用的端口
10. 流量控制相关问题
11. 数据库TPS是多少，是否进行测试过（
12. 缓存击穿有哪些方案解决
13. 分布式锁，redis缓存，spring aop，系统架构图
14. 分布式事务一致性
15. HTTP2.0、thrift
16. 微信红包怎么实现。

## 2
1. 单例模式 懒汉式、饿汉式、双重校验锁、静态加载，内部类加载、枚举类加载。保证一个类仅有一个实例，并提供一个访问它的全局访问点。

	答:懒汉模式:要的时候才生产.恶汉模式: 一来就有了.  双重检查锁+volatile,静态加载:设置成静态属性. 内部类加载: 里面有个静态内部类静态方法,加载的时候创建

'''
public class Singleton
{
    private Singleton(){}
    
    static {
        System.out.println("This's static code block!");
    }
    
    private static class SingletonHandler {
        private static Singleton singleton = new Singleton();
        static {
            System.out.println("This's innerClass's static code block");
        }
    }
    
    public static Singleton getInstance(){
        return SingletonHandler.singleton;
    }
    
    public static void display(){
        System.out.println("This's display!");
    }
}

'''

2. 代理模式：动态代理和静态代理，什么时候使用动态代理。

|||



3. 装饰者模式：动态给类加功能。
4. 观察者模式：有时被称作发布/订阅模式，观察者模式定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主题对象在状态发生变化时，会通知所有观察者对象，使它们能够自动更新自己。
5. 策略模式：定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。
6. 外观模式：为子系统中的一组接口提供一个一致的界面，外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。
7. 命令模式：将一个请求封装成一个对象，从而使您可以用不同的请求对客户进行参数化。
8. 创建者模式：将一个复杂的构建与其表示相分离，使得同样的构建过程可以创建不同的表示。
9. 抽象工厂模式：提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。
10. 什么时候使用Linkedhashmap、Concurrenthashmap、Weakhashmap
11. 什么时候使用Hashmap
12. Arrays.sort的实现
13. 什么时候使用CopyOnArrayList
	 答:适用场景:读多写少,数据最终一致性。
	 缺点:
	  1. CopyOnWrite容器只能保证数据的最终一致性，不能保证数据的实时一致性。所以如果你希望写入的的数据，马上能读到，请不要使用CopyOnWrite容器。
	  2.  因为CopyOnWrite的写时复制机制，所以在进行写操作的时候，内存里会同时驻扎两个对象的内存，旧的对象和新写入的对象（注意:在复制的时候只是复制容器里的引用，只是在写的时候会创建新对象添加到新容器里，而旧容器的对象还在使用，所以有两份对象内存）。如果这些对象占用的内存比较大，比如说200M左右，那么再写入100M数据进去，内存就会占用300M，那么这个时候很有可能造成频繁的Yong GC和Full GC。之前我们系统中使用了一个服务由于每晚使用CopyOnWrite机制更新大对象，造成了每晚15秒的Full GC，应用响应时间也随之变长。
	3. 优点:CopyOnWrite容器即写时复制的容器。通俗的理解是当我们往一个容器添加元素的时候，不直接往当前容器添加，而是先将当前容器进行Copy，复制出一个新的容器，然后新的容器里添加元素，添加完元素之后，再将原容器的引用指向新的容器。这样做的好处是我们可以对CopyOnWrite容器进行并发的读，而不需要加锁，因为当前容器不会添加任何元素。所以CopyOnWrite容器也是一种读写分离的思想，读和写不同的容器。
14. volatile的使用
     + 可见性
     + 禁止重排序     
15. synchronied的使用
		+ 偏向锁->轻量锁->重量锁 
16. reentrantlock的实现和Synchronied的区别
     + reentrantlock 基于aqs框架(底层算法clh队列),java 语言级别可重入锁实现
     +  Synchronied 编译器级别实现, bytecode monitorenter monitor exit
        
17. CAS的实现原理以及问题
      + compare and swap 需要cpu底层指令支持cas 算法,天然原子性, 方便无锁编程
18. 双亲委派模型
19. 类加载机制的步骤，每一步做了什么，static和final修改的成员变量的加载时机
20. 反射机制：反射动态擦除泛型、反射动态调用方法等
21. mysql的优化策略有哪些
22. mysql索引的实现 B+树的实现原理
23. 什么情况索引不会命中，会造成全表扫描
24. java中bio nio aio的区别和联系
25. Reactor模型和Proactor模型
26. http三次握手和四次挥手
27. StringBuff 和StringBuilder的实现，底层实现是通过byte数据，外加数组的拷贝来实现的
28. Future和ListenableFuture 异步回调相关
29. 如果线上服务器频繁地出现full gc ，如何去排查
30. reactor模型的演变
31. linux命令，awk、sed,cat、sort、cut、grep、uniq、wc、top等

	1. 命令grep，更适合单纯的查找或匹配文本, 
	2. awk 格式化文本逐行处理,begin {} end{}
	3. sort 用来给文本的行排序 
	4. cut 略
	5. grep 搜搜文本 -r 级联 -n 行号 --color 标红   -o 只显示匹配词 
	6. wc -l 行数 -c 统计字节数。 -m 统计字符数    -w 统计字数。
	7. top  性能必备
 







32. 压力测试相关，怎么分析，单接口压测和多情况下的压测
33. 缓存的设计和优化
34. 缓存和数据库一致性同步解决方案
35. ActiveMQ、RabbitMQ、Kafka的区别
36. 多个线程同时读写，读线程的数量远远大于写线程，你认为应该如何解决并发的问题？你会选择加什么样的锁？
     1. 读写锁


37. Tomcat本身的参数你⼀一般会怎么调整？
答:export JAVA_OPTS=""-Dfile.encoding=UTF-8 -server -Xms1400M -Xmx1400M -Xss512k
-XX:+AggressiveOpts
-XX:+UseBiasedLocking -XX:PermSize=128M -XX:MaxPermSize=256M
-XX:+DisableExplicitGC -XX:MaxTenuringThreshold=30 -XX:+UseConcMarkSweepGC
-XX:+UseParNewGC  -XX:+CMSParallelRemarkEnabled -XX:ReservedCodeCacheSize=32m
-XX:+UseCMSCompactAtFullCollection -XX:LargePageSizeInBytes=128m 
-XX:+UseFastAccessorMethods -XX:+UseCMSInitiatingOccupancyOnly
-Djava.awt.headless=true"
 + server 意味着是已真正的生产环境来运行
 + 初始大小和最大大小一致
 + 使用偏向锁,有时候可以禁用,可重入底层jvm
 + DisableExplicitGC 严禁代码显式gc
 + MaxTenuringThreshold这个参数用于节制对象能履历几多次Minor GC才提升到旧生代，默许值是15，
 + UseConcMarkSweepGC  使每次停顿尽量短, UseParNewGC 新生代并行收集
 + 
 + 





38. 线程池内的线程如果全部忙，提交一个新的任务，会发生什什么？队列全部塞满了之后，还是忙，再提交会发生什么？
39. aba问题?
    + StampedLock
39. wait/notify/notifyAll方法需不需要被包含在synchronized块中？这是为什么？
	答:需要,因为wait notify, notifyAll 都是等待条件发生,或者条件已经改变,可以通知,如果没有的话,可能引起race condition, 先验判断失效,毫无意义.
	

40. ExecutorService你一般是怎么用的？是每个service放一个还是一个项目里面放一个？有什么好处？
    答:参考java并发编程实战所说,最好是一类任务放一个线程池,不然会造成业务耦合或者死锁,饥饿
    
41. Spring的声明式事务 @Transaction注解一般写在什么位置? 抛出了异常会自动回滚吗？有没有办法控制不触发回滚?
42. 你们的数据库单表数据量是多少？一般多大的时候开始出现查询性能急剧下降？
43. Perm Space中保存什么数据? 会引起OutOfMemory吗？
    perm space 主要PermSpace主要是存放静态的类信息和方法信息，静态的方法和变量，final标注的常量信息等。
    一般两种情况爆: 1.一直搞新字符串 intern() ,爆常量池.
    				2.cglib 搞出很多新类出来.爆
    				
44. Linux下面如果想看某个进程的资源占用情况是怎么看的？系统load大概指的什么意思？你们线上系统load一般多少？如果一个4核机器，你认为多少load是比较正常的？top命令里面按一下1会发生什么?
45. 查看网络连接发现好多TIMEWAIT 可能是什么原因？对你的应用会有什么影响？你会选择什么样的方式来减少这些TIMEWAIT
 答: <a href=https://www.cnblogs.com/softidea/p/5741192.html><a/>
46. 可否介绍一下TCP三次握手的过程，如果现在有个网络程序，你用第三方的library来发送数据，你怀疑这个library发送的数据有问题，那么怎么来验证？tcpdump导出的文件你一般是怎么分析的？
47. 缓存穿透可以介绍一下么？你认为应该如何解决这个问题?
48. .你是怎么触发缓存更新的？(比如设置超时时间(被动方式), 比如更新的时候主动update)？如果是被动的方式如何控制多个入口同时触发某个缓存更新？
49. 你们用Redis来做什么？为什么不用其他的KV存储例例如Memcached,Cassandra等?
50. 你熟悉哪些Redis的数据结构? zset是干什么的? 和set有什么区别?
51. .Redis中List, HashTable都用到了ZipList, 为什么会选择它?



## linux底层
1.  nio的底层实现。
 答:Linux的内核将所有外部设备都可以看做一个文件来操作,对一个socket的读写也会有相应的描述符，称为socketfd(socket描述符)
 下图阻塞调用
 ![Alt text](https://img-blog.csdn.net/20150907142335811)
 
 下图非阻塞调用
 ![Alt text](https://img-blog.csdn.net/20150907142428853)
 I/O复用模型
 ![Alt text](https://img-blog.csdn.net/20150907142605678)
 信号驱动异步I/O模型
 ![Alt text](https://img-blog.csdn.net/20150907142638225)
 异步I/O模型
 ![Alt text](https://img-blog.csdn.net/20150907142720641)
 
 前四种都是同步IO，在内核数据copy到用户空间时都是阻塞的。 
最后一种是异步IO，通过API把IO操作交由操作系统处理，当前进程不关心具体IO的实现，通过回调函数，或者信号量通知当前进程直接对IO返回结果进行处理。
Java BIO ： 同步并阻塞，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善。

Java NIO ： 同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。（底层是epoll）
Java AIO(NIO.2) ： 异步非阻塞，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理

2. 排序算法
  ![](https://img-blog.csdn.net/20180807094112221?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3OTYyNjAw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
  单轴点快速排序: 
  + 交换指针法
  + 挖坑
  + 双轴点快速排序,java内部采用 arrays 工具方法碰到基本类型 喜欢这种算法,原因是不容易试算法变得不稳定的哦o(n^2),因为是基本类型所以,原地置换位置,方便的很,但是用到了堆栈 空间复杂度是log 2 n 
  + timsort 分成run, 然后归并,归并的时候记得掐头去尾,适当时候还得开舞动模式,如果舞动模式不成功,就回归普通模式,记得入栈,上下依次是xyz,z>y+x 和y>x 要保持,直到最后合并一个run,目的是为了保持每次归并,能够保持合并的2个run接近一样大小,这样就可以接近log 2n ,同时可以利用已经有的顺序,此方法比较优秀
  + arrays 对引用排序 一般情况下 可选 归并 或者 timsort,未来会移除 归并. 
  + 直接插入排序,数目少时候很有效. 打扑克牌
  + shell 排序就是加强版的插入排序,只是插入排序要一个个的移动,shell可以跳跃移动
  + 堆排序 利用了 最大堆,可以sink和swim 保持依次取最大的头,变态版选择排序
  + 
   





