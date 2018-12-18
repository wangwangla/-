---
title: spring boot快速入门
user: 见贤思齐
date: 2018-12-17
---
**controller第一例**
```
@Controller
public class HelloController {

    @RequestMapping(value = "/hello",method = RequestMethod.GET)
    @ResponseBody
    public String sayHello() {
        return "Hello，Spring Boot！";
    }
}
```
- 控制层上使用@Controller，在方法上使用@RequstMapping("设置路径")，method=RequestMethod.GET方法。
- 启动
```
@SpringBootApplication
public class App {
	public static void main(String[] args) {
		SpringApplication.run(App.class, args);
	}
}
```
使用@SpringBootApplication进行注解加载自动配置。
- 配置设置编码
```
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>
```
**配置参数设置**
- 配置文件
```
## \u4E66\u4FE1\u606F
demo.book.name=[Spring Boot 2.x Core Action] From Dev
demo.book.writer=BYSocket
```
- 获取参数配置
```
@Component
public class BookProperties {
	 /**
     * 书名，从配置中获取参数来设置
     */
    @Value("${demo.book.name}")
    private String name;

    /**
     * 作者
     */
    @Value("${demo.book.writer}")
    private String writer;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getWriter() {
        return writer;
    }

    public void setWriter(String writer) {
        this.writer = writer;
    }
}
```
- 使用配置参数
```
@Autowired
BookProperties bookProperties;
bookProperties.getWriter()
```
其实参数只是将数据从配置中获取参数。
- 在注解上添加前缀
```
@Component
@ConfigurationProperties(prefix = "demo.book")
@Validated
public class BookComponent {

    /**
     * 书名
     */
    @NotEmpty
    private String name;

    /**
     * 作者
     */
    @NotNull
    private String writer;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getWriter() {
        return writer;
    }

    public void setWriter(String writer) {
        this.writer = writer;
    }
}
```
**web的操作**
```
@Controller
@ResponseBody
public class WebController {
	@Autowired 
	private WebService webService;
	
	@RequestMapping(value="/",method=RequestMethod.GET)
	public Entity getEntity() {
		return webService.fun();
	}
}

```
- @ResponseBody：返回的是json
- @Controller：控制层
- url：value="/"
- method:method=RequestMethod.GET
- @service：服务层
**表单验证**
- 加入依赖
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
- web层
```
@RequestMapping(method = RequestMethod.GET)
public String getUserList(ModelMap map) {
    map.addAttribute("userList", userService.findAll());
    return "userList";
}
```
通过modelMap map的addAttribute进行将数据放入到list中
返回的userList是页面的名字
验证：
```
 @Id
    @GeneratedValue
    private Long id;

    /**
     * 名称
     */
    @NotEmpty(message = "姓名不能为空")
    @Size(min = 2, max = 8, message = "姓名长度必须大于 2 且小于 20 字")
    private String name;

    /**
     * 年龄
     */
    @NotNull(message = "年龄不能为空")
    @Min(value = 0, message = "年龄大于 0")
    @Max(value = 300, message = "年龄不大于 300")
    private Integer age;

    /**
     * 出生时间
     */
    @NotEmpty(message = "出生时间不能为空")
    private String birthday;
```

**获取参数**
```
    /**
     * 处理 "/users/{id}" 的 GET 请求，用来删除 User 信息
     */
    @RequestMapping(value = "/delete/{id}", method = RequestMethod.GET)
    public String deleteUser(@PathVariable Long id) {

        userService.delete(id);
        return "redirect:/users/";
    }
```
**H2**
添加依赖
```
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <!-- h2 数据源连接驱动 -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>runtime</scope>
        </dependency>
```
写实体
```
package kw.test.valid;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Table
@Entity
public class User {
	@Id
	@GeneratedValue(strategy=GenerationType.AUTO)
	private Long id;
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	private String username;
	private String password;
	public String getUsername() {
		return username;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
	
}

```
写仓库
```
package kw.test.valid;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

/**
 * 用户持久层操作接口
 *
 * Created by bysocket on 21/07/2017.
 */
@Repository
public interface UserRepository extends JpaRepository<User, Long> {

}
```
Controller使用
```
	@Autowired
	private UserRepository userRepository;
	@RequestMapping("/")
	public void  test() {
		User user = new User();
		user.setUsername("test");
		user.setPassword("111");
		userRepository.save(user);
	}
	@RequestMapping("/find")
	public List<User>  gettest() {
		return userRepository.findAll();
	}
	
```
**使用log**
```
private static final Logger LOGGER = LoggerFactory.getLogger(UserServiceImpl.class);
```
**分页查询**
```
 @Override
    public Page<User> findByPage(Pageable pageable) {
        LOGGER.info(" \n 分页查询用户："
                + " PageNumber = " + pageable.getPageNumber()
                + " PageSize = " + pageable.getPageSize());
        return userRepository.findAll(pageable);
    }

```
分页参数
     *    Pageable 支持的分页参数如下
     *    page - 当前页 从 0 开始
     *    size - 每页大小 默认值在 application.properties 配置
**redis的使用**
```
 <!-- Cache 缓存依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-cache</artifactId>
        </dependency>

        <!-- Redis 数据源依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-redis</artifactId>
        </dependency>
```
**验证**
```
	@NotNull
	private String username;
```
然后在保存到数据的时候，未设置username，就会报错。
ConstraintViolationImpl{interpolatedMessage='不能为null', propertyPath=username, rootBeanClass=class kw.test.valid.User

正式项目中，需要使用一个异常处理，然后将其捕获。

```
@CacheConfig(cacheNames = "books")

@CachePut(key = "#p0.id")
```
```
package kw.test.cache;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.cache.annotation.CacheConfig;
import org.springframework.cache.annotation.CachePut;
import org.springframework.stereotype.Service;

@CacheConfig(cacheNames = "books")
@Service
public class UserService {
	@Autowired
	private UserRepository userRepository;
	public void  save() {
		User user = new User();
		user.setUsername("222222");
		user.setPassword("111");
		userRepository.save(user);
	}
	@CachePut(key = "#p0.id")
	public List<User> findAll() {
		return userRepository.findAll();
	}
	
}

```
**elasticsearch的使用**
