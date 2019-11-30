---
title: Interview-Python
date: 2019-07-03 01:18:58
tags:
---
## 经典题目
1. Python的参数传递
所有的变量都是内存中一个对象的'引用', 可以理解为C语言中的void *

2. Python中的元类
具体的使用场景，在ORM中会使用它。

3. Python中的静态方法、类方法和实例方法

```
    class A(object):
        def foo(self, x):
            pass
        
        @classmethod
        def class_foo(cls, x):
            pass
            
        @staticmethod
        def static_foo(x):
            pass
```

4. 类变量和实例变量
类变量就是在所有实例之间共享的值。

```
    class Test(object):
        num_of_instance = 0
        def __init__(self, name):
            self.name = name
            Test.num_of_instance += 1
```
           
5. Python自省
面向对象语言在程序的运行过程中，可以知道对象的类型。type(), dir(), isinstance(), getattr(), hasattr()

6. 单下划线、双下划线
单下划线就是变量私有
双下划线，双下划线结束：Python的魔术对象，__init__(), __name__, 不能将这些名字用于自己的变量或者函数
双下划线，会被Name Mangling变更为_clsname__x,为了防止该成员与子类名称冲突。

9.迭代器和生成器
```
L = [x*x for x in range(10)] # 通过一个列表生成器直接生成一个列表
g = (x*x for x in range(10)) # 迭代器
``` 

10. *args 和 **kwargs
不确定参数将要传递多少个参数时，用*args
没有事先约定参数名的时候，用**kwargs
但是*args必须出现在**kwargs前面

```
def table_things(**kwargs):
    for name, value in kwargs.items():
        print '{0} = {1}'.format(name, value)
        
# 也可以用来解包
mylist = ['aaa', 'bbb', 'ccc']
print_three_thinds(*mylist)
```


11. 装饰器模式
装饰器的作用就是为了已经存在的对象添加额外的功能。
```
from functools import wraps

def makebold(fn):
    @wraps(fn)
    def wrapped(*args, **kwargs):
        return '<b>' + fn(*args, **kwargs) + '</b>'
    return wrapped
```

12. 鸭子类型
一只鸟走起来像鸭子，游泳像鸭子，叫起来像鸭子，那这只叫就可以被称为鸭子。
我们并不关心对象是什么类型、到底是不是鸭子、只是关心行为。
有很多file-like的东西，比如StringIO, GzipFile, socket,我们都可以把它当文件使用。
鸭子类型在动态语言中经常使用，非常灵活，使得python不像java一样去弄一大堆的专门设计模式。

13. Python为什么不支持函数重载
重载解决两个问题
    1.可变参数类型
    2.可变参数个数
情况1不需要处理，python可以接受任务类型参数。情况2，函数功能相同，但是参数个数不一样，答案就是缺省参数，对于那些缺少的参数设定为缺省值就可以解决问题。

14. 新旧类，Python3里面全是新式类，新式类继承是C3算法，旧式类是深度优先。
旧式类从左到右，深度优先的。会导致C重写的foo1()被绕过
```
class A():
    def foo1(self):
        print "A"
class B(A):
    def foo2(self):
        pass
class C(A):
    def foo1(self):
        print "C"
class D(B, C):
    pass

d = D()
d.foo1()
```

15. __new__和__init__的区别
- __new__是一个静态方法，__init__是一个实例方法
- __new__返回一个创建的实例，__init__一般用于初始化，什么也不返回
- 只有__new__返回一个cls的实例后，__init__才能被调用

ps: __metaclass__是在创建类时起作用，可以用__metaclass__ __new__ __init__在创建类、实例、初始化的时候做一些小动作

16. 单例模式
```
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            orgi = super(Singleton, cls)
            cls._instance = orig.__new__(cls, *args, **kwargs)
            return cls._instance

class Borg(object):
    _state = {}
    def __new__(cls, *args, **kwargs):
        ob = super(Borg, cls).__new__(cls, *arg, **kw)
        ob.__dict__ = cls._state
        return ob
        
def singleton(cls):
    instances = {}
    def getinstance(*args, **kw):
        if cls not in instances:
            instances[cls] = cls(*args, **kw)
         return instances[cls]
    return getinstance
         
@singleton
class MyClass:

```            


18. GIL
线程全局锁(Global Interpreter Lock),即Python为了保证线程安全而采取的独立线程运行的限制。对于io密集型任务，python的多线程起到作用，但对于cpu密集型任务，python的多线程几乎占不到任何优势，还有可能因为争夺资源而变慢。


19. 协程
简单点说协程是进程和线程的升级版,进程和线程都面临着内核态和用户态的切换问题而耗费许多切换时间,而协程就是用户自己控制切换的时机,不再需要陷入系统的内核态

22. 函数式编程
```
a = [1, 2, 3, 4, 5, 6]
b = filter(lambda x: x > 5, a)
print b

b = map(lambda x:x*x, a)

reduce(lambda x,y: x*y, range(1,4))
```

23. copy() deepcopy()
a = [1, 2, 3, 4, ['a', 'b']]

b = a # 赋值，传递对象引用
c = copy.copy(a) # 对象拷贝，浅拷贝
d = copy.deepcopy(a) # 对象拷贝，深拷贝

浅拷贝只拷贝了第一层对象，子可变对象没有进行深拷贝
深拷贝会递归到子可变对象里面
```
import copy
a = [1, 2, 3, 4, ['a', 'b']]  #原始对象

b = a  #赋值，传对象的引用
c = copy.copy(a)  #对象拷贝，浅拷贝
d = copy.deepcopy(a)  #对象拷贝，深拷贝

a.append(5)  #修改对象a
a[4].append('c')  #修改对象a中的['a', 'b']数组对象

print 'a = ', a
print 'b = ', b
print 'c = ', c
print 'd = ', d

输出结果：
a =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
b =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
c =  [1, 2, 3, 4, ['a', 'b', 'c']]
d =  [1, 2, 3, 4, ['a', 'b']]
```


26. is
is 是对比地址，== 是对比数值

27. read, readline, readlines
read读取整个文件
readline读取下一行，使用生成器
readlinese读取整个文件到一个迭代器供我们遍历

28. Python2和3的主要区别
print()变成了函数
str都是unicode了，多了byte类型
Handling exceptions,需要使用as
整除, 在python2里面 3/2=1但是，python3中3/2=1.5

29. super int


30. range和xrange
xrange()的性能更好，range()生成的是一个列表，range(100)在内存中生成0-99的数字，xrange()生成的是一个生成器，
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
            
            
## OS 
1. select poll epoll
- 打开的文件描述符数量有限制，epoll只跟系统内存有关系，select, poll有限制，默认1024,当然可以修改以后，重新编译OS内核。
- 但是select poll是轮训所有的fd, 有数据就处理，却又就跳过，所以把fd改大了，效率就下降了。epoll只处理就绪的常fd, 它有一个就绪的队列，每次只查询该队列的数据，然后处理。另外select、poll需要把数据从内核态拷贝到用户态，但是epoll使用了mmap的机制省略了这个步骤。

## apache和nginx的区别
nginx的优点：
    - 轻量级，占用的比apache更少的内存和资源
    - 抗并发，支持更多的并发连接，nginx是异步非阻塞的，apache是阻塞的，高并发下nginx能保持低资源低消耗高性能。

apache的优点：
    - rewrite比nginx的强大
    - 模块多，
    - 少bug
    
# MySQL存储引擎 MyISAM与InnoDB的区别
1. 事务支撑，MyISAM不提供事务>
2. 表锁的差异，MyISAM只支持表级锁，select, update, delete, insert 语句都会给表自动加锁。InnoDB支持行级锁，提高了多用户并发性。但是InnoD的行锁，只有在Where中有主键才生效。
3. MyISAM不支持外键


# MVCC 多版本并发控制
innodb为每个行添加两个在字段，分别表示创建的版本和删除的版本。填入事务的版本号。
insert 将新行的版本号设置为当前系统版本号
delete 将删除版本号设置为当前版本号
update 转化为insert + delete
select 需要满足select行创建的版本号小于当前版本号，并且delete版本号为空，或者大于当前版本号。实现了repeated read的隔离级别。但是要想seriallizable还是必须加锁。
 insert、delete、update执行时，需要将系统版本号递增。
 但是旧数据并不真正的删除，必须堆这些数据进行清理，innodb会开启一个后台进程进行清理工作，将版本号小于系统当前版本号的行进行删除。
 
 
 Storm构建一个Topology，分成了4层，spout读取kafka数据一层使用shuffle发给二层bolt格式化数据，然后fieldshuffle发给二层做去冲，最后在shufflegrouping给到最后一个节点。
 
 
Nimbus: 主控节点，用于提交任务、分配任务、集群监控等。
zk: 集群集中协调，共有数据存放（心跳、集群状态），Nimbus将分配给supervisor的任务写到ZK.
supervisor:负责接受nimbus分配的任务，管理属于自己的worker进程。


# reduceByKey 和 groupByKey的区别是什么？
reduceByKey是对每个key的value进行函数自定义函数进行merge,它可以现在本地就先merge。

groupByKey是对每个key生成一个sequence,那么也就是说reduceByKey等于groupByKey+map操作。在很多key-value对的情况下，reduceByKey优于groupByKey

