<h1>9.28</h1>
<ul>1.spring-social不能导入，我怀疑是聚合工程里的那个控制版本的东西搞的鬼，我另一个项目里面就可以直接用</ul>
<ul>2.不要过分相信pom.xml里的版本控制，这次加了版本号就OK了</ul>
<ul>3.maven项目版本控制，依赖版本控制</ul>

<h1>9.29</h1>
<ul>1.StringUtils一般用的是commands包里面的</ul>

<h1>10.1</h1>

- **遇到的难处**
<ul>1.验证码点击刷新搞定，但是刷新之后 session中保存的值好像没换</ul>
<ul>2.验证码验证失败之后的反馈没做好</ul>
<ul>3.接下来就是验证码重构</ul>
<ul></ul>
<ul></ul>
<ul></ul>

<ul>1.spring-security的项目做起来，那些分模块的，我把他放在一个模块里了，用不同包表示</ul>
<ul>2.验证码刷新的时候，用的是jquery，但是security把静态url拦截了，要设置过</ul>
<ul>3.刚才出现了一个很大的麻烦，验证码在后台一直得不到验证，，，经过debug之后，发现是后面的 "post".equals(request.getMethod())，，，，小写的post 应该改成大写，这样就没事了</ul>

- **外包**
<ul>1.淘宝卖家中心的数据，在卖家中心是拿不到的，但是他是由另一个api提供数据支持，去那里就可以抓到，，，，，，，，，说明智者千虑必有一失，有时候需要转个脑筋想一下</ul>
<ul>2.太烦，懒得做</ul>
<ul></ul>
<ul></ul>


<h1>10.4</h1>
<ul>1.Linux有时候新创建的用户不能使用sudo，，https://blog.csdn.net/sinat_36118270/article/details/62899093</ul>
<ul>2.更好用的ls -Al</ul>
<ul>3./etc/environment中修改环境变量。结果我配错了，基本所有命令都不能用了，还好export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin</ul>
<ul>4.开机直接启动文字界面</ul>
<ul>5.更改主机名，，ubuntu和centos还不一样</ul>
<ul>6.用hosts构建主机名和ip地址的映射</ul>
<ul>7.vi 的具体操作</ul>

- **总结**
<ul>1.今天把大体环境弄好了，明天把ssh弄好</ul>

- **深夜收获**
<ul>1.使用ls -al更好</ul>
<ul>2.~ 目录下有.ssh目录，用来存放用户的ssh密钥，，sshkeygen -t rsa -P '' -f ~/.ssh/id_rsa</ul>
<ul>3.把公钥加到公钥库，也就是authorized_keys里面</ul>

<h1>10.5</h1>
<ul>1.把昨天的公钥放进库中，但是登录localhost还是需要密码，，，看这篇文章http://www.mamicode.com/info-detail-2128504.html，，，，，，，主要是权限问题，用户目录和.ssh是700，，authorized_keys是600</ul>
<ul>2.nc 是一个传输工具</ul>
<ul>3.centos的yum install 要用sudo</ul>
<ul>4.ssh 整好之后，就是用start-all.sh脚本，开启hadoop配置，如果遇到pemission not allowed，，就可以chmod 777 xxx，，，</ul>
<ul>5.Nodemanager不能开启，https://blog.csdn.net/icebergwang/article/details/22992069，，，按照网页中修改yarn-site.xml即可</ul>


<h1>10.7</h1>
<ul>1.8020是hadoop的端口，50070是hadoop weib UI的端口，可以可视化查看hadoop状态，，，，data node 50075,,,,,2nn 50090</ul>
<ul>2.linux sudo halt关机别忘了</ul>
<ul>3.我本来以为我五台机器的ssh公钥要重新分发，结果因为我是克隆的，所以生成的公钥是一样的authorized_keys也是一样的，配好hosts就可以直接登录</ul>
<ul>4.把用户目录下的ssh文件夹复制到root，，就可以实现root的远程登录</ul>
<ul>5.vi 的一些简单的命令，，比如粘贴 ,是非insert下的 p ，，复制当前一行是非insert的 yy</ul>
<ul>6.centos的 /etc/sysconfig/network 中更改主机名</ul>
<ul>7. cp 命令复制一个文件夹的时候，带 -R ，可以复制文件夹和它下面的文件</ul>
<ul>8. rsync 和 scp 命令</ul>
<ul>9. linux中有三个bin ，，首先是 /etc/bin ，这个是linux系统自带的 bin 目录，，还有个 /usr/bin，，这个是出厂自带的 bin ，最后是我们自己可以写脚本的 /usr/local/bin ，，同样也在PATH 中，可以直接使用，写命令不一定要 sh 文件，也可以没有后缀，别忘了 chmod a+x，，让所有权限可以执行</ul>
<ul></ul>
<ul>10.https://blog.csdn.net/xiashan17/article/details/52599065/</ul>
<ul>11.吸取一个教训，linux脚本之类的，比如 x=5,,不能写成 x = 5，，中间不能有空格，，，并且以后用nano更加方便</ul>


<h1>10.8</h1>
<ul>1.照着敲了一个rsync的群发脚本，，，里面有不少shell 语言的注意点，在s136里面</ul>
<ul>2.xsync和xcall完工</ul>
<ul>3.按照配置，把 NN 和 resourceManager 放在一台主机上，另找三台放 dataNode ,并且把副本数变成3，，，，并在hdfs中，把SecondaryNameNode放在 s140上，，，，实际上做了这么多，就是把单机版的伪分布式，任务分到各个机子，变成真正的分布式</ul>
<ul>4.在windows上，50070访问不到，明天再解决</ul>

<h1>10.9</h1>
<ul>1.昨天50070外部浏览器不能访问，今天 xcall reboot，，然后 关闭防火墙，就搞定了</ul>
<ul>2.有时候datanode起不开，，这时候删除 /tmp/hadoop-username 就可以了，，并且format</ul>
<ul>3.徐培成的多线程下载</ul>
<ul>4.core-site里配置hadoop.tmp.dir=你想要的，，本来不设置，默认是在/tmp/下创建hadoop-xxx 目录的，，现在更改过了，，记住啊，以后再出现 datanode 没有起开的情况，需要清除缓存，就要清除自己配的本地目录了</ul>
<ul>5.需要着重了解下 datanode的本地存放情况，，和 block 的分块情况，，</ul>
<ul></ul>


<h1>10.10</h1>
<ul>1.hadoop-daemon.sh 后面start namenode 这类命令可以单独启动和停止进程</ul>
<ul>2.hadoop-daemon.sh 和Hadoop-daemons.sh </ul>
<ul>3.助手git</ul>
<ul>4.![](https://i.imgur.com/l4hKEr9.png)</ul>

<h1>10.11</h1>
<ul>1.pycharm连接远程git仓库，，push被拒绝，应该是远程仓库有一个readme.md，本地没有，会冲突，这时候应该先拉到本地，再进行提交，，，，，，，我这里直接用的git命令行，而且 git push -u origin master -f 直接强制push</ul>
<ul>2. git remote add origin xxxx.git</ul>
<ul>3.输入输出流有点淡忘，还有JAVA 的 URL对象 和 UrlConnection</ul>
<ul>4.抽象类和接口的优缺点和区别</ul>
<ul>5.hadoop api 的 read,write,还有conf配置的具体读写，还有block块的读取和下载，拼接</ul>
<ul></ul>
<ul></ul>

<h1>10.12</h1>
<ul>1.IDEA查看函数返回值，函数说明</ul>
<ul>2.hadoop 的 api，，</ul>
<ul>3.python 直接把一个字符串变成一串bytes,,,但是字符串中有 
 \ 这么一个转义的字符，encode或者 bytes()函数都会变成 \\ ，，所以最后用了 eval() ，里面是 'b\''+code+'\''</ul>
<ul>还有urllib.parse ，这个包很神奇，马天波居然成功了，明天看看你</ul>

<h1>10.13</h1>
- 现在定下每日目标
<ul>1.每天100个深蹲</ul>
<ul>2.每天做每日总结</ul>
<ul>3.每天背墨墨记单词</ul>

- hadoop 
<ul>1.block的概念，hadoop2.7分成128M一块，目的是 让磁盘寻道时间占用数据传输的1%</ul>
<ul>2.namenode的多目录，是用来做副本，，，datanode的多目录是存在不同地方而已，没有副本概念，因为datanode 之间本身就有副本概念</ul>
<ul>3.hadoop for IDEA  https://blog.csdn.net/fyzLucky2015/article/details/77170440，，，，然后是IDEA 安装插件，，https://blog.csdn.net/qq_35246620/article/details/78289074?locationNum=6&fps=1</ul>
<ul>4.我觉得hadoop 的 hdfs 差不多了。不需要特别精通，，，我觉得可以直接开始 yarn 和 mapreduce</ul>


<h1>10.14</h1>
<ul>1.main 的 args 有啥用</ul>
<ul></ul>
<ul></ul>



<h1>10.15</h1>
<ul>1.调用 api 来上传文件到 hdfs ，权限不够可以创建 permisson（具体咋做），，但是这个hadoop插件怎么做的</ul>
<ul>2.Integer.MIN_VALUE？？？？？？</ul>


<h1>10.16</h1>
<ul>1.找到一个不错的python 工具类</ul>
<ul>2.找到了这个作者没有注意到的地方，怎么在github上面协同啊</ul>
<ul>3.开始写，另外没啥，client有Bug，发送一次login 是正常的，紧接着再发一条，就会发生阻塞，我怀疑是start函数一开始的接收是阻塞的，可以尝试新开一个线程</ul>
<ul>4.具体看看新开一个线程</ul>
<ul>5.那个mysql.connector 咋回事，和pymysql 有啥区别，，还有封装新的工具类怎么做的，研究一下人家写的工具类</ul>
<ul>6.数据库的电子书，看到内外模式了</ul>


<h1>10.17</h1>
<ul>1.hadoop 在win下运行，需要hadoop.dll,winutils.exe,已经解决，运行成功</ul>
<ul>2.现在可以这样做，client维护一个接收的消息队列，单开两个线程，一个发送，一个接收，接收的消息放在接收队列中，while true检测队列长度，有值就打印或者处理，用 type字段来标识数据，，，，，，，，下面是服务器端，也是用字段标识吧。来处理发来的消息是群发还是单发，同时维护一个在线用户列表，，可以通过api拉取，，接收是一个线程，发送应该也可以是一个线程</ul>
<ul>3.一直有这种情况，发送一次login 请求之后，返回错误值，然后再次发送login ,这时候实际上并没有发送成功，但是并不报错，原来是我写成tcp了，换成udp的就好了，但是为什么会这样恩</ul>

- 实验课作业
<ul>1.完成度一点点上升，后面的难度不大，有几点容易有bug</ul>
<ul>2.多个客户端登录同一个账号，服务端应该有个去重机制，判断是不是已经有了，就可以解决后面的广播发到同一用户两次</ul>
<ul>3.怎么做到和cookie差不多的意思，有登录时限</ul>
<ul>4.注册好像还没写</ul>
<ul>5.参数缺失的expection</ul>
<ul>6.输入了无效的命令怎么办</ul>
<ul>7.暂时想到这些</ul>


<h1>10.18</h1>
<ul>1.实验做好了，那个hadoop的小demo 也早就完成了，应该继续hadoop学习了</ul>

- hadoop 概念
<ul>1.job : 一个完整的 Map Reduce 过程</ul>
<ul>2.task : 比如说就是一个 Map 过程，就是一个 Map task</ul>

<h1>10.19</h1>
<ul>1.数据库的 模式，基本表，索引，视图的概念？？</ul>
<ul>2.主码，外码，，主码就是主键，外码就是另外表的主键</ul>
<ul>3.各种数据类型的定义和特点</ul>
<ul>4.书里讲的很多都是sql 通用的语法，在MySQL 里面，很多都行不通，比如 schema ,在MySQL 里面大致相当于 database</ul>


<h1>10.20</h1>

<ul>1.sqlalchemy 封装工具类   https://blog.csdn.net/qq_17612199/article/details/75945102</ul>
<ul>2.想做一个二进制转换，或者bytes转换的模块，上传到pypi上</ul>
<ul>3.上课想到后台高并发，以后项目面试可能会被问到</ul>

- **设计模式**
<ul>1.使用设计模式的时候，当遇到一个超类不能照顾到所有子类，就可以创建相关属性的接口，使用这些接口的实现类，来整合属性行为，，，，，就和controller 里面调用 service一样，在controller里面定义接口类型，不同的是，这里没有spring 注入的概念，只能自己来做实现，，一般是在该子类的构造方法里来 new </ul>
<ul>2.上面的话总的来讲，就是超类定义 接口变量，并定义方法来使用接口，，，，，，而子类在构造方法中具体实现接口</ul>
<ul>3.单例模式？？好像数据库封装类可以用到</ul>

- **sqlalchemy**
<ul>1.创建DB连接</ul>
<ul>2.generate code sqlacodegen</ul>

- **自我梳理**
<ul>自我感觉学了很多东西，但是要真的拿出来讲讲，大部分都不能很好的精通，接下来开始好好梳理</ul>
<ul>1.python ，这方面好像花的时间是很多的，爬虫，爬虫框架，挺熟练，还有算法，和机器学习的一些库，，最后还有很多的python的底层细节，，具体说欠缺，也是有，比如scrapy我就快忘得差不多了，还有如果要面算法岗，我算法方面真的还有很大的不足，，所以这方面，我需要捡起从前的爬虫，和恶补算法，数据结构，最后是python的具体语法</ul>
<ul>2.Linux 用的倒也算熟练，但是对于shell的语法还不是很会，要到那种能随便写脚本做自己事情的程度才行，所以linux 欠缺 shell </ul>
<ul>3.Java ，这个用的时间远远不如 python 但是进展比想象中要快，现在能写一些挺简单的后台，另外，，，好像真的没啥，，，欠缺的太多了，还差 java 的 hadoop 使用，和更高深的后台</ul>
<ul>4. 前端 ，，，一直停留在，，改代码的阶段，，简单的jquery还是会的</ul>
<ul>5.就是上次闲着没事去面试，真的要阐述自己的项目的时候，才觉得差的有点多，，我可以写自己有写后台的经验，杭助的后台可以写上去，但这样就要真的去了解公众号后台的很多细节，不然被问到就很尴尬，还有导师合作网站的后台，这些算是真实项目，，还可以说，有分布式爬虫的经验，这个到没有吹牛，不过最好能搞成，做过搜索引擎的那种，，。关于hadoop ，，最好毕设就是推荐系统这种东西，涉及协同过滤，不要求我能搞成那种算法工程师，但是最好是那种，能实现的大数据工程师</ul>

- **写了这么多，对自己的要求**
<ul>1.能拿出一点真正的项目，吹的也算，但不能露馅</ul>
<ul>2.对一些东西有源码级的理解，比如说原理啥的，spring啊，都可以</ul>
<ul>3.面试题目要开始看起来了，比如leecode</ul>
<ul>4.java基础和python 基础，总不能到时候基础面试都过不了</ul>
<ul>5.爬虫就差不多，机器学习还是吃算法，，hadoop就要看实操，比如推荐系统，，后台就看高并发，架构，还有很多框架之类，，前端放弃，，数据库看优化和原理，，，Linux 就shell ，，，</ul>
<ul>6.python 做一个模块上传到pypi吧，目前看起来做一个字符串的bytes2str更好，把编码也考虑进去</ul>
<ul>7.对了云计算，openstack是个啥？？？</ul>
<ul>8.英语！！！！！！！！！</ul>
<ul>9.大型搜索引擎，推荐系统，广告系统</ul>
<ul></ul>


<h1>10.21</h1>
<ul>1.想去阿里的话，还应该有用过他们的平台和产品</ul>
<ul>2.java.net.URL</ul>
<ul>3.intputstream 是读取数据，outputstream 是写数据进去</ul>
<ul>4.从一个@Before 的注解中，我突然想起我的spring 并不是很懂，只是会使用而已，对于底层真的垃圾</ul>
<ul>5.JUnit4 的注解详情  https://www.cnblogs.com/565261641-fzh/p/6081004.html</ul>
<ul>6.正则</ul>
<ul>7.可不可以做一个关于正则的模块</ul>
<ul>8.策略模式</ul>

- **hadoop**
<ul>1.HDFS是一个相对底层的文件系统，在此基础上可以跑简单的 mapreduce程序，，Hbase则是在HDFS基础上的键值对存储模型，，而YARN是资源调度框架，能让不是mapreduce的程序，也可以跑在hadoop 上</ul>
<ul>2.solr搜索平台可以跑在hadoop上，，这个方向可以做一下，主要是海量数据的查询和检索</ul>
<ul>3.hadoop和普通关系数据库之间的区别，就是减少了磁盘寻道时间，，，这一部分也体现在 HDFS 的 块的大小</ul>
<ul>4.namenode 就是那种命名空间，存在数据块的信息和索引之类的，提供容错机制，，，而datanode 是具体的存放数据的，，，，，，最后还有个辅助namenode，，定期整合namenode 的数据，而且单独开一个主机，因为占用较大内存，在namenode挂掉之后，，会暂时充当主namenode</ul>
<ul>5.联邦HDFS???是可拓展的HDFS的意思吗，，书里说，比如一个namenode负责/usr,,,另一个负责/local</ul>
<ul>6.namenode单点失效的时候，等待辅助结点很慢，所以引入活动-备用namenode 的配置</ul>
<ul>7. HDFS 中的目录会作为元数据，存在namenode中，而不是 datanode</ul>
<ul>8.new Progressable()通过重写这个，可以实现回调，一般可以用来实现，百分比进度之类的东西。</ul>
<ul>9.hadoop 的 IOUtils ，，里面还有个 copybytes，可以通过Bytes来复制</ul>



<h1>10.22</h1>
<ul>1.观察者模式，一个对象的改变，会有其他对象紧跟着做出反应</ul>
<ul>2.python 的 struct 模块</ul>
<ul>3.hadoop 命令行可以通过 -conf 后跟 hhhhhhh.xml 来选择不同的 xml 来选择不同的 模式，，，，但我这边是直接重写了 core-site.xml 这种，，有点麻烦</ul>


<h1>10.23</h1>
<ul>1.python 的 del函数</ul>
<ul>2.既然以后要吹杭助项目，那就要熟悉微信公众号开发</ul>
<ul>3.整一个单机版的hadoop,平时测试用，已经弄好  </ul>

<h1>10.25</h1>
<ul>1.IOUtils 真的挺好用，而且注意下读操作是输入流，写是输出流</ul>
<ul>2.HDFS 权限怎么搞，代码里有身份这么一说吧</ul>
<ul>3.hadoop权威指南在看</ul>


<h1>10.26</h1>
- **MRUnit的那些坑**
<ul>1.maven里面不能导入，，要记得加hadoop 的版本号</ul>
<ul>2.问题都在里头 https://blog.csdn.net/Xiblade/article/details/80559683</ul>

- **hadoop权威指南**
<ul>1.知道一个新的点，job.setCombinerClass </ul>
<ul>2.出现两个问题，第一个，本地IDEA可以跑在远程的mapreduce程序，达成 jar包就不可以在远程跑，一直报WARN hdfs.DFSClient: Caught exception ，，这是一个，另一个是，每次在远程跑一遍程序，hdfs里面就会生成很多 /temp 临时文件，怎么更改</ul>
<ul>3.  https://blog.csdn.net/dai451954706/article/details/50464036  不知道有没有用，先写上</ul>
<ul>.hadoop学习路线 https://blog.csdn.net/sinat_38648491/article/details/79032396</ul>
<ul>4.各种实战项目 https://www.oschina.net/news/73199/full-stack-engineer-growth-ideabook</ul>
<ul>5.一个结合hadoop 的实战项目 https://www.cnblogs.com/DarrenChan/p/6640983.html</ul>
<ul></ul>




<h1>10.27</h1>
- **hadoop之坑**
<ul>1.win下可以运行的程序，打成jar放在伪分布式跑，就会卡在一个地方，我按照方法，增加了虚拟机的内存，处理器，磁盘，都没用，还更改了yarn-site.xml，还是没用，重启了两次，也没用</ul>
<ul>2.ip:8088的 yarn 管理界面打不开，配置了yarn-site.xml就好了</ul>
<ul>3.把capacity-scheduler.xml 里的yarn.scheduler.capacity.maximum-am-resource-percent 调到0.9了都不行，，我下次试试集群版的</ul>
<ul>4.那以后就在win下跑了吧，我尝试过在win下跑mapreduce，但是远程的yarn里面没有记录，说明是在本地跑的，但是最后上传到远程 hdfs了，应该是这样的</ul>
<ul>5.经测试，不修改的集群，也跑不动</ul>

- **杂项**
<ul>1.hduhelper用户的仓库中有万能查询，学工部接口等等，可以用来吹项目</ul>
<ul></ul>


<h1>10.28</h1>
- **hadoop**
<ul>1.回答一下昨天的问题，在win下跑mapreduce，在远程yarn管理界面没有，是因为win的真的是在win本地跑的，结果上传而已，想要真的在远程跑，而在win下调试，需要专门配置，具体查看徐培成第9天</ul>
<ul>2.算是于心不甘吧，还在这折腾昨天的跑不起来的问题，想到了会不会需要配置调优，结果试了下，还是不行，，，资料 https://blog.csdn.net/WYpersist/article/details/80699372，，，，，主要是mapred.default.xml</ul>
<ul>3.顺便又多了解了一下 ，nano的用法，挺好用的，，，，https://www.cnblogs.com/nufangrensheng/p/3486018.html</ul>
<ul>4.又搞了半天，发现自己yarn.scheduler.capacity.maximum-am-resource-percent 配错了，应该是几十几十的代表百分比，但是我该成百分百也不行，疯了，应该是机器配置太差的原因，随缘吧</ul>
<ul></ul>
<ul></ul>
<ul></ul>
- **杂项**
<ul>1.Java 的 netty</ul>
<ul>2.Ngrok</ul>
<ul>3.明天正式开始微信开发，主要是为了可以吹杭助的真实的上线项目，这个应该不会花太久时间，等这个过去继续hadoop，然后就差不多可以实习了，就可以准备基础和复习操作系统和计网之类的，还有算法导论</ul>
<ul></ul>


<h1>10.29</h1>
<ul>1.到现在才明白，原来在win下使用hadoop，是需要你自己配置 xml的，就比如，我之前配了 core-site.xml ，指定了hdfs的地址，所以真正运行，就用的是远程的hdfs ，和本地的yarn </ul>
<ul>2.是真的，把mapred-site拿下来，就会在远程跑</ul>
<ul>3.win下的 yarn 管理界面打不开</ul>
<ul>4.用 natapp 就把内外网打通了，因为是免费用户，域名是随机分配，不利于微信开发，要么花钱每个月9块，要么直接用ngrok 的一个开源软件</ul>
<ul>5.想起来我的博客应该要部署上去，，看了一下，spring boot项目打成jar包，拿上去 jar 运行就可以了</ul>
<ul></ul>
<ul></ul>


<h1>10.30</h1>
<ul>1.内网穿透终于搞定了一个免费的，，https://github.com/Wisdom-Projects/holer，，，打扰了，要money</ul>
<ul>2.最终版，真正的免费，，https://www.wezoz.com/</ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>








<h1></h1>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>