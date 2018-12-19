---
title: Hystrix 
user: 见贤思齐
date: 2018-12-18
---

### Hystrix
- 使用步骤
1.application.properties添加：
feign.hystrix.enabled=true
2.创建回调类
创建HelloRemoteHystrix类继承与HelloRemote实现回调的方法
```
@Component
public class HelloRemoteHystrix implements HelloRemote{

    @Override
    public String hello(@RequestParam(value = "name") String name) {
        return "hello" +name+", this messge send failed ";
    }
}
```
3.添加fallback属性
在HelloRemote接口添加指定fallback类，在服务熔断的时候返回fallback类中的内容
```
@FeignClient(name= "spring-cloud-producer",fallback = HelloRemoteHystrix.class)
public interface HelloRemote {

    @RequestMapping(value = "/hello")
    public String hello(@RequestParam(value = "name") String name);

}
```
4.启动
将所有的进行启动，然后可以正常访问，下来手动的挂掉提供者，再次访问就会访问其他的
