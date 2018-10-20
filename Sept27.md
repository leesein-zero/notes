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
<ul>2.主码，外码，，主码就是主键，外码就是另外表的主键ul>
<ul>3.各种数据类型的定义和特点</ul>
<ul>4.书里讲的很多都是sql 通用的语法，在MySQL 里面，很多都行不通，比如 schema ,在MySQL 里面大致相当于 database</ul>


<h1>10.20</h1>
<ul>1.使用设计模式的时候，当遇到一个超类不能照顾到所有子类，就可以创建相关属性的接口，使用这些接口的实现类，来整合属性行为，，，，，就和controller 里面调用 service一样，在controller里面定义接口类型，不同的是，这里没有spring 注入的概念，只能自己来做实现，，一般是在该子类的构造方法里来 new </ul>
<ul>2.上面的话总的来讲，就是超类定义 接口变量，并定义方法来使用接口，，，，，，而子类在构造方法中具体实现接口</ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>








<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>