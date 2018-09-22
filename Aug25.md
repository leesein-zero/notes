<h1>8.25</h1>
- **springboot开张了**
<ul>1.不再去很纠结并发编程，现阶段用不到，等到大三下左右，去看java并发编程，应该才会有收获，现在用处不大</ul>
<ul>2.springboot的main函数，如果不自己配置扫描的话，系统只会默认扫描那个main函数所在包下的文件，应该加上比如@ComponentScan("com.liyang.controller")，，，@ComponentScan这个注解</ul>
<ul>3.在写controller的时候，和原来一样，也是@Controller,@RequestMapping("/index")这类，但可以用@RestController来简化，相当于Controller和ResponseBody</ul>




<h1>8.26</h1>
- **疑问**
<ul>1.SOA架构是啥</ul>
<ul>2restful风格怎么体现</ul>
<ul></ul>
<ul></ul>

- **springboot**
<ul>1.这里的html映射不太懂，不知道怎么查看他的view拦截器，后来是依赖了spring-boot-starter-thymeleaf，网页后缀是html，直接return成功的</ul>
<ul>2.thead,tbody,td等等标签的使用</ul>

- **权限控制**
<ul>1.隐式控制，把访问对象和用户身份相关联，导致耦合度高，要改很多地方</ul>
<ul>2.显式控制，把对象和相应权限关联，耦合度低，可以对一个访问的用户进行权限的灵活变更</ul>
<ul>3.两个框架，apache shiro和spring security</ul>
<ul>4.应该不止两个框架，还有其他的方法来验证，比如我之前做过的项目里的验证，和那个springboot系列文章里的验证方法</ul>
<ul></ul>

- **技术选型**
<ul>1.权限验证，有上述的</ul>
<ul>2.数据库，有JPA，有Mybatis</ul>
<ul>3.渲染模板，有thymeleaf，有freemarker</ul>
<ul></ul>
<ul></ul>





<h1>8.27</h1>
- **心得和疑问**
<ul>1.总算找到一个靠谱的项目，一个博客项目，不过有些东西我自己来改动，不需要完全一样</ul>
<ul>2.终于搞定了用IDEA clone github的项目，保持项目结构完整</ul>
<ul>3.该项目用了一些stringutils,jsonuitls.好像不是自己写的，是自带的，我去看看以前项目里的，那个Json我去看看fastjson的那个</ul>
<ul>4.前端还是不愿意自己写，抄吧</ul>


<h1>8.29</h1>
- **springboot**
<ul>1.一直有一个mapper无法注入的问题，后来解决了，发现application.properties里面，有一个mybatis.configuration.cache-enabled=true，这样设置会导致问题，，而且当@Mapper这个注释没有的时候，可以引入import org.apache.ibatis.annotations.*;</ul>
<ul>2.模板渲染到底怎么搞啊（终于搞定一点基本的东西，把原来的都用thymeleaf 重写）</ul>
<ul>3.有一个点，poji类里面，id设为Integer类型，在为空的时候，就会报nullpoint的错，这是因为Integer默认为Null，改成int 就好了</ul>


<h1>8.30</h1>
- **博客项目继续**
<ul>1.很多时候，在注入的时候，@Autowired不行，需要用@Resource</ul>
<ul>2.加了拦截器之后，老是redict到 /in 的问题，终于解决，有两个bug ,第一个，是获取不到User类的主键 ID,所以在mapper.xml的insert方法里加上配置，，，，，第二个，就是粗心了，根据ticket的userid查询User,这里逻辑错了，现已纠正</ul>
<ul>3.现在用的是Spring拦截器进行访问权限验证，还可以用AOP，和spring security</ul>
<ul>4.create页面在首页右上角那个加号，请求代码在header.html里</ul>


<h1>9.1</h1>
<ul>1.@RequestParam("title")String title ，这个注释是为了绑定html中的id到变量上</ul>
<ul>2.一个页面需要传值的变量太多咋办，有啥方法</ul>
<ul>3.pagehelper有时候会出现版本冲突，更换最新版一般就好了</ul>
<ul>4.时间格式化，${#dates.format(discusser.creatAt, 'yyyy-MM-dd')}</ul>
<ul>5.用两个方括号包起来，，，，[[${custUser.nickname}]]，，和 th:text="${custUser.nickname}" ，，，一模一样，这叫行内表达式</ul>
<ul>6.突然想起，有的pojo类要注释@Compent，有的注入对象要注释@Resource或者@Autowired，有啥区别</ul>
<ul></ul>
- **分页显示和文章显示成功**
<ul>1.文章显示本来以为很难的，结果查询之后返回的list,放在model里面即可，但是我到现在还没分清thymeleaf 里面 *{} 和 ${} 的区别</ul>
<ul>2.分页就难多了，首先是导入依赖。两种方法，导入原始依赖和导入springboot封装过的，具体讲解 https://blog.csdn.net/csdn_huzeliang/article/details/79350425</ul>
<ul>3.分页的跳转是个难题，比如说我现在是第一页，想要到第二页怎么办，，，，我是这样解决的，，写一个隐形的input ，里面传一个pageNum的值，用来设置页数，然后用一个js函数，相应的链接就是需要跳转的页数。</ul>
<ul>4.href标签调用js函数，但是传进去的值，不能用thymeleaf解析，不能变成后台传过来的值，我也想不懂咋办，但是好在js代码里面，申明过 th:inline+"javascript"，之后，就可以在js代码里面用 行内表达式 ，算是解决了</ul>
<ul>5.Html的特殊字符 http://www.mamicode.com/info-detail-1251831.html</ul>
<ul>6.spring拦截器怎么同时拦截多个不同的网址，我现在是这么解决的 addPathPatterns(new ArrayList<String>(){{add("/"); add("/index");}})，，， 里面可以设置一个List类型的参数，我不知道怎么更加优雅，只能这样写</ul>



<h1>9.2</h1>
<ul>1.在html模板中使用thymeleaf，有两个情况比较尴尬，第一个，，js函数的参数，，，第二个href，跳转的网址，，，，，第一个在script>中直接使用，第二个可以改用th:href="@{xxxxxxxxxxxx}"</ul>
<ul>2.时间要精确到秒，那么new date()怎么使用</ul>


<h1>9.3</h1>
<ul>1.bug待修复，Tag标签后台是用英文逗号分来的，但是有时候用户是用中文逗号的，这样就分不开，，，，，而且思考下，能不能用选择的方式，来选择tag标签</ul>
<ul>2.现在的用户权限，是我在数据库自己改成admin的，，怎么搞成注册的时候，就确定好用户权限呢</ul>
<ul>3.想要两个表产生关系，除了用外键，还可以用第三张表，来规定他们的关系</ul>
<ul>4.有一个需求，在一个由article组成的list里面，给article增加新的字段，一开始打算更改pojo类，但是这样会同时改变数据库里的字段，不可取。后来自己创了个pojo类，来重新封装，在html中使用会标红，但是可以使用
</ul>
- **近期要做的事情**
<ul>1.海报</ul>
<ul>2.比赛算法</ul>
<ul>3.博客相关的bug和自己的想法</ul>
<ul></ul>
<ul></ul>



<h1>9.4</h1>
<ul>1.给这个博客项目加上事务安全</ul>

- **疑问总结**
<ul>1.redirect和直接return 某jsp的区别？？？</ul>
<ul>2.热启动和复制到目录下自动添加jar包？？</ul>
<ul>3.了解下增量爬取策略</ul>
<ul>4.数据校验</ul>
<ul>5.抛出异常和try-catch本质上有什么区别</ul>
<ul>6.NIO</ul>
<ul>7.utf8,gbk中文各占几个字节</ul>
<ul>8.有没有好的多线程框架？？好的并发框架？？</ul>
<ul>9.各种锁？</ul>
<ul>10.SOA架构是啥</ul>
<ul>11.restful风格怎么体现</ul>
<ul>12有的pojo类要注释@Compent，有的注入对象要注释@Resource或者@Autowired，有啥区别
有的pojo类要注释@Compent，有的注入对象要注释@Resource或者@Autowired，有啥区别
.时间要精确到秒，那么new date()怎么使用</ul>

<h1>9.5</h1>
- **springboot 参数校验**
<ul>1.要引入hibernate-validator，先要引入springboot JPA</ul>
<ul>2.pojo类增加注解，比如 @Pattern()</ul>
<ul>3.controller网页传参增加@Valid </ul>
<ul>4.增加BindingResult bindingResult</ul>
<ul>5.心得，html传到后台的参数，只要name 和 pojo 字段一样，controller就可以用这个pojo 来接收</ul>

- **前端页面优化**
<ul>1.fontawesome是为bootstrap设计的图标样式，只要class="fa fa-xxx",就可以使用，前提是导入相关css</ul>

- **updateByExample**
<ul>1.这个方法有两个参数，第一个是pojo的实例对象，第二个是example</ul>
<ul>2.原来我一直都错了，以前我是先通过example找到要修改的那一条，然后再用这个找到的对象去updateByExample，然后会报错，，真正的应该是重新New 一个对象，对要修改的部分set 修改，另外不改动，会默认Null，，，这样才不会报错</ul>

- **拦截器和controller之间传递数据**
<ul>这里是写了一pojo 来传递存取数据，，用@Component 来申请扫描</ul>
<ul>2.为了保证线程间数据安全，用ThreadLocal，，，，，需求临时要获取ticket 字段，本来是在pojo中增加字段，，，但是这样并不保证线程安全</ul>
<ul>3.最后在ThreadLocal 中 hashmap，，每个线程单独维护一个hashmap，，存放ticket 和 user</ul>

<h1>9.7</h1>
- **springboot 事务配置**
<ul>1.在service中的相关方法上加@Transactional，，，在启动类上加@EnableTransactionManagement，，，，是spring-tx.jar哦</ul>
<ul>2.@Transactional注解一般只加在增删改上</ul>

<h1>9.9</h1>
- **redis**
<ul>1.今天突然发现redis远程连不上了，重启下就好，，用的是kill -9 pid，，，，，，那个 systemctl restart redis 没用</ul>
<ul>2.适合做排行榜之类，听说是redis 的 zset比较合适，里面有好几个字段，key,score,member，，第一个是键名，第二个得分，第三个变量名吧，相当于，，，，我找了很久，也没有找到直接获取score值的api......我觉得，，排名和具体的值，可以用redis 的两个不同数据结构做，一个是List，一个zset</ul>
<ul>3.Redis zset具体 API很多，随便贴一个，，https://blog.csdn.net/u013372487/article/details/51485047</ul>

- **杂项**
<ul>1.getContextPath等等的作用，，，，，https://www.cnblogs.com/keyi/p/6232658.html</ul>
<ul>2.String.valueOf  可以把很多其他类型的，转成String</ul>
<ul></ul>

- **项目进程**
<ul>1.redis排行榜和阅读量做到一半</ul>
<ul>2.spark单机版已经完成，可以尝试跑算法</ul>

<h1>9.10</h1>
- **redis**
<ul>1.阅读量和排行榜分开存储，一个用hash，，一个用zset</ul>
<ul>2.Integer.parseInt，，，把其他格式变成 int </ul>
<ul>3.把api都封装在jedisService里，功能已经实现，，，，，，，，现在有一个BUG，，，拦截器是拦截了 /article/** 这样的url，然后进行统计的，，但是如果故意输错，弄成 /article/xxx  乱七八糟的字符，还是会存进redis，，我觉得这里应该有验证的功能</ul>
<ul></ul>
<ul></ul>





<h1>9.13</h1>
<ul>1.今天的话，做好api</ul>
<ul>2.spring security 和 spring cloud</ul>

- **做api**
<ul>1.flask 返回json数据，可以直接返回 json.dumps()，，，也可以用jsonify({xxxxxxxxxxxxx})</ul>
<ul>2.request.get_data()和request.json()都可以获得前端json</ul>
<ul>3.部署，，第一个问题是开启虚拟环境，source /flask_demo/env/bin/activate，，，，这样就是开启了，，，然后uwsgi ii.ini开启uwsgi服务，具体可以更改配置文件，，，，，，最后就是nginx的配置，可以find . nginx.conf，，，还有sites-available里的default文件，可以配置，，，，，这样就可以了</ul>

- **杂项**
<ul>1.vim 直接跳转到最后一行 shift + G</ul>
<ul>2.postman初探
账号是我qq和密码</ul>

<h1>9.14</h1>
<ul>1.flask token验证</ul>
<ul>2.JWT token验证</ul>
<ul></ul>
<ul></ul>


<h1>9.18</h1>
- **restful特点**
<ul>1.用url表示资源，而不是表现用途，比如/user/delete 这种就不行</ul>
<ul>2.不只是使用get,post，，，而是把四种method都使用，比如delete,put</ul>
<ul>3.传统的返回的状态码只有404,200，但是restful活用更多状态码</ul>
<ul>4.传输数据，使用JSon</ul>
<ul>5.具体讲解http://www.cnblogs.com/wang-yaz/p/9237981.html</ul>
- **security**
<ul>1.那个logging的模块</ul>
<ul>2.测试模块</ul>
<ul>3.使用userdetails好像可以返回数据对象，，里面可以设置权限啥的</ul>

<h1>9.19</h1>
- **security**
<ul>1.逻辑，在config里面的http参数方法中，设置权限和验证方式，比如formlogin，，，在auth参数方法中，引入UserDetailsService和PasswordEncoder接口的概念和使用，UserDetailsService是接口，要先实现，这里主要是进行数据库操作和返回userdetails类型的对象，，顺便赋予权限，，，然后经过PasswordEncoder进行加解密，，，具体数据操作用UserDetails 接口实现</ul>
<ul>2.新版本的security需要passwordEncoder</ul>

- **背单词**


<h1>9.20</h1>
<ul>1.在自定义loginPage的时候，发现输入信息之后不能跳转验证，原来是form表单中没有 method="post"</ul>

- **security**
<ul>1.实现目标，使用restful传递json的思想，后缀不是html的请求，就401返回，是html，就重定向到自定义验证页面。</ul>
<ul>2.实现可重用功能，通过设置properties，来重用，封装类来读取properties</ul>
<ul>3.各种api查看代码</ul>
<ul>4.controller中，返回html的话，就用string，，，返回json就用@ResponseBody</ul>

<h1>9.22</h1>
<ul>1.spring-security差不多搞定</ul>
<ul>2.下载了几套UI模板，而且收藏了网址</ul>

- **近期目标**
<ul>1.spring-security大概已经弄清楚一些了，可以尝试做一个基于security的模块，跟着B站视频就行</ul>
<ul>2.基本的简单的后台开发已经差不多了，权限验证和安全啥的，看完上面那个也差不多了，还差评论功能，点赞。</ul>
<ul>3.再有就是，有个全文搜索的功能，搭集群之类的</ul>
<ul>4.JVM调优，，bootstrap,分布式学习</ul>
<ul>5.阶段再后面一些，开始java基础</ul>

- **博客评论功能开发和纠错**
<ul>1.updateByExample更新的使用自身好像也是可以的</ul>
<ul>2.redis的排行榜突然出了问题，先注释掉</ul>
<ul>3.Comment表的content字段返回时Null ,非常费解，我一路debug,发现CommentExample里面没有content有关的方法，但是有其他属性的方法，我就去数据库里面查看，发现content的属性是text而不是varchar，，改回来之后重新逆向工程，顺利解决</ul>
<ul>4.每个评论之间加了css的分割线https://blog.csdn.net/LucasLi2016/article/details/55095849</ul>
<ul>4.在显示评论内容和username的时候，有个问题，comment和user是不同的pojo,所以需要整合到一块，我这里用了重新封装的item类</ul>
<ul>5.评论功能大致完成，但是有缺陷，首先没有回复评论功能，然后发送评论后，系统重新跳转到当前页面，但是此时回退，不能直接回到Index,而是重新回到当前界面，所以我一开始的跳转就是有缺陷的，，，最后，Index 页面的排行榜功能有Bug，未修复</ul>
<ul>6.？？？我是不是能用ajax来做评论提交？？这样就搞定了那个跳转</ul>
<ul>7.排行榜注释放开了，因为我redis数据清空，bug就消失了</ul>

- **思考**
<ul>1.程序的异常处理，spring boot 有没有专门的异常处理器</ul>
<ul>2.现在的拦截器真的蠢，可以试试spring-security重构</ul>
<ul>3.提交数据之后刷新当前页面，用redirect太蠢了，直接用ajax完美解决</ul>
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








<h1></h1>
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
<ul></ul>
<ul></ul>
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








<h1></h1>
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
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>
<ul></ul>