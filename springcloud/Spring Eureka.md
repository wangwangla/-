---
title: Spring Eureka
user: 见贤思齐
date: 2018-12-18
---
### 注册仓库的使用
- 导入jar文件
```
<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka-server</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>
```
- 写启动main类
```
@SpringBootApplication
@EnableEurekaServer//服务端
public class SpringCloudEurekaApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringCloudEurekaApplication.class, args);
	}
}
```
- 写配置
```
spring.application.name=spring-cloud-eureka
server.port=8000
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
eureka.client.serviceUrl.defaultZone=http://localhost:${server.port}/eureka/
```
**参数说明**
```
eureka.client.register-with-eureka ：表示是否将自己注册到Eureka Server，默认为true。
eureka.client.fetch-registry ：表示是否从Eureka Server获取注册信息，默认为true。
eureka.client.serviceUrl.defaultZone ：设置与Eureka Server交互的地址，查询服务和注册服务都需要依赖这个地址。默认是http://localhost:8761/eureka ；多个地址可使用 , 分隔。
```
启动之后就已经将注册中心启动了。

####  注册中心集群
```
注册中心这么关键的服务，如果是单点话，遇到故障就是毁灭性的。在一个分布式系统中，服务注册中心是最重要的基础部分，理应随时处于可以提供服务的状态。为了维持其可用性，使用集群是很好的解决方案。Eureka通过互相注册的方式来实现高可用的部署，所以我们只需要将Eureke Server配置其他可用的serviceUrl就能实现高可用部署。
```
- 创建两个配置文件
配置1：
```
spring.application.name=spring-cloud-eureka
server.port=8000
eureka.instance.hostname=peer1
eureka.client.serviceUrl.defaultZone=http://peer2:8001/eureka/
```
配置2
```
spring.application.name=spring-cloud-eureka
server.port=8001
eureka.instance.hostname=peer2
eureka.client.serviceUrl.defaultZone=http://peer1:8000/eureka/
```
但是在启动的时候需要指定配置文件

- 多个节点
将配置写入一个文件的方式
```
---
spring:
  application:
    name: spring-cloud-eureka
  profiles: peer1
server:
  port: 8000
eureka:
  instance:
    hostname: peer1
  client:
    serviceUrl:
      defaultZone: http://peer2:8001/eureka/,http://peer3:8002/eureka/
---
spring:
  application:
    name: spring-cloud-eureka
  profiles: peer2
server:
  port: 8001
eureka:
  instance:
    hostname: peer2
  client:
    serviceUrl:
      defaultZone: http://peer1:8000/eureka/,http://peer3:8002/eureka/
---
spring:
  application:
    name: spring-cloud-eureka
  profiles: peer3
server:
  port: 8002
eureka:
  instance:
    hostname: peer3
  client:
    serviceUrl:
      defaultZone: http://peer1:8000/eureka/,http://peer2:8001/eureka/
```

