
<h1>8.18</h1>
- **String**
<ul>1.编码和解码，一个是str.getBytes(),另一个是new String(XX)指定参数</ul>
<ul>2.转码String value = new String(str.getBytes("ISO-8859-1"),"utf-8");</ul>
<ul>3.Stringbuffer的api和String 的差不多，最后toString就行</ul>
<ul>4.StringBuffer和StringBuilder好像都是方法链编程，也就是builder设计模式，每次方法执行，返回类本身，就可以一直链下去，比如buffer.append("liyang").append("hahahaah");</ul>
<ul>5.StringBuffer线程安全，StringBuilder不安全，所以后者效率率更高</ul>
<ul>6.一个贼重要的点，用  ==  来判断两个str的内存地址是否相同，两个不一样的对象，但是内容可以一样，所以判断内容，一般用的是equals()..........</ul>

- **线程安全同步**
<ul>1.非静态的方法，用自身类作为锁同步</ul>
<ul></ul>
<ul></ul>

- **基本类型（值类型）和包装类型（引用类型）**
<ul>1.比如int 就是值类型，默认0，Integer就是引用类型，默认mull</ul>
<ul>2.int 等值类型可以直接运算，而Integer不行，要经过自动拆箱，转成值类型，，，i.intValue()，，，，，，，</ul>

- **集合和数组**
<ul>1.数组只能存基本类型，ArrayList只能存对象，看似,list.put(100)，，这种添加的是int,但是实际上会自动封箱，变成Integer</ul>
<ul>2.List是size，，，数组和String才有length</ul>
<ul>3.因为List源码里面是用object[] 数组来存取的，所以读取很快，可以直接用index读取，但是add 的时候，会把后面的元素依次后移，性能很差</ul>
<ul>4.List为空的时候，返回[]，，，，，List不存在的时候，返回null</ul>
<ul>5.常用的三种集合，ArrayList,,HashSet,,HashMap，，都是线程不安全的</ul>
<ul>6.LinkedList，，链式集合，增删速度快</ul>
<ul>7.面向接口编程，像ArrayList这种，基本用List类型来实例化</ul>
<ul>8.因为Collection类中有iterable方法，所以下面的集合类都有迭代器方法 list.iterable().hasnext()，，，，，，，，，，而且返回的值是object,,,,,需要强转</ul><ul></ul>
<ul>9.想把List 去重，直接使用HashSet的构造方法，传入list就好</ul>
<ul>10.toString方法是object 超类提供的，可以进行重写</ul>
<ul>11.集合类有三种，List，，，Set，，，Hash，，，，</ul>



- **IDEA**
<ul>1.Ctrl 按住加点击，查看源码</ul>
<ul></ul>

- **明日目标**
<ul>1.java tostring重写</ul>


<h1>8.19</h1>
- **IO**
<ul>1.分成字节流和字符流，字节流主要基类InputStream和OutputStream，，，，，，，，字符流Reader和Writer</ul>
<ul>2.FileWriter writer = new FileWriter("test.txt");，，，，，，，，，类似这种的，没有文件会自己创建文件</ul>
<ul>3.对一个文件写操作，如果没有close()，内容就会一直放在内存里，源码中的close()，其实包含了flush()的操作，所以只要flush一下，也是可以写进文件的，否则写不进文件</ul>
<ul>4.new FileWriter(String filename,boolean append)，可以用参数true或者false来设置直接写入或者覆盖，默认是覆盖</ul>
<ul>5.read()之前要创建一个char[] ，，，长度就是缓冲区的长度，不宜太长，太耗费内存，也不宜太短，每次读取都冲刷掉原来的数据</ul>
<ul>6.缓冲区最后一次读取如果没有全部用尽缓冲区大小，会重复之前的读过的字符，所以在new String(buff,0,len)生成String的时候，定义好偏移量</ul>
<ul>7.读取的时候，必须保证文件存在，否则抛异常</ul>

- **明日目标**
<ul>1.java tostring重写（罪过罪过，居然拖了一天）</ul>



<h1>8.20</h1>
- **toString重写搞定**

- **BufferedWriter**
<ul>1.利用了装饰模式，和Writer相比，只是多了个缓冲区，减少了和流的交互，提高了效率</ul>
<ul>2.构造参数是一个Writer对象</ul>
<ul></ul>
<ul></ul>


- **杂项**
<ul>1.String line = System.getProperty("line.separator")</ul>
<ul>2.System.currentTimeMillis();</ul>
<ul>3.byte是字节，有8位，所以可以表示256个数，从-128~127，比如Byte(128)，就超过了127，所以就会变成-128，是一个轮回</ul>
<ul></ul>
<ul></ul>


<h1>8.21</h1>
- **装饰模式和builder模式**

- **杂项**
<ul>1.抛出异常和try-catch本质上有什么区别</ul>
<ul>2.utf8,gbk中文各占几个字节</ul>
<ul>3.NIO</ul>
<ul>4.文件归档</ul>
<ul></ul>

- **File类**
<ul>1.对于File对象来说，目录和文件是一样的，</ul>
<ul>2.常用api</ul>
<ul>3.做了个复制目录以及文件的demo</ul>






<h1>8.22</h1>
- **Thread类**
<ul>1.main函数，在执行的时候，是有两个线程的，一个是main主线程，另一个是垃圾回收线程，</ul>
<ul>2.常用api，，，sleep让线程处于阻塞状态，，，，，，yield出让cpu抢占权，让当前的运行中进程回到可运行的状态，但是还是有可能被选中，而且即使高优先的进程让出，低优先的还是不可能抢到，，，，，，，join，把一个线程相当于插队插进来，不等他结束，当前进程不会继续运行，，，，，，，</ul>
<ul>3.Thread类的方法：sleep(),yield()等 
   Object的方法：wait()和notify()等，sleep是阻塞该进程，让别的进程可以执行，但是并不释放锁，而wait会释放锁，当被notify()或者wait有时间参数时，返还锁</ul>
<ul>4.Thread.currentThread()来获取当前进程</ul>






<h1>8.23</h1>
- **多线程**
<ul>1.https://www.cnblogs.com/lemon-flm/p/7880119.html</ul>
<ul>2.线程工厂和ThreadLocal，，，，https://blog.csdn.net/evankaka/article/details/51705661，，，，线程工厂总的说，就是批量生产线程</ul>
<ul></ul>

- **线程安全**
<ul>1.Java 中i++ 和 ++i 都不是线程安全的，AtomicInteger类才是，有get()和getAndIncrement()等方法</ul>
<ul></ul>
<ul></ul>

- **内部类**
<ul>1.内部类，可以任意访问外部类的元素，不论是不是private,而且更改在外部类中是生效的</ul>
<ul>2.内部类是个编译时的概念，一旦编译成功后，它就与外围类属于两个完全不同的类（当然他们之间还是有联系的）。对于一个名为OuterClass的外围类和一个名为InnerClass的内部类，在编译成功后，会出现这样两个class文件：OuterClass.class和OuterClass$InnerClass.class。</ul>
<ul>3.第一：成员内部类中不能存在任何static的变量和方法；第二：成员内部类是依附于外围类的，所以只有先创建了外围类才能够创建内部类。第三，外部类要访问内部类，也要先实例化该内部类，不能因为是亲生的，就没有规矩</ul>
<ul>4.基于上条，每次得到内部类都要outClass.new InnerClass()，这样很麻烦，可以在外部类自身写好getInnerClass()方法，来返回内部类实例，return new InnerClass();</ul>


<h1>8.24</h1>
- **ThreadLocal（主要是下面的同一线程内共享数据，不同类和模块共享数据）**
<ul>1.ThreadLocal使用场景为 用来解决 数据库连接、Session管理</ul>
<ul>2.ThreadLocal给每个线程，都创建了一个数据副本，就是说，main方法中set，get一份数据，然后New Thread另起一个线程，同样set,get，数据是不一样的，而且互不干扰，这样的特点导致耗费内存</ul>
<ul>3.ThreadLocal中initValue方法，return想要的数据，可以让ThreadLocal不用总是先set ，，再get</ul>
<ul>4.本质上ThreadLocal不是用来解决多线程共享变量的</ul>
<ul></ul>

- **interrupt、interrupted 、isInterrupted**
<ul>1.interrupt没有返回值，单纯的中断线程，</ul>
<ul>2.interrupted，静态的，对当前运行的进程生效，就是说，代码逻辑在哪个线程，就对应的哪个线程，，返回boolean，并且如果原来是中断，则更改状态，变成不中断，原来中断的，不变化，也就是会改变状态，，源码  return currentThread().isInterrupted(true);</ul>
<ul>3.isInterrupted，，对线程对象对应的线程生效，就是说，可以在A线程中对B线程操作，，只返回状态，，不更改，，，</ul>
<ul>4.其实isInterrupted是可以有参数的，但是外部不可调用，是private,true表示会清除状态，false表示不会，在interrupted源码中有体现</ul>

- **线程组，ThreadGroup**
<ul>1.ThreadGroup构造方法，和Thread的构造方法</ul>
<ul>2.线程组主要是讲同一类的线程归为一组，方便批量操作，比如interrupt</ul>


- **线程间（不同线程）共享变量**
<ul>1.多个相同的方法，共享一个变量，一个Runnable里面有变量，也有run，里面写了对变量的操作，加上synchronized就好，将这个Runnable传入Thread做参数就好</ul>
<ul>2.不同操作方法共享变量，额外写一个类，里面封装变量和各种方法，方法加上synchronized，在每个Thread里面调用方法即可，因为synchronized实例方法以该实例对象作为锁，所以可以实现同步互斥</ul>

- **线程内（同一线程，不同代码）共享变量**
<ul>1.ThreadLocal同一线程，不同类get到的数据是一样的</ul>
<ul></ul>

- **疑问**
<ul>1.synchronized和lock的具体区别</ul>
<ul>2.lock的使用</ul>
<ul>3.有没有好的多线程框架？？好的并发框架？？</ul>
<ul>4.各种锁？？</ul>
<ul>5.那个知识图谱？？？？</ul>

- **书籍记下，以后看**
<ul>1.think in java</ul>
<ul>2.java并发编程</ul>
<ul>3.Effective Java</ul>

