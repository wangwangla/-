---
title: JQuery 
user: 见贤思齐
date: 2018-12-15
---
**jQuery初体验**
*****
1.页面加载结束
> 原始js
```
window.onload== function () {}
```
> jQuery处理方式
```
$(document).ready(function () {});
```
> 获取标签 
js
```js
var btn = document.getElementsByTagName("button")[0];
var divArr = document.getElementsByTagName("div");
```
jQuery
```jQuery
var jQbtn = $("button");//根据标签名获取元素
var jQdiv = $("div");//根据标签名获取元素
```
> 绑定事件
js
```
btn.onclick = function (){}
```
JQuery
```
 jQbtn.click(function () {});
```
2.入门
	使用步骤：
> 加载js文件
```
<script src="jquery-1.11.1.js"></script>
```
> 入口
```
$(document).ready(function () {
            //获取元素和绑定事件（通过方法实现）
        });
```
3.程序入口
> 传统js的程序入口
```
//原生js，入口函数。页面上所有内容加载完毕，会执行。
//不仅文本加载完毕，而且图片也要加载完毕，在执行函数。
        window.onload = function () {
        alert(1);
}
```
> jQuery的程序入口
```
jquery的入口函数。  1.文档加载完毕，图片不加载的时候就可以执行这个函数。
      $(document).ready(function () {
       alert(1);
})
```
简写
```
$(function () {
     alert(1);
});
```
**jQuery的$和JQuery的关系**
```
console.log($);
console.log(jQuery);
console.log($==jQuery)
```
最终的结果是true
**jQuery中的dom和js的有什么区别**
- jquery对象是一个数组。数组中包含着原生JS中的DOM对象。
- jquery中有css();  原因就是因为：jquery有一层功能皮肤。原生的没有
```
jqdiv.css({"width": 100,"height":100,"background-color":"red","margin":10});
```
如果想要那种方式设置属性或方法，必须转换成该种类型。
1.js对象转换成jquery对象。     $(js对象);
```
var box = document.getElementById("box");
var cbox = document.getElementsByClassName("box");
var div = document.getElementsByTagName("div");

box = $(box);
cbox = $(cbox);
div = $(div);
```
3.2.jquery对象转换成js对象。     1.jquery对象[索引值]   2.jquery对象.get(索引值)
```
jquery对象转换成js对象
jqdiv[0].style.backgroundColor = "black";
jqdiv.get(4).style.backgroundColor = "pink";
```
**案例
```
		$(function(){
			var arr = $('li');
			for(var i=0;i<arr.length;i++){
				if(i%2==0){
					arr[i].style.color="blue";
				}
			}
		});
```
设置属性
```
$('div').css("background-color","red")	
$('div').css("width",100)	
$('div').css("height",100)	
```
数组试过但是有问题

**选择器**
```
 var jqdiv = $("div");
 var jqCdiv = $(".box");
 var jqIdiv = $("#box");
```
**后代选择器**
```
var jqli = $("ul li");
```
**子类选择器**
```
var jqotherLi = $("ul>li");
```
**过来选择器**
```
 获取奇数
 var jqliodd = $("ul li:odd"); //获取奇数索引
 获取偶数
 var jqlieven = $("ul li:even");//获取偶数索引
指定
 var jqlieven = $("ul li:eq(0)");//获取指定索引
 计算方式进行
var jqlifirst = $("ul li:eq("+(li.length-1)+")");
```
**find**
```
var jqul = $("ul"); //获得所有的ul
//find(selector); 从jquery对象的后代中查找
//必须指定参数，如果不指定获取不到元素。length === 0
jqul.find("li").css("background","pink");
//必须指定参数，不然就不会定位参数
console.log(jqul.find());
//chidlren(selector); 从jquery对象的子代中查找
//不写参数获取所有子元素。
jqul.children("li").css("background","green");
//eq(索引值); 从jquery对象的子代中查找该索引值的元素
//要求该数组中的第几个。
jqul.children().eq(0).css("background","red");
 //next(); 该元素的下一个兄弟元素
 jqul.children().eq(0).next().css("background","yellow");           
 //siblings(selector); 该元素的所有兄弟元素
 jqul.children().eq(0).next().siblings().css("border","1px solid blue");
 //parent(); 该元素的父元素（和定位没有关系）
console.log(jqul.children().eq(0).parent());
```
案例：隔行变色
```
$(li:odd)
$(li:even)
```
**鼠标事件**
```
//鼠标进入变色，移开回复
//计数器
    var color = "";
     $("li").mouseenter(function () {
           color = $(this).css("background");
           $(this).css("background","blue");
    });
      //移开恢复
    $("li").mouseleave(function () {
    $(this).css("background",color);
});
```
**显示和隐藏**
```
$('div').hide();
$('div').show();
```
**案例**
```
 $(".wrap").find("li").mouseenter(function () {
                //连式编程
                $(this).css("opacity",1).siblings("li").css("opacity",0.4);
            });

            //离开wrap的时候所有的li全部opacity值为1；
            $(".wrap").mouseleave(function () {
                $(this).children().children("li").css("opacity",1);
//                $(".wrap li").css("opacity",1);
            });
```

**CSS属性的增加**
```
$("div").css({"width":100,"height":100,"background-color":"pink"});
$("div").css("background-color","red");
/获取的时候如果有很多，那么获取jquery对象中的第一个
 alert($("div").css("width"));
```
**css增加属性和删除属性**
```
 $("button").eq(0).click(function () {
       //添加类
       $("div").addClass("current");
       //判断类
        alert($("div").hasClass("current"));//has是have的单三
      });
        $("button").eq(1).click(function () {
       //删除类
       $("div").removeClass("current");
      //判断类
      alert($("div").hasClass("current"));//has是have的单三
});
```
**点击切换屏幕**
```
$(function () {
      $("button").click(function () {
      //需求：点击按钮 ，切换背景
     if($("div").hasClass("current")){
       //如果有类名，那么删除
              $("div").removeClass("current")
               }else{
                //如果没有类名，那么添加
               $("div").addClass("current")
          }
            });
        })
也可以使用开关进行设置
   //切换类（toggleCLass）
    $("div").toggleClass("current");
```

**show的使用**
```
 //显示动画用法1:   show();   不加参数
$("div").show();  //通过这个方法实现的：display: block;
//显示动画用法2:   show(2000);   毫秒值
 $("div").show(2000);  //通过这个方法实现的：display: block;
 //通过控制  宽高透明度和display

                //显示动画用法3:   show(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").show("slow");
//                $("div").show("fast");
//                $("div").show("normal");

                //显示动画用法1:   show(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").show(5000,function () {
//                    alert("动画执行完毕！");
//                });
            })
```
**hide的使用**
```
 $("button:eq(1)").click(function () {
//                //显示动画用法1:   hide();   不加参数
                $("div").hide();  //通过这个方法实现的：display: none;

//                //显示动画用法2:   hide(2000);   毫秒值
//                $("div").hide(2000);  //通过这个方法实现的：display: none;
//                //通过控制  宽高透明度和display

                //显示动画用法3:   hide(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").hide("slow");
//                $("div").hide("fast");
//                $("div").hide("normal");

                //显示动画用法4:   hide(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").hide(2000,function () {
//                    alert("动画执行完毕！");
//                });
            })

```
**滑动操作**
```
 $("button:eq(0)").click(function () {
//                //滑入动画用法1:   slideDown();   不加参数
                $("div").slideDown();

//                //滑入动画用法2:   slideDown(2000);   毫秒值
//                $("div").slideDown(2000);
//                //通过控制  高和display

                //滑入动画用法3:   slideDown(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").slideDown("slow");
//                $("div").slideDown("fast");
//                $("div").slideDown("normal");

                //滑入动画用法4:   slideDown(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").slideDown(5000,function () {
//                    alert("动画执行完毕！");
//                });
            })
```
**划出**
```
            //滑出动画
            $("button:eq(1)").click(function () {
//                //滑出动画用法1:   slideUp();   不加参数
//                $("div").slideUp();

//                //滑出动画用法2:   slideUp(2000);   毫秒值
//                $("div").slideUp(2000);  //通过这个方法实现的：display: none;
//                //通过控制  高和display

                //滑出动画用法3:   slideUp(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").slideUp("slow");
//                $("div").slideUp("fast");
//                $("div").slideUp("normal");

                //滑出动画用法1:   slideUp(毫秒值，回调函数[显示完毕执行什么]);
                $("div").slideUp(2000,function () {
                    alert("动画执行完毕！");
                });
            })
```
**隐藏**
```
 //滑出动画
            $("button:eq(1)").click(function () {
//                //滑出动画用法1:   slideUp();   不加参数
//                $("div").slideUp();

//                //滑出动画用法2:   slideUp(2000);   毫秒值
//                $("div").slideUp(2000);  //通过这个方法实现的：display: none;
//                //通过控制  高和display

                //滑出动画用法3:   slideUp(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").slideUp("slow");
//                $("div").slideUp("fast");
//                $("div").slideUp("normal");

                //滑出动画用法1:   slideUp(毫秒值，回调函数[显示完毕执行什么]);
                $("div").slideUp(2000,function () {
                    alert("动画执行完毕！");
                });
            })
```

**淡入淡出**
```
            //点击按钮后产生动画
            $("button:eq(0)").click(function () {
//                //淡入动画用法1:   fadeIn();   不加参数
                $("div").fadeIn();

//                //淡入动画用法2:   fadeIn(2000);   毫秒值
//                $("div").fadeIn(2000);
//                //通过控制  透明度和display

                //淡入动画用法3:   fadeIn(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").fadeIn("slow");
//                $("div").fadeIn("fast");
//                $("div").fadeIn("normal");

                //淡入动画用法4:   fadeIn(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").fadeIn(5000,function () {
//                    alert("动画执行完毕！");
//                });
            })



            //滑出动画
            $("button:eq(1)").click(function () {
//                //滑出动画用法1:   fadeOut();   不加参数
//                $("div").fadeOut();

//                //滑出动画用法2:   fadeOut(2000);   毫秒值
//                $("div").fadeOut(2000);  //通过这个方法实现的：display: none;
//                //通过控制  透明度和display

                //滑出动画用法3:   fadeOut(字符串);   slow慢：600ms   normal正常:400ms   fast快：200ms
//                $("div").fadeOut("slow");
//                $("div").fadeOut("fast");
//                $("div").fadeOut("normal");

                //滑出动画用法1:   fadeOut(毫秒值，回调函数[显示完毕执行什么]);
//                $("div").fadeOut(2000,function () {
//                    alert("动画执行完毕！");
//                });
            })



 $("button:eq(2)").click(function () {
                //滑入滑出切换
                //同样有四种用法
                $("div").fadeToggle(1000);
            })

            $("button:eq(3)").click(function () {
                //改透明度
                //同样有四种用法
                $("div").fadeTo(1000,0.5, function () {
                    alert(1);
                });
            })
```

**toggle的总结**
```
 $("div").toggleClass("current");  //class的开关
 $("div").toggle(2000);//显示隐藏开关
 $("div").slideToggle(1000);//滑动的开发
```
**自定义动画**
 ```
 $("div").animate({"display":"none","opacity":0,"width":0,"height":0},2000);
 ```
 animate的使用
 参数一：样式
 参数二：时间
 ```
 $("div").animate(json,1000, function () {
  $("div").animate(json2,1000, function () {
        alert("动画执行完毕！");
   });
});
 ```
 **停止动画**
 ```
 $("div").stop();   //都不写，默认两个都是false;
 // 第一个参数表示后续动画是否要执行
 //（true:后续动画不执行  ;false:后续动画会执行）
 // 第二个参数表示当前动画是否执行完
 //（true:立即执行完成当前动画  ;false:立即停止当前动画）
//四种情况：情况1：true,true
//（后续动画不执行，立即执行完成当前动画）
//$("div").stop(true,true);
//四种情况：情况2：false,true
//（后续动画会执行，立即执行完成当前动画）
//$("div").stop(false,true);
//四种情况：情况3：true,false
//（后续动画不执行，立即停止当前动画`）
//$("div").stop(true,false)
//四种情况：情况4：true,false
//（后续动画会执行，立即停止当前动画`）
//$("div").stop(false,false);
 ```
 **创建标签**
 ```
 $("<li class='aaa'>我是li标签</li>")
 ```
 类似于
 ```
  document.createElement("li");
 ```
 创建方式二
 ```
 $("ul").html("");
 ```
 类似于
 ```
  $("ul").html("<li>我是html方法穿件出来的li标签</li>")
 ```
 **案例**
 ```
 创建标签
 var jqNewLi = $("<li>我是jquery创建出来的li。用的是append方法添加</li>");
 //$("ul").append(jqNewLi);   //把新创建的li塞进ul中
//jqNewLi.appendTo($("ul"));  //把新创建的li塞进ul中
//在盒子最前面添加
//$("ul").prepend(jqNewLi);
//jqNewLi.prependTo($("ul"));
//下面两个方法是操作兄弟元素的。放在兄弟元素之后或者之前
//after();
//$("li").after(jqNewLi);
 //before();
  $("li").before(jqNewLi);
```
**清空标签**
```
$("ul").empty();  //获取标签，执行entry方法
自杀式删除
  $("button").eq(1).click(function () {
     //删除指定的li。  ---  自杀！
     $("li:eq(0)").remove();
  })
```
**复制节点**
```
 var newUl  = $(".box ul").clone();
 $(".box").append(newUl);
```
**案例切水果**
```
它的执行方式是：
	首先将需要移动的选中，加到需要添加的一方
```
**案例动态添加数据**
```
 for(var i=0;i<data.length;i++){
     //如何生成3组？？？
     str += "<tr><td>1</td><td>2</td><td>3</td></tr>";
     //data[i] = 数组中的每一个json
     //data[i].name = 数组中的每一个json的name属性值
     str += "<tr><td>"+data[i].name+"</td><td>"+data[i].url+"</td><td>"+data[i].type+"</td></tr>";
 }
```
**JQuery的属性操作**
```
定位元素
var jqinp = $("input").eq(0);
var jqinp2 = $("input:checkbox");
var jqbtn = $("button");
```

```
绑定到标签上
jqinp.attr("title",111);
```
特殊的属性
```
 //form中的特殊属性，用prop
 jqinp2.prop("checked",true);
//jqinp2.attr("checked",true);//一次性的
```