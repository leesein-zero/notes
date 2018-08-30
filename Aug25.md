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