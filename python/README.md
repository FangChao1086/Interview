<span id="re_"></span>
# python

[参考链接：python知识点详细](https://github.com/taizilongxu/interview_python#20-%E9%97%AD%E5%8C%85)   

* [python3新特性](#python3新特性)
* [基础知识](#基础知识)
* [变量的作用域](#变量的作用域)
* [dict按value排序](#dict按value排序)
* [.format的用法](#.format的用法)
* [np.mat()与np.array()的区别](#np.mat()与np.array()的区别)
* [\*args与\*\*kwargs的区别](#args与kwargs的区别)
* [re.match与re.search的区别](#re.match与re.search的区别)
* [extend与append的区别](#extend与append的区别)
* [浅拷贝与深拷贝](#浅拷贝与深拷贝)
* [迭代器和生成器](#迭代器和生成器)
* [装饰器](#装饰器)
* [进程与线程](#进程与线程)
* [拍照功能](#拍照功能)
* [日期处理datetime](#日期处理datetime)
* [生成可执行文件.exe](#生成可执行文件.exe)
* [python彩蛋](#python彩蛋)

<span id="python3新特性"></span>
## [python3新特性](#re_)
* pathlib模块
* 格式化字符串变量
* 统一编码支持中文字符
* Python 3.5 将支持 Async/Await 异步编程

<span id="基础知识"></span>
## [基础知识](#re_)

* <details><summary>输入数据相关代码</summary>
    
    ![1.png](https://github.com/FangChao1086/Coding_language/blob/master/依赖文件/1.PNG)  
    ```py
    M, N = list(map(int, input().split(',')))

    book = []
    for i in range(M):
        line = list(map(int, input().split(',')))
        book.append(line)
    ```
    ---
    ![2.png](https://github.com/FangChao1086/Coding_language/blob/master/依赖文件/2.PNG)
    ```py
    # 输入处理
    m = int(input())

    tmp = []
    for _ in range(m):
        line = [list(map(int, item.split(','))) for item in input().split(';')]
        tmp.extend(line)  # 
    ```
    ---
    ![3.png](https://github.com/FangChao1086/Coding_language/blob/master/依赖文件/3.PNG)
    ```py
    # 输入处理
    n = int(input())
    x, y = [], []
    for i in range(n):
        _x, _y = list(map(int, input().split()))
        x.append(_x)
        y.append(_y)
    ```
</details>

* 自动补0  
```python
# 字符串
n = '123'
s = n.zfill(5)

# int
n = 123
s = "%05d" % n

'''
'00123'
'''
```
### 基本操作
* 赋值
```py
# 同步赋值
# a=a+b,b=a同时进行，运算时使用原始值
a, b = 1, 2
a, b = a + b, a
print("a = ", a)
print("b = ", b)

"""
a =  3
b =  1
"""
```
* 列表
```py
# 元素反向
list_test = [1, 2, 3, 4, 5]
print("列表元素顺序反向：" + str(list_test[-1::-1]))
# 元素替换
list_test[0:2] = [9, 8]
print("替换后的列表为：" + str(list_test))
# 开头插入元素
list_test[:0] = [7, 6]
print("插入后的列表为：" + str(list_test))

"""
列表元素顺序反向：[5, 4, 3, 2, 1]
替换后的列表为：[9, 8, 3, 4, 5]
插入后的列表为：[7, 6, 9, 8, 3, 4, 5]
"""
```
* 推导式
```py
# 普通推导式
list_test = [pow(i, 2) for i in range(1, 11)]
print("生成平方数（1-10）：", list_test)

# 二维推导式
list_test0 = {j for i in range(2, 20) for j in range(i * i, 20, i)}
print("2-19所有的合数", list_test0)
list_test1 = [i for i in range(2, 20) if i not in list_test0]
print("2-19所有的质数", list_test1)

"""
生成平方数（1-10）： [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
2-19所有的合数 {4, 6, 8, 9, 10, 12, 14, 15, 16, 18}
2-19所有的质数 [2, 3, 5, 7, 11, 13, 17, 19]
"""
```
* 字典实现模糊查找
```py
# 字典实现模糊查找
dict = {'mr.zhang': '46317', 'miss.wang': '64717', 'cheng': '46397'}
while (True):
    str_name = input("输入要查找人姓名开头字符（可模糊查找）：")
    for k, v in dict.items():
        if k.startswith(str_name):
            print(k + ':' + v)
    i = input("是否继续进行查找(y/n):")
    if i == 'n':
        break


"""
输入要查找人姓名开头字符（可模糊查找）：M
是否继续进行查找(y/n):m
输入要查找人姓名开头字符（可模糊查找）：mr
mr.zhang:46317
是否继续进行查找(y/n):y
输入要查找人姓名开头字符（可模糊查找）：m
mr.zhang:46317
miss.wang:64717
是否继续进行查找(y/n):n

"""
```

## [变量的作用域](#re_)
* 全局变量
  * 在函数体外定义的变量
* 局部变量
  * 在函数体内部定义的变量
* **作用域**
  * **全局变量在所有作用域都可读**
  * **局部变量只能在本函数可读**
  * 优先读取函数本身有的局部变量，再去读全局变量
  * 函数体内要想对全局变量进行修改，需要在函数体内先用全局关键字global定义
  
```python
'''
author:fangchao
date:2019/6/10

content: 变量的作用域
'''
# 全局变量
balance = 1


def change():
    # 定义全局变量
    global balance
    balance = 100
    # 定义局部变量
    num = 20
    print("change() balance={0}".format(balance))


if __name__ == "__main__":
    change()
    print("修改后的 balance={0}".format(balance))

'''
change() balance=100
修改后的 balance=100

# 如果注释掉change()函数里的 global
change() balance=100
修改后的 balance=1
'''
```

<span id="dict按value排序"></span>
## [dict按value排序](#re_)
```python
# 按照value从大到小排序:
sorted(d.items(), key = lambda x:x[1], reverse = True)

# 按照value从小到大排序:
sorted(d.items(), key = lambda x:x[1], reverse =False)
```

<span id=".format的用法"></span>
## [.format的用法](#re_)
```python
d = 'a: {}, b: {}'.format(23, 34)
print(d)

'''
a: 23, b: 34
'''
```

<span id="np.mat()与np.array()的区别"></span>
## [np.mat()与np.array()的区别](#re_)
* np.mat()
  * 矩阵相乘：\* 或者 np.dot()
  * 点乘：np.multiply()
* np.array()
  * 矩阵相乘：np.dot()
  * 点乘：\* 或者 np.multiply()

<span id="args与kwargs的区别"></span>
## [\*args与\*\*kwargs的区别](#re_) 
[参考链接：\*args与\*\*kwargs的区别](https://www.cnblogs.com/yunguoxiaoqiao/p/7626992.html)
* \*args：将关键字参数打包成**tuple**给函数体使用  
* \*\*kwargs：将关键字参数打包成**dict**给函数体使用  

<span id="re.match与re.search的区别"></span>
## [re.match与re.search的区别](#re_)
[参考链接：re.match与re.search的区别](http://www.runoob.com/python3/python3-reg-expressions.html)  
* re.match：从字符串的起始位置匹配，起始位置匹配不成功就返回None
* re.search：对整个字符串进行匹配

<span id="extend与append的区别"></span>
## [extend与append的区别](#re_)
[extend与append的区别](https://www.cnblogs.com/tzuxung/p/5706245.html)   
* extend：只能接收list，把list中的每个元素添加到原list中
* append：接收任意数据类型的参数，直接全部加到list尾部

<span id="浅拷贝与深拷贝"></span>
## [浅拷贝与深拷贝](#re_)
[参考链接：浅拷贝与深拷贝](https://www.cnblogs.com/xueli/p/4952063.html)  
* copy浅拷贝：没有拷贝子对象，原始数据改变，子对象也会跟着改变
* deepcopy深拷贝：拷贝子对象，原始数据改变，子对象不会改变

<span id="迭代器和生成器"></span>
## [迭代器和生成器](#re_)
[参考链接：迭代器和生成器](http://www.runoob.com/python3/python3-iterator-generator.html)  
* 迭代器：一个可以记住遍历的位置的对象。
  * 基本方法：iter() 和 next()  
* 生成器：一个返回迭代器的函数，只能用于迭代操作
  1. 运行时，每次遇到**yield**时函数会暂停并保存当前所有的运行信息，返回 yield 的值
  2. 在下一次执行next()方法时从当前位置继续运行。
* 生成器的优点：
  * 省空间
  * 响应快

## [装饰器](#re_)
[参考链接:装饰器](https://www.runoob.com/w3cnote/python-func-decorators.html)
* 概念：修改其他函数功能的函数
* 简单装饰器
  ```python
  def use_logging(func):
    def wrapper():
        logging.warn("%s is running" % func.__name__)
        return func()   # 把 foo 当做参数传递进来时，执行func()就相当于执行foo()
    return wrapper

  def foo():
      print('i am foo')
      
  foo = use_logging(foo)  # foo没有加括号表示未执行，可以传递，可以传给给变量，也可以作为参数传递；因为装饰器 use_logging(foo) 返回的是函数对象 wrapper，这条语句相当于foo = wrapper
  foo()                   # 执行foo()就相当于执行 wrapper()
  ```
* 简化
  ```python
  def use_logging(func):
    def wrapper():
        logging.warn("%s is running" % func.__name__)
        return func()
    return wrapper

  @use_logging
  def foo():
      print("i am foo")
  # 省去foo = use_logging(foo)
  foo()
  
  """
  WARNING:root:foo is running
  i am foo
  """
  ```
* 带参数的装饰器
  ```python
  def use_logging(level):
    def decorator(func):
        def wrapper(*args, **kwargs):
            if level == "warn":
                logging.warn("%s is running" % func.__name__)
            elif level == "info":
                logging.info("%s is running" % func.__name__)
            return func(*args)
        return wrapper
    return decorator

  @use_logging(level="warn")
  def foo(name='foo'):
      print("i am %s" % name)

  foo()
  ```
* 问题：失去了原函数的元信息，比如__name__
* 解决方法
  ```python
  from functools import wraps
  def logged(func):
      @wraps(func)
      def with_logging(*args, **kwargs):
          print func.__name__      # 输出 'f'
          print func.__doc__       # 输出 'does some math'
          return func(*args, **kwargs)
      return with_logging

  @logged
  def f(x):
     """does some math"""
     return x + x * x
  ```

## [进程与线程](#re_)
### 线程
* **守护线程**
  * 运行前提：主线程必须存在，不存在时守护线程就会被销毁
* **多线程的锁机制**
  * 多进程之间对内存中的变量不会产生冲突
  * **多个线程对内存中的共享变量同时进行操作时会产生影响，产生死锁（线程安全问题，需要加锁解决，对数据进行锁定）**
    * 示例，两个线程：t1,t2；t1对全局变量a进行加100任务，t2对全局变量a进行减100任务；当线程t1、t2同时修改全局变量a时，循环次数够多时，a的值就会出现变化
    * ```python
      '''
      author:fangchao
      date:2019/6/10

      content:线程死锁
      '''
      import threading

      balance = 100


      def change(num, counter):
          global balance
          for i in range(counter):
              balance += num
              balance -= num
              if balance != 100:
                  # 如果输出这句话，说明线程不安全
                  print("balance=%d" % balance)
                  break


      if __name__ == "__main__":
          thr1 = threading.Thread(target=change, args=(100, 500000), name='t1')
          thr2 = threading.Thread(target=change, args=(100, 500000), name='t2')
          thr1.start()
          thr2.start()
          thr1.join()
          thr2.join()
          print("{0} 线程结束".format(threading.current_thread().getName()))

      '''
      balance=200
      MainThread 线程结束
      '''
      ```
* 死锁的解决方案：**互斥锁**
  * 在某个线程需要更改共享数据时，先将其资源锁定，直到该线程释放资源时，其他线程才能对其进行更改
  * 核心代码
    * ```python
      # 创建锁
      mutex = threading.Lock()
      # 锁定
      mutex.acquire()
      # 释放
      mutex.release()
      ```
  * 示例
    * ```python
      '''
      author:fangchao
      date:2019/6/10

      content:互斥锁
      '''
      import threading

      balance = 100
      lock = threading.Lock()  # 创建锁


      def change(num, counter):
          global balance
          for i in range(counter):
              # 先要获取锁
              lock.acquire()
              balance += num
              balance -= num

              # 释放锁
              lock.release()

              if balance != 100:
                  # 如果输出这句话，说明线程不安全
                  print("balance=%d" % balance)
                  break


      if __name__ == "__main__":
          thr1 = threading.Thread(target=change, args=(100, 500000), name='t1')
          thr2 = threading.Thread(target=change, args=(100, 500000), name='t2')
          thr1.start()
          thr2.start()
          thr1.join()
          thr2.join()
          print("{0} 线程结束".format(threading.current_thread().getName()))

      '''
      MainThread 线程结束
      '''
      ```
      
### 多进程与多线程的区别
* **进程：系统进行资源调度和分配的基本单位；线程：CPU进行调度和分配的基本单位**
* **线程容易通信，切换灵活；**
* 一个程序至少有一个进程，一个进程至少有一个线程
* 进程在执行过程中拥有独立的内存单元，但多个线程共享内存
* 线程不能够独立的执行，需要依存在应用程序中

## [拍照功能](#re_)
* 显示画面，按S拍照，按空格退出
```python
'''
author:fangchao
date:2019/6/11

content:拍照功能
'''
import cv2

# 0:笔记本摄像头  1：外置摄像头
cap = cv2.VideoCapture(0)
i = 0

while (True):
    ret, frame = cap.read()
    if ret:
        cv2.imshow('capture', frame)
    k = cv2.waitKey(1)  # 等待1ms
    if k == ord(' '):
        break
    if k == ord('s'):
        cv2.imwrite('capture_' + str(i) + '.jpg', frame)
        i = i + 1

cap.release()  # 关闭视频捕获器
cv2.destroyAllWindows()  # 关闭所有窗口
```

<span id="日期处理datetime"></span>
## [日期处理datetime](#re_)
```python
# 时间差
import datetime as dt

date_received = '20120301'
d = '20120305'
this_gap = (
        dt.datetime(int(d[0:4]), int(d[4:6]), int(d[6:8])) -
        dt.datetime(int(date_received[0:4]), int(date_received[4:6]), int(date_received[6:8]))).days
print('时间差this_gap:', this_gap)
```

<span id="生成可执行文件.exe"></span>
## [生成可执行文件.exe](#re_)
* 依赖pyinstaller  
`pip install pyinstaller`
* **生成可执行文件命令**  
  * 一般打包：`pyinstaller -F xx.py`  
  * 加密打包：`pyinstaller.exe -F --key 123456 xx.py` key后面的密钥可以随便输
  * `-F`表示生成单个可执行文件  
* 结果
  * 在终端命令行路径中出现xx.spec文件（成功打包时，还会有dist文件夹）
  * **可执行文件.exe在dist文件夹中**
<details><summary>可能出现的问题</summary>
 
`RecursionError: maximum recursion depth exceeded`
  * 解决步骤1，在xx.spec文件中添加如下代码,并保存  
  ```python
  import sys
  sys.setrecursionlimit(1000000)
  ```
  * 解决步骤2，在终端执行以下命令  
  `pyinstaller -F xx.spec`
  </details>
  
<span id="python彩蛋"></span>
## [python彩蛋](#re_)
```python
'''
author:fangchao
date:2019/6/4

content:python彩蛋
'''

# 彩蛋一
import __hello__
'''
Hello world!
'''

# 彩蛋二
import this
'''
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
'''

# 彩蛋三
import antigravity
'''
$输出反重力图像$
'''
```
