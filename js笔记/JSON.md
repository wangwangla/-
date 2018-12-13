---
title: JSON
user: 见贤思齐
date: 2018-12-13
---
####  json
```
var json = {"name":"拴住","age":18,"arr":[1,2,3]};
```
> 注意：
    对象本身没有length,所以不能用for循环遍历
    要用for。。。in...循环

#### 打印

```
    var arr = [1,2,3];
    for(var k in arr){
        console.log(arr[k])
    }
```
打印结果：
	1.2.3

打印2
```
var aaa = {"name":"拴住","age":18,"arr":[1,2,3]};
for(var k in aaa){
        console.log(k);
}
```
结果：
	name、age、arr

打印3
```
console.log(aaa[k]);
```
结果：将对象属性值打印出来

数组的大小
```
var arr = [1,2,3];
for(var k in arr){
      console.log(arr[k])
}
```
##### 创建json
```
var json = {};
console.log(json);
for(var i=1;i<10;i++){
	json[i] = i*10;
}
console.log(json);

```
定义json
```
    for(var k in json){
        console.log(json[k]);
    }
```