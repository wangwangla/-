---
title: provider
user: 见贤思齐
date: 2018-12-18
---

### 服务提供方
- 添加pom
```
<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
</dependencies>
```
- 配置
```
spring.application.name=spring-cloud-producer
server.port=9000
eureka.client.serviceUrl.defaultZone=http://localhost:8000/eureka/
```
第一个参数服务名，第二个是服务的端口，第三个是将服务注册的仓库地址
将自己的服务注册到仓库中，所以相对于仓库是一个客户端
```
@SpringBootApplication
@EnableDiscoveryClient
public class ProducerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ProducerApplication.class, args);
	}
}
```
- 通过服务接口
```
@RestController
public class HelloController {
	
    @RequestMapping("/hello")
    public String index() {
        return "hello 见贤思齐，this is first messge";
    }
}
```
