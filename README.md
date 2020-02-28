# Interview
* [C++](https://github.com/FangChao1086/Interview//blob/master/C%2B%2B.md)
* [python](https://github.com/FangChao1086/Interview/tree/master/python)
* [Linux](https://github.com/FangChao1086/Interview/blob/master/Linux.md)
  * [命令搜索](https://wangchujiang.com/linux-command/)  
* [mysql常用命令](https://mp.weixin.qq.com/s/wUCVeYLxx5JL2Xy-XJNvNQ)    

[算法与数据结构](#算法与数据结构)    
[操作系统](#操作系统)  
[计算机网络](#计算机网络)  
[设计模式](#设计模式)  

<span id="算法与数据结构"></span>
# 算法与数据结构
* [红黑树](#红黑树)
* [B树与B+详解 ](#B树与B+详解 )

<span id="红黑树"></span>
## 红黑树
* 节点是黑色或者红色
* 根节点是黑色
* 每个叶节点（NIL节点，空节点）是黑色的
* 每个红节点的两个子节点都是黑色的
* 从任一节点到其每个叶子节点的所有路径都包含相同数目的黑色节点
### 红黑树的旋转
* 左旋
  * 对某个节点x做右旋，假设其右孩子为y。旋转后，y成为新的子树根节点，x成为y的左孩子，y的左孩子成为x的右孩子
<div align=center><img src="https://github.com/FangChao1086/Interview/blob/master/依赖文件/左旋.png"></div>

* 右旋
  * 对某个节点x做左旋，假设其左孩子为y。旋转后，y成为新的子树根节点，x成为y的右孩子，y的右孩子成为x的左孩子
<div align=center><img src="https://github.com/FangChao1086/Interview/blob/master/依赖文件/右旋.png"></div>

<span id="B树与B+详解"></span>
## B树与B+详解 
目的：降低树的深度，提高查找效率  
[参考链接：B树与B+详解](https://www.cnblogs.com/guohai-stronger/p/9225057.html)
### B树（B-树）
<div align=center><img src="https://github.com/FangChao1086/Interview/blob/master/依赖文件/b树.jpg"></div>  

m阶的B树：
1. 根结点至少有两个孩子（除了没有孩子的根结点）
2. 每个中间节点都包含 `k - 1` 个元素和 `k` 个孩子，其中 `m/2 <= k <= m`
3. 每个叶子节点都包含 `k - 1` 个元素，其中 `m/2 <= k <= m`
4. 所有的叶子结点都出现在同一层中
5. 每个节点中元素从小到大排列，节点中 `k - 1` 个元素正好是 `k` 个孩子包含元素的值域划分

> B树的插入：
>> 1. 如果B树已存在需要插入的键值时，用新的值替换旧的值
>> 2. 若B树不存在这个值时，则是在叶子结点进行插入操作。
  
> 一棵含有N个总关键字数的m阶的B树的最大高度是多少?  
>> 1. log_ceil(m/2)((N+1)/2)+1=**log┌m/2┐((N+1)/2)+1**
>> 2. 树中每个结点含有最多含有m个孩子，即m满足：ceil(m/2)<=m<=m

### B+树
<div align=center><img src="https://github.com/FangChao1086/Interview/blob/master/依赖文件/b+树.jpg"></div>   
1. 有 `k` 棵子树的中间节点包含 `k` 个元素，每个元素不保留数据，只用来索引，所有数据都保存在叶子节点
2. 所有的叶子结点包含全部元素信息，及指向这些元素记录的指针，且叶子节点本身依关键字大小自小到大顺序连接；
3. 所有中间节点元素都同时存在于子节点，在子节点元素中是最大（或最小）元素）

* B+树的优点
  * **查询的IO次数更少**
    * 同样数据量的情况下，B+树比B-树更加矮胖，查询时IO次数更少
      * 中间节点没有卫星数据，所以同样磁盘可以容纳更多的节点元素
  * **查询性能稳定**
    * 中间节点仅仅作为叶子结点的关键字索引，因此所有的关键字查询都会走一条从根节点到叶子结点的路径。**即s所有关键字查询的长度是一样的，查询效率稳定**
  * 范围查询简便
    * **B树**需要先自上而下查到底，然后**中序遍历**往上查
	* **B+树**查到底后，叶子节点**链表上遍历**即可

> B+树插入：
>> 1. 若为空树，直接插入，此时也就是根结点
>>  2. 对于叶子结点：根据key找叶子结点，对叶子结点进行插入操作。插入后，如果当前结点key的个数不大于m-1，则插入就结束。
>>> 反之将这个叶子结点分成左右两个叶子结点进行操作，左叶子结点包含了前m/2个记录，右结点包含剩下的记录key，将第m/2+1个记录的key进位到父结点中（父结点必须是索引类型结点），进位到父结点中的key左孩子指针向左结点,右孩子指针向右结点。

>>3. 针对索引结点：如果当前结点key的个数小于等于m-1，插入结束。
>>>>> 反之将这个索引类型结点分成两个索引结点，左索引结点包含前(m-1)/2个数据，右结点包含m-(m-1)/2个数据，然后将第m/2个key父结点中，进位到父结点的key左孩子指向左结点, 父结点的key右孩子指向右结点。

<span id="操作系统"></span>
# 操作系统
[进程与线程](#进程与线程)  
[互斥锁与读写锁](#互斥锁与读写锁)  
[内存溢出和内存泄漏](#内存溢出和内存泄漏)

## 进程与线程
* **进程**
  * 对运行时程序的封装
  * **系统进行资源调度和分配的的基本单位**
  * 实现了操作系统的并发
* **线程**
  * 进程的子任务
  * **CPU调度和分派的基本单位**
  * 用于保证程序的实时性，实现进程内部的并发
### 区别
* 线程依赖于进程而存在
  * 一个线程只能属于一个进程，一个进程至少有一个线程，可以有多线程
* 进程是资源分配的最小单位，线程是CPU调度的最小单位
* 一个进程崩溃，不会对其他进程产生影响；而一个线程崩溃，会让同一进程内的其他线程也死掉。
* 系统开销  进程大
  * 创建或撤消进程时，操作系统所付出的开销将显著地大于在创建或撤消线程时的开销
* 通信
  * 同一进程中的多个线程具有相同的地址空间，致使它们之间的同步和通信的实现，也变得比较容易
  * 进程间通信，需要进程同步和互斥手段的辅助
* 调试
  * 进程简单可靠性高，线程编程调试相对复杂
### 进程间的通信方式
**管道**、系统IPC（包括**消息队列、信号量、信号、共享内存**等）、以及套接字socket
* 管道
  * 无名管道：可用于具有亲缘关系的父子进程间的通信
  * 有名管道：允许无亲缘关系进程间的通信
* 系统IPC
  * 消息队列
    * 消息不一定要以先进先出的次序读取,也可以按消息的类型读取
  * 信号量
    * 是一个计数器，可以用来控制多个进程对共享资源的访问
    * 用于实现进程间的互斥与同步，而不是用于存储进程间通信数据
  * 信号
    * 用于通知接收进程某个事件已经发生
  * 共享内存
    * 使得多个进程可以访问同一块内存空间
    * 需要依靠某种同步操作，如互斥锁和信号量
* 套接字socket
  * 可用于不同主机之间的进程通信
### 线程间的通信方式
* 临界区
  * 通过多线程的串行化来访问公共资源或一段代码
* 互斥量
  * 采用互斥对象机制，只有拥有互斥对象的线程才有访问公共资源的权限
  * 互斥对象只有一个，所以可以保证公共资源不会被多个线程同时访问
* 信号量
  * 允许多个线程在同一时刻去访问同一个资源
  * 一般需要限制同一时刻访问此资源的最大线程数目
* 事件
  * 通过通知操作的方式来保持多线程同步，还可以方便的实现多线程优先级的比较操作
### 多进程和多线程的使用场景
* 多进程：适用于CPU密集型，也适用于多机分布式场景中
* 多线程：适用于I/O密集型，也适用于单机多核分布式场景中

**<details><summary>进程状态转换图</summary>**
 
<div align=center><img src="https://github.com/FangChao1086/Interview/blob/master/依赖文件/操作系统_进程状态转换图.png"></div>

* 创建状态
  * 进程正在被创建
* 就绪状态
  * 进程被加入到就绪队列中等待CPU调度
* 执行状态
  * 进程正在运行
* 等待阻塞状态
  * 进程由于某种原因，比如等待 I/O ，等待设备， 而暂时不能运行
* 终止状态
  * 进程运行完毕 
</details>

## 互斥锁与读写锁
* **互斥锁（mutex）**
  * **任何时刻，都只能有一个线程访问该对象**
  * 当获取锁操作失败时，**线程会进入睡眠**，等待锁释放时被唤醒
* **读写锁（rwlock）**
  * 读锁 + 写锁
  * 读操作：**同一时刻，多个线程可获得读操作**
  * 写操作：**同一时刻，只能有一个线程可以获得写操作**；其他获取写操作失败的线程都会进入睡眠状态，直到写锁释放时被唤醒
  * 注意：
    * **写锁会阻塞其他读写锁**，当有一个线程获得写锁在写时，读锁也不能被其他线程获取；
    * **写着优先于读者**，一旦有写着，则后续读者必须等待，唤醒时优先考虑写着
### 互斥锁与读写锁的区别
* 读写锁分为读者与写者， 互斥锁不分
* 互斥锁同一时间只允许一个线程访问该对象；读写锁同一时间只允许一个写着，但是允许多个读者同时访问
### Linux的4种锁机制
* **互斥锁（mutex）**
* **读写锁（rwlock）**
* **自旋锁（spinlock）**
  * 任何时刻，都只能有一个线程访问该对象
  * 当获取锁操作失败时，**线程不会进入睡眠**，而是在原地自旋，直到锁释放
  * 适用于加锁时间短暂的环境下
* **RCU（read-copy-update）**
  * 在修改数据时，首先需要读取数据
  * 然后生成一个 copy 副本，对副本进行修改
  * 修改完成后，再将老数据 update 成新的数据
  * 适用于在大量读操作，少量写操作的情况
### 死锁产生的必要条件
1.互斥条件：一个资源每次只能被一个进程使用。
2.请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
3.不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
4.循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

## 内存溢出和内存泄漏
* **内存溢出**  程序申请内存时，没有足够的内存供申请者使用
  * 原因
    * 内存中加载的数据量过大
    * 代码中存在死循环
* **内存泄漏**  程序未能释放掉不再使用的内存，造成了内存的浪费
  * 原因
    * 堆内存泄漏
      * new/malloc 分配的内存没有使用 delete/free 释放
    * 系统资源泄漏
      * 程序使用系统分配的资源比如 Bitmap,handle ,SOCKET等没有使用相应的函数释放掉
    * 没有将基类的析构函数定义为虚函数
      * 当基类指针指向子类对象时，如果基类的析构函数不是virtual, 那么子类的析构函数不会被调用，子类资源不会被释放

<span id="计算机网络"></span>
# 计算机网络
* [OSI模型](#OSI模型)
* [TCP](#TCP)
  * [三次握手四次挥手](#三次握手四次挥手)
  * [TCP和UDP](#TCP和UDP)
* [HTTP和HTTPS](#HTTP和HTTPS)

## OSI模型
OSI 7层模型
* 物理层  IEE802.3 CLOCK RJ45
* 数据链路层  MAC VLAN PPP
* **网络层**  IP ARP ICMP
* **传输层**  TCP UDP
* 会话层  RPC NFS
* 表示层  JPEG ASII
* **应用层**  FTP HTTP DNS
  
### TCP/IP 4层模型
网络接口层：MAC VLAN  
网络层:IP ARP ICMP  
传输层:TCP UDP  
应用层:HTTP DNS SMTP  

## TCP
### TCP保证可靠性
* **序列号、确认应答、超时重传**
  * 数据到达接收方，接收方发出确认应答，确认序列号会说明下一个需要接受的数据序列号
  * 发送方迟迟没有收到应答，会等待一定时间后进行重传
* **窗口控制**与高速重发控制/快速重传
  * TCP利用窗口控制来提高传输效率，在一个窗口大小内不一定要等要应答才能发送下一段数据
  * 窗口大小就是无需等待确认而可以继续发送数据的最大值
  * 解释：
    * 使用窗口控制，如果数据段1001-2000丢失，后面数据每次传输，确认应答都会不停地发送序号为1001的应答，表示我要接收1001开始的数据，发送端如果收到3次相同应答，就会立刻进行重发；但还有种情况有可能是数据都收到了，但是有的应答丢失了，这种情况不会进行重发，因为发送端知道，如果是数据段丢失，接收端不会放过它的，会疯狂向它提醒......
* **拥塞控制**
  * 解决的问题：当把窗口定的很大，发送端连续发送大量的数据，可能会造成网络的拥堵
  * 慢启动
    * 定义拥塞窗口，一开始大小为1，之后每次收到确认应答，将拥塞窗口 *2；
  * 拥塞避免
    * 设置慢启动阈值，当达到阈值后，拥塞窗口变成加法增加（每次确认应答，拥塞窗口 +1）
  * 报文段超时重传
    * 一旦发生，需要先将阈值设为窗口大小的一半，并且将窗口大小设为初值1，然后进入慢启动
  * 快速重传
    * 接收方每次收到一个失序的报文段后就立即发出重复确认，发送方只要连续收到三个重复确认就立即重传
### 三次握手四次挥手
* 三次握手
  * C->SYN0->S
    * 客户端发送syn包(syn=x)到服务器，并进入SYN_SEND状态，等待服务器确认
  * S->SYN1,ACK(SYN0+1)>C
    * 服务器收到syn包，必须确认客户的syn(ack = x + 1), 同时自己也发送一个syn包（syn=y）,即SYN+ACK包，此时服务器进入SYN_RECV状态
  * C->ACK(SYN1+1)->S
    * 客户端收到服务器的 SYN + ACK 包，向服务器发送确认包ACK(ACK = y + 1),此包发送完毕，客户端和服务器进入 ESTABLISHED 状态
* 四次挥手
  * C->FIN->S
    * 主动关闭方，发送FIN，告诉被动方自己不会再发数据了
  * S->ACK->C
    * 被动方收到 FIN 包，发送 ACK (收到序列号 + 1)确认
  * S->FIN->C
    * 被动方发送一个 FIN 包，告诉主动方我也不会再给你发送数据了
  * C->ACK->S
    * 主动方收到 FIN 后，发送一个 ACK (收到序列号 + 1)给被动方，至此完成四次挥手
### TCP和UDP
* TCP:面向连接的可靠传输  传输慢
  * 场景：文件传输、重要状态的更新
* UDP:面向非连接的不可靠传输  传输快
  * 场景：视频传输、实时通信

## HTTP和HTTPS
* **HTTPS 优点**
  * **安全**，传输过程中使用密钥进行加密
  * **准确**，协议可以认证用户和服务器，确保数据发送到正确的用户和服务器
* **HTTPS 缺点**
  * **延时较高**，在进行HTTP会话之前还需要进行 SSL 握手
  * **部署成本较高**，协议需要使用证书来验证自身的安全性，需要购买CA证书；另一方面由于协议需要进行加解密计算，需要服务器配置数目高
### HTTP和HTTPS的不同
* HTTPS更安全；HTTP协议是以明文的方式在网络中传输数据，HTTPS传输的数据是经过 SSL 加密后的
* HTTP的端口80； HTTPS协议端口443；
### HTTP返回码
* 1xx：临时响应
* 2xx:成功
* 3xx:重定向
  * 301：永久重定向
  * 302：临时重定向
* 4xx:请求错误
  * 403：服务器拒绝请求
  * 404：服务器找不到请求的网页
* 5xx:服务器端错误
### HTTP请求/响应步骤
* 客户端连接到web服务器
* 发送HTTP请求
* 服务器接受请求并返回HTTP响应
* 释放连接TCP连接
* 客户端浏览器解析HTML内容

<span id="设计模式"><span>
# 设计模式
* 结构型模式
  * 装饰器模式
    * 允许向一个现有的对象添加新的功能，同时又不改变其结构
  * 代理模式
    * 一个类代表另一个类的功能
    * 意图：为其他对象提供一种代理以控制对这个对象的访问。
* 创建型模式
  * 单例模式
    * 单例类只能有一个实例，必须自己创建自己的唯一实例，必须给所有其他对象提供这一实例。
  * 工厂模式
    * 在创建对象时不会对客户端暴露创建逻辑，并且是通过使用一个共同的接口来指向新创建的对象
  * 抽象工厂模式
    * 接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。
* 行为型模式
  * 观察者模式
    * 当对象间存在一对多关系时，使用观察者模式（Observer Pattern）
    * 比如，当一个对象被修改时，则会自动通知它的依赖对象
