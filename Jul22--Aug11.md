<h1>7.22</h1>

- 一个web project先看 web.xml ,在这里配置 dispatcher 和监听器
-  dispatcher指向dispatcher-servlet.xml，里面找映射的视图监听器listener,指向多个 xml,分别是dao ,service,tx,controller等,要分别进行扫描
- mybatis反向工程 由数据库生成domain 
- 还有一个点，example的查询，模糊查询，准确查询等等
- @AuteWird 自动注入
- controller里面  寻找视图，有点麻烦，明天再弄





<h1>7.23</h1>

- 很傻逼的一个点，目录本来是 web 到 WEB-INF ，我在WEB-INF里面添加了css等文件夹。所以才不能显示，现在拿出来了
- 我发现springmvc.xml 根本没有配置进去，一点用都没，全部注释了（后来才知道，原来**那个springmvc.xml其实就是前端控制器的配置，就是dispatcher-servlet.xml**）
- 天啦噜，springmvc项目里是没有 servlet相关包的，还要我自己来导入
- jstl包也要自己导入 
- jstl的使用,redirect重定向
- controller类的方法返回 ModelandView 一般是没错的，当要用到重定位的时候，返回string ，参数传入model，就可以了
- 使用pagehelper ,要先导jar包
- 实践分页时的教训<br>
1.pagehelper的jar包不能和mybatis jar包的版本差太多，会报错<br>
2.这个东西在controller中，先弄一个拦截器
PageHelper.startPage(pageNumber,pageSize)，
然后PageInfo pageInfo = new PageInfo<>(list); 
把得到的list对象放进去
model.addAttribute("pageinfo",pageInfo);最后加在作用域里面，方便页面的各种方法的使用，比如获取下一页什么的${pageinfo.nextPage}

3.mybatis的配置文件里加点东西

4.有一个挺重要的controller类的方法里传参设置默认值，用@RequestParam(value = "pageNumber",required = false,defaultValue = "1") ，还必须紧跟着对应的值(但是value要和传过来的值的name一样)


<h1>7.24</h1>

- 针对不同用户的不同显示，用if语句捕捉用户的权限
- 这次的权限设置，和前面的获取${AllAuction} 不太一样，这个是存在model里的。而${sessionScope.get('user').userisadmin==1} 是放在sessionScope里的，不一样
- 现在做出来的东西，不需要登录，直接输入对应网址，也可以进入首页，这样就没有userisadmin,没有user,可能后面会解决吧
        

<h1>7.25</h1>
- **组合查询1/2**
<ul>1.首先jsp表单的部分需要修改，每一项的name值对应 controller 接收到的Auction 的参数，不用怎么特殊设置，字段名字一样，就能传值</ul>
	
<ul>2.controller 部分不用怎么改，主要修改 serviceimpl ,对相关条件进行查询和排序，主要是criteria 的操作和Example.setOrderByClause("auctionstartprice desc") 这种需要注意下</ul>

<ul>3.细节方面,比如 double类型和Double类型是不一样的，一个是值类型，默认是0，一个是引用类型，默认是null</ul>

<ul>4.时间方面引入了WebCalendar.js ，我js不是很懂，以后再说</ul>

- **另一个组合查询1/2**
<ul>1.有一个点终于弄明白了,那个springmvc.xml其实就是前端控制器的配置，就是dispatcher-servlet.xml</ul>
<ul>2.没有加时间转换器的时候，为什么报错？？是因为那个时间的框里面返回的是Sring，不是后台对象需要的Date类型，需要一个转换器</ul>

<ul>3.加了转换器之后页面不出400了，但是单独的模糊查询有问题，会显示所有商品，这个被发现是！的原因，没有加！的时候，第一个名字的criteria添加了查询，但是第二个描述没有填，所以进去了if，加了一个查询所有的东西，所以就变成查询所有了？？？这个会覆盖的？？？</ul>
<ul>4.后台报时间为""，无法parse的错，说明即使时间没有填，还是传了空的字符串值，不是null</ul>

<ul>5.@ModelAttribute("condition") Auction condition这样的参数定义和  model.addAttribute("condition",condition)这样的代码是等效的，并且在jsp页面里加上value，就可以解决数据回显</ul>

<ul>6.数据查询之后，在进行下一页的时候，无法带着查询的条件跳转，还是会回到查询全部的状态，在这里，点击下一页的时候，利用js解决。<br>
input id="page" name="pageNumber" type="hidden" value="1"
 document.getElementById("page").value=pageNumber;
 document.getElementById("form_query").submit();<br>
最关键这三句，第一个写在form里，用来给页面传页号，第二个设置页号，第三个相当于带着条件在提交一次，前提是数据回显
</ul>
<ul>7.使用了上面的分页查询之后，本质上是页面并没有跳转，只是后台返回的数据变了而已，pageHelper自己在后台就把数据分页好了</ul>
<ul>8.由此引出三种传值方式，url传值，表单传值，ajax传值，上面的例子就是从url传值变成了表单传值，而且java后台都能接收，只要name一致</ul>


- **文件上传**
<ul>1.导jar包commons-fileupload-1.3.1.jar和commons-io-1.3.2.jar </ul>
<ul>2.页面表单 enctype="multipart/form-data"</ul>
<ul>3.一个点，js的location跳转可以直接写web目录下的jsp名称，也可以用controller接收返回jsp,是一样的</ul>

<ul>4.报了不能自动注入bean的错误，导入了aspectjweaver-1.8.4.jar就好了</ul>
<ul>5.xml里面加上文件上传的配置</ul>
<ul>6.MultipartFile pic的使用piv.transferTo(File),参数是file对象，可以自己new ,在controller最后redirect:/AllAuction</ul>
<ul>7.redirect和直接return 某jsp的区别？？？</ul>
<ul>8.热启动和复制到目录下自动添加jar包？？</ul>

<h1>7.26</h1>
<ul>1.发现那个上传居然有错，后来查出来是路径不存在，自己制定一个路径是OK的，然后了解了project Structure设置</ul>
<ul>2.project Structure设置存在谷歌的收藏里了，很好的介绍</ul>
<ul>3.想要了解下增量爬取策略</ul>
<ul>4.之前有个bug，点击下一页，到了最后一页之后，继续点击会跳到第一页，用<c:if>做了个判断，判断pageinfo.pageNum!=pageinfo.pages，成功解决。</ul>
- **修改商品信息**
<ul>1.在jsp中链接带着参数，比如/xxx?id=1,就算是这样，controller里面还是只要/xxx 就好，在捕获url参数的时候，用@PathVariable注解</ul>
<ul>2.逻辑很简单，先根据id查询原本的信息，并回显，然后重新提交入库</ul>
<ul>3.唯一的点就是,jsp页面表单中，可以使用hidden的input框，通过value传递一些值</ul>



<h1>7.27</h1>
- **数据校验**
<ul>1.导jar包，hibernate-validator-5.2.2.Final.jar，，jboss-logging-3.1.0.CR2.jar，，，validation-api-1.1.0.Final.jar，，还有需要一个classmate.jar</ul>
<ul>2.xml配置</ul>
<ul>3.onclick="javascript:location='/register'"要熟练掌握</ul>
<ul>4.实现数据校验，首先controller接收的参数带有@Validated 的注解，然后domain类中对相关字段进行诸如@Size(min = 3,max = 6,message = "{username.length.error}") 的注解</ul>
<ul>5.有一个功能，在输入有误的时候，进行提示，先把错误的信息传导后台，然后BindingResult bindingResult处理，同时提示出错之后，错误的信息不能消失啊，不能让别人再填一次，所以还要数据回显</ul>


<ul>上面的关键代码不能粘贴，在UserController的addUser方法里，对每一个错误名称和错误信息都传入了model</ul>
<ul>propeties里的中文在网页里乱码，难道要弄成unicode??</ul>
- **自己的想法**
<ul>1.有没有那种类似权限验证的，或者处理cookie的，不带着cookie或者没有登录，就不能访问有关页面？？</ul>
<ul>2.好像springBoot是处理高并发的？？改天试试</ul>
<ul>3.这个弄完再做一个电商项目，然后去看jquery视频</ul>
<ul>4.不用jsp，直接springmvc和html交互数据</ul>

- **拦截器**
<ul>1.只拦截handler,也就是只拦截路径，不拦截页面jsp等等</ul>
<ul> request.getRequestDispatcher("loginForm").forward(request, response);</ul>
<ul>明天再搞，弄完拦截器，就去做电商项目或者jquery</ul>





<h1>7.28</h1>
- mawen其实本质上就是个工具，有着项目模板，和jar包管理
<ul>1.http://mvnrepository.com/这个网址可以查询包的依赖</ul>
<ul>2.基本配置好，https://www.cnblogs.com/Leo_wl/p/4459274.html</ul>
<ul>3.eclipse working set在intel中就是projects,里面对应的是modules</ul>
<ul>4.凌晨收获，eclipse里的work set,intel里面没有啊，直接创建的就是父工程，子工程就是modules</ul>




<h1>7.29</h1>
- 明天第一件事情，按照图片上的，配置好环境，设置好打包方式等等
<ul>1.modules的打包方式，有pom.war,jar，由<packaging>war</packaging>控制，一般没有模板的maven项目都是pom,父工程也是pom</ul>
<ul>2.pom工程就是聚合工程，就是不打包的</ul>
<ul>3.有一个很蛋疼的，父工程里面规定了版本控制，但是假如不包在<dependencyManagement>这个标签里，就会不管用，这时候就必须在子工程里面申明版本，否则就会出现unkown包</ul>

- **淘淘商城maven创建完美开局**
<ul>1.taotaoProj是空项目，一般是quickstart,需要网页就是webapp</ul>

<ul></ul>


<h1>7.30</h1>
<ul>1.成功把taotao-parents项目Install maven了，有两个install，要区分开</ul>
<ul>2.右边有个maven projects，里面可以对项目进行clean,install,package</ul>
<ul>3.系统间通信，可以用restful,可以用dubbo,里面再用zookeeper进行注册中心的配置</ul>
<ul>4.阿里的com.alibaba.druid.pool.DruidDataSource比C3P0这些的都要好用</ul>
<ul>5.Intel的maven，classpath是src，然后resources放在src下，设为resource才能扫描到（大错特错，classpath就是resources）</ul>
<ul>6.一个知识点，拦截器/ 的意思是拦截所有除了jsp文件</ul>
<ul>7.原来xshell可以连接虚拟机，然后自己电脑上要做集群呢，配置要低一些，比如无桌面，内存小，32位之类的</ul>
<ul></ul>
<ul></ul>





<h1>7.30</h1>
<ul>1.有点白痴，把ip地址写错了，折腾了一上午，总算搞定了</ul>
<ul>2.linux的Path搞了无数次，这次再重申，vim /etc/profile,然后source /etc/profile立即生效</ul>
<ul>3.贼难受，搞了一天吧，还是报错，dubbo和zookeeper还是有错，不过报的是注入的问题</ul>
<ul>4，找了个专门的IDEA的教程，明天跟着做一下</ul>
<ul>5.一般用quickstart,web项目用webapp,聚合项目用site</ul>


<h1>8.1</h1>
- 
<ul>1.看了IDEA的视频，学会了不用maven的模板，然后自己加框架支持，最好用</ul>
<ul>2.从eclipse重新开始</ul>



<h1>8.2</h1>
- **从eclipse开始，终于解决了**
<ul>1.原来我数据库根本没有连接上，所以一直报错timeout,连接了就好了，而且zookeeper经常会宕机，不能restart,必须要先stop,然后start</ul>
<ul>2.可能IDEA也没错吧，但是我不想花时间去改了，没必要</ul>

- **进入开发**
<ul>1.@PAthVariabvle 注解，获得url参数</ul>
<ul>2.把Project Explorer换成Package Explorer</ul>
<ul>3.eclipse批量选中一些文件，按住shift,选中上下文件即可</ul>
<ul>4.为什么要实现json的序列化，序列化类要继承xxxxxxxx</ul>
<ul>5.这个东西和之前做的拍卖商城的实现方式有点不一样。上次那个startpage之类的操作放在controller，淘淘是全放在service里面</ul>
<ul>6.页面不是自己写的，是用easyui的框架弄的，同时学到了怎么返回json，因为跨工程，所以要序列化，然后@responsebody,逻辑都写在seviceimpl里，另外和之前做的分页没有区别</ul>




<h1>8.3</h1>
<ul>1.dubbo监控中心的使用，把dubbo-admin.war放在tomcat的webapps下即可，就可以访问ip:8080/dubbo-admin</ul>
<ul>2.day3讲了git服务器搭建的东西，现在不看，以后可以看</ul>
- **门户网站的搭建**
<ul>1.创建一个新的项目，web.xml里面不再是拦截/，而是拦截*.html,这样一来，url带有html,但是controller可以返回jsp,做到伪静态化，而且因为不是拦截/，对静态资源也不用特别注明</ul>
<ul>2.Ctrl+Shift+C快速注释eclipse</ul>
<ul>3.js,css等静态资源放在webapps下，不是放在WEB-INF下，WEB-INF目录是被保护起来的，其下的jsp页面不能直接运行，只能通过控制器跳转来访问；静态资源（js、css、img）也不能被WEB-INF目录外的其他文件直接引用</ul>
<ul>4.CMS系统进行内容管理</ul>
<ul>5.EasyUITreeNode的使用，这个概念不是很懂</ul>


<h1>8.4</h1>
- **EasyUiTree**
<ul>1.异步树控件的使用，这其实就是一个Ajax请求控件，每次发送一个id参数，服务器返回id,text,state的一个json</ul>
<ul>2.别忘了设置默认值parentId,还有pojo类的序列化</ul>
<ul>3.要返回json数据，要么用pojo，要么用mapper,而且@Responsebody</ul>

- **图片服务器**
<ul>1.ps aux|grep nginx*</ul>
<ul></ul><ul></ul>
<ul></ul>

- t**aotao-content中的内容管理目录和新增商品分类的目录部署**
<ul>1.遇到bean无法注入的时候，看看上下文有没有这个Bean,这一次我是忘了在dubbo中引用，所以没有bean</ul>
<ul>2.@RequestParam(value = "pageNumber",required = false,defaultValue = "1") ，还必须紧跟着对应的值(但是value要和传过来的值的name一样)</ul><ul></ul>


<h1>8.5</h1>
<ul>1.switchhosts的使用</ul>
<ul>2.反向代理简单说就是服务的转发</ul>
<ul>3.apache和nginx都可以提供http服务</ul>
<ul>4.虚拟机可以克隆</ul>
<ul>5.maven项目不能直接添加自己的jar包，需要用命令行先install该jar包，也就是先要装进仓库</ul>
<ul>6.fastDFS工具类的使用</ul>
<ul>7.贼傻逼的一个事情，那个图片服务器读取配置文件，因为路径有空格，导致不行，改掉之后，eclipse除了问题，不能加载，只能重新创各个子模块，搞定之后，还发现一个bug，现在这个逻辑下，不需要点提交新商品信息，只要上传了图片，图盘服务器就上传了</ul>


<h1>8.6</h1>
<ul>1.eclipse插件egit,昨天晚上eclipse上传到github老是失败</ul>
<ul>2.怪不得一直无法上传，要在git的设置里面自己添加用户名密码等字段</ul>
<ul>3.更改github项目的语言显示，创建.gitattributes，添加*.js linguist-language=java；*.css linguist-language=java；*.html linguist-language=java即可</ul>
<ul>4.util.date和sql.date是不一样的，，要找机会弄明白</ul>
<ul>5.突然想到redict重定向</ul>
<ul>6.一个特别重要的点，controlller方法里，如果不加@ResponseBody.那就是要返回jsp啊，这种被视图解析器解析的后缀，比如返回json,mapper,pojo,就必须要@ResponseBody</ul>
<ul>7.以前思考的一个问题，就是不用Jsp,怎么传输数据，现在其实已经知道了，前端使用ajax,后端用json,pojo,mapper都可以传输数据</ul>
<ul>8.想了很久，觉得java web到这个地步，不学js，进行不下去了，后面很多东西看都看不懂，根本搞不好，所以先李南江的js视频学起来，js差不多之后，再开始继续电商项目</ul>


<h1>8.7</h1>
- **jquery**
<ul>1.掌握jquery入口函数和原生JS的入口函数</ul>
- **jQuery和原生JS的区别**
<ul>1.原生JS等DOM元素全部加载，包括图片弄好再执行，而jquery不加载图片什么的</ul>
<ul>2.原生JS的入口函数会被覆盖，而jquery的入口函数会依次执行</ul>
<ul>3.jquery $的冲突。第一种方法，jQuery.noConflict(),然后就只能使用"jQuery",第二种var xxxx = jQuery.noConflict(),这样就可以使用xxxx</ul>
<ul>4.静态方法通过类名调用，实例方法通过对象调用</ul>
<ul>5.可以直接拖动文件进来吗</ul>
- **jQuery核心方法**
<ul>1.$(),这个就是核心方法</ul>
<ul>2.参数是方法，也就是function,照常执行</ul>
<ul>3.参数是DOM选择器，返回选择的带有DOM元素的jQuery对象</ul>
<ul>4.参数是HTML代码，返回jQuery对象</ul>
- **jQuery对象**
<ul>1.伪数组，可以[0] ,类似取下标这种操作</ul>

- **jQuery静态方法**
<ul>1.比如先整个类function Aclass() {},Aclass.xxx=function(){},这个就是静态方法了，Aclass.prototype.xxxx就是实例方法了</ul>
<ul>2.$.holdReady(true)和$.holdReady(false)控制入口函数的暂停和放行</ul>

- **jetbrain系列的自定义代码模板**
<ul>1.经常要写的模板，可以自定义缩写，并使用</ul>


<h1>8.8</h1>
- **jQuery内容选择器**
<ul>1.empty 2.parent 3.contains 4.has</ul>

- **另外**
<ul>1.prop()和attr(),prop()的范围更广，但是不是返回值true,false的，推荐用attr</ul>
<ul>2.addClass,removeClass,toggleClass,这些是对class属性的操作</ul>
<ul>3.html,text,val</ul>
<ul>4.css(),可以逐个添加，可以链式操作，还可以传入{width:100px;xxxxxxxxxx}这类的对象</ul>
<ul>5.各种尺寸偏移函数，有个scrollTop,无参是获取滚动距离，有参是设置滚动距离，为了保证IE或者Chrome等都能成功获取页面滚动，可以这么写$("body").scrollTop()+$("html").scrollTop(),其中一项为零，另一项就不为零，还有$("html,body")</ul>
<ul>6.jQuery绑定事情，1.$("div").click(fn),第二种，$("div").on("click",fn)。而且同一对象可以绑定多个，甚至是不同的事件，不会被覆盖，都会执行</ul>
<ul>7.off()无参解绑所有事件，一个参数，解绑一个类型，两个参数，解绑该类型的某方法</ul>
<ul>8.事件冒泡就是字标签触发了一个事件，父标签同样触发，只要字标签里return false，就可以避免，同理，阻止默认行为，return false同样可以做到</ul>
<ul>9.自动触发事件，一般使用trigger()或者triggerHandler()。里面传入事件类型，比如“click”。。。但这两个有所不同，trigger()会触发默认行为和事件冒泡，triggerHandler()就不会，但是在处理a标签的时候有特殊</ul>
<ul>10.接上条，a标签，一般是跳转到某个链接，trigger()和triggerHandler()在自动触发后，都不会进行跳转，所以要解决这个，就要在a中加入span之类的标签，事件绑定在span上，再进行trigger()</ul>




<h1>8.9</h1>
<ul>1.想要自定义事件，必须用on来绑定</ul>
<ul>2.给事件添加命名空间，首先必须是用on绑定，然后“click.liyang”, 类似于这样，在触发的时候trigger(“click.liyang”)</ul>
<ul>3.delegate???终于明白了事件委托，在入口函数执行的过程中，DOM中有些元素是后来才加上的或者后来才出现的，不是一开始加载就有的，所以需要先委托给早就有的，用delegate来监听后出现的元素的行为</ul>
<ul>4.IDEA永久破解搞定https://blog.csdn.net/weixin_37937646/article/details/79119540</ul>
<ul>5.鼠标的移入移出事件，第一种mouseover和mouseout,子标签移入移出也会触发父标签的动作，第二种mouseenter和mouseleave，就不会重复触发，第三种，移入和移出合二为一，hover(),参数就是两个fn</ul>
<ul></ul><ul></ul>

</ul>
- **delegate小案例**
<ul>1.css样式之类的，比如html,body{}，，，，，还有width: 100%;height: 100%;就是占满屏幕的意思。。。。。。。。。。position: fixed;背景透明吧，，，，，，， top: 0;left: 0;选中左上，，，，，，， margin: 100px auto;居中，，，，，，，position: relative;和position: absolute;</ul>


- **电影排行榜移入移出显示功能**
<ul>1.css布局，，，，padding:10px 5px 15px 20px;分别代表上右下左，，，，text-align: center;字体位置设置。。。。。。margin-right: 10px;右边距，，，，，父标签清除浮动overflow: hidden，，，，，，display: none;和display: block;是否隐藏，，</ul>
<ul>2.JS逻辑，把一个东西放进div里，并预先设置display: none，然后.current .content{display: block;}，类似这样把class="content"的div和current的class相关联，这样，只有标签里存在current的class，才会显示，再结合鼠标移入移出即可</ul>
<ul>3.忘了一个很厉害的点，overflow：auto;使用这个在显示不下的其情况，他会自动添加滚动条</ul>

<h1>8.10</h1>
- **TAB菜单**
<ul>1.css样式，，，，，list-style: none;去掉li标签黑点，，，，，，line-height: 50px;调整行高，，，，，，，</ul>
<ul>2.JS逻辑，eq()和get()，一个是获取对应index的元素并封装成jquery对象，另一个只返回元素，不生成对象，，，，，，index()，返回被选中的元素的下标位置，，，，，，$(this).siblings()，选中除当前标签的其他所有同类标签，类似于反选</ul><ul></ul>
<ul>3.很牛逼的发现，js代码可以像链子一样一直xxxx.xxxx.xxxx过去，很方便</ul><ul></ul>
<ul>4.show()和hide(),相关参数，time(ms)，fn(出现隐藏效果结束后执行的函数)</ul>

- **对联广告**
<ul>1.是对上面show(),hide()的使用，这里要注意top：50%的时候，图片特别下面，这是为啥？？？？？？？，，，，，，一个元素display:none,,直接用show()即可。</ul>
<ul>2.之前的display的转换，都是通过将display属性写进class样式里，然后addClass或者remove实现的，，在这里直接用的是show和hide，还有一个更直接的方法$(this).css("display","none")</ul>


<ul>3.这里top的百分比参数怎么回事啊？？（懂了，搞定了，50%的时候看起来很下面，是因为这是图片的上沿对准了50%这个位置，而且是相对于一个屏幕的比例）</ul>
<ul>4.css里面的百分比%，一般都是相对于父元素</ul>


- **IDEA快捷键小技巧**
<ul>1.按住ALT下拖，就能选中同一列的多个光标</ul>
<ul>2.那个同时选中多个光标的咋弄的来着？？？？</ul>


<h1>8.11</h1>
- ajax实践
<ul>1.原生ajax稍微了解，主要是jquery的ajax()</ul>
<ul>2.现在我自己实验的是，ajax用GET方法，后台返回直接返回String或者String样式的json,前端里面再转成JSON，，，这里有个大坑，前端要获得返回的数据，应该在success里面传入参数，再转成json</ul>
<ul>3.我现在探索的是，怎么在后台直接变成Json</ul>
<ul></ul>
<ul></ul>
<ul></ul><ul></ul><ul></ul>






