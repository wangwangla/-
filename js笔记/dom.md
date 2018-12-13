---
title: dom
user: 见贤思齐
date: 2018-12-13
---

#####  一些内置的使用

创建时间对象

 第一种
 ```
 var date1 = new Date();
  console.log(date1);
```
第二种
```
var date2 = new Date("2016/09/06 00:00:00");
console.log(date2);
```
后两种兼容性不好，不推荐使用
第三种
```
var date3 = new Date('Wed Jan 27 2016 12:00:00 GMT+0800 (中国标准时间)');
```
第四种
```
var date4 = new Date(2016, 1, 27);
```
常用的方法
```
 console.log(date1.getDate()          )       //获取日 1-31
console.log(date1.getDay ()          )       //获取星期 0-6（0代表周日）
console.log(date1.getMonth ()        )       //获取月 0-11（1月从0开始）
console.log(date1.getFullYear ()	 )      //获取完整年份（浏览器都支持）
console.log(date1.getHours ()	     )       // 获取小时 0-23
console.log(date1.getMinutes ()	     )     //获取分钟 0-59
console.log(date1.getSeconds ()	     )     //获取秒  0-59
console.log(date1.getMilliseconds () )       //获取毫秒 （1s = 1000ms）
console.log(date1.getTime ()	     )      //返回累计毫秒数(从1970/1/1午夜)
```

### 案例
```
//1.创建一个当前日期的日期对象
var date = new Date();
//2.然后获取其中的年月日和星期
var year = date.getFullYear();
var month = date.getMonth();
var hao = date.getDate();
var week = date.getDay();
//console.log(year+" "+month+" "+hao+" "+week);
//3.赋值给div
var arr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
var div = document.getElementsByTagName("div")[0];
div.innerText = "今天是："+year+"年"+(month+1)+"月"+hao+"日 "+arr[week];
innerText将数据写出去。
```
### 案例2
```
var future = new Date("2019/01/01 00:00:00");
var timeSum = future.getTime() - nowtime.getTime();
var day = parseInt(timeSum/1000/60/60/24);
var hour = parseInt(timeSum/1000/60/60%24);
var minu = parseInt(timeSum/1000/60%60);
var sec = parseInt(timeSum/1000%60);
var millsec = parseInt(timeSum%1000);
```
#### 事件添加方法
方式一：
		获取元素，然onClick，一个function处理就可以了。
方法二：
	增加一个点击事件，然后执行一个方法
```
	 btn.addEventListener("click",fn1);
	btn.addEventListener("click",fn2);
	function fn1(){
		console.log("九尺龙泉万卷书，上天生我意何如。");
	}
	function fn2(){
		console.log("不能报国平天下，枉为男儿大丈夫。");
	}
```
##### 事件监听的方法
```
 //原理（了解）（自己封装一个）(click)
    function fn(str,fn,ele){
        //判断位置要注意：如果进入绑定事件本身，那么该事件已经本绑定了
        //所以获取旧的事件必须在新的事件绑定之前
        var oldEvent = ele["on"+str];
        ele["on"+str] = function () {
            //不能直接执行函数，因为我们还不知道以前有没有绑定我同样的事件
            //进行判断，如果以前有过绑定事件，那么把以前的执行完毕在执行现在的事件，如果没有就直接执行
            //如果没有被定义过事件该事件源的该事件属性应该是null对应的boolean值是false
            //如果已经定义过事件该事件源的该事件属性应该是function本身对应的boolean值是true
            if(oldEvent){
                //因为oldEvent本身他就是函数本身，那么后面加一个();就是执行函数
                oldEvent();
                fn();
            }else{
                //没有绑定过事件
                fn();
            }
        }
```
```
fn("click",fn1,btn);
fn("click",fn2,btn);
fn("click",fn3,btn);
```
#### 绑事件
```
   var div = document.getElementsByTagName("div")[0];

    div.onclick = fn;

    function fn() {
        alert(1);
    }

    //第二种属性绑定
//    div["onclick"] = function () {
//        alert(2);
//    }

//    console.log(div.onclick);
//    console.log(div.onmouseover);

    div.removeEventListener("click",fn);

```
#### 获取子类
```
var arr = sel1.children;
```
#### 给子类添加
```
sel2.appendChild(arr[0]);
```