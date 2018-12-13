---
title: CSS笔记--选择器
user: 见贤思齐
date: 2018-12-12
---

### mate的使用
``` html
<meta charset="UTF-8">
	<title>Document</title>
	<meta name="keywords" content="java培训,大前端培训">
	<meta name="description" content="据说中国口碑最好的IT培训机构！">
	<meta http-equiv="refresh" content="5; http://www.itcast.cn">
	<link rel="stylesheet" href="1.css">
	<link rel="icon" href="favicon.ico">
```
keywords：为了可以方便速索
description：是网站的描述信息
refresh：页面刷新，内容是数字；地址，多久之后跳转到这个地址。

### css的外部引入

``` css
	<link rel="stylesheet" href="1.css">
	<link rel="icon" href="favicon.ico">
```
### 表格

``` html
	<table width="400" height="400" border="1" cellspacing="0" align="center" bgcolor="pink">
		<tr>
			<th colspan="2">京东会员</th>
			<!-- <td></td> -->
		</tr>
		<tr>
			<td>用户名:</td>
			<td><input type="text" value="请输入用户名" maxlength="6"><font color="red" size="2">最多输入6个字符</font></td>
		</tr>
		<tr>
			<td>密 码:</td>
			<td><input type="password"  maxlength="6"><font color="red" size="2">最多输入6个字符</font></td>
		</tr>
		<tr>
			<td>验证码:</td>
			<td><input type="text"><br><br><img src="作业/yzm.jpg" width="100"></td>
		</tr>
		<tr>
			<td align="center" colspan="2"><a href="dl.html">登录</a>|<a href="zc.html">注册用户</a></td>
			<!-- <td></td> -->
		</tr>
	</table>
```
 介绍：

 1.  table：设置长和高 	
 2.  背景色（bgcolor）
 3.  colspan:合并列

### 选择器

 1. 标签选择器 
 2. 类选择器 
 3. id选择器


###### 案例
```
	<style type="text/css">
		类选择器
		.G{
			font-size: 200px;//字体大小和颜色
			color: #000099;
		}
		.o1{
			font-size: 200px;
			color: #990000;
		}
		.o2{
			font-size: 200px;
			color: orange;
		}
		.g1{
			font-size: 200px;
			color: #000099;
		}
		.l{
			font-size: 200px;
			color: #009900;
		}
		.e{
			font-size: 200px;
			color: #990000;
		}


	</style>
</head>
<body>
	<span class="G">G</span>
	<span class="o1">o</span>
	<span class="o2">o</span>
	<span class="g1">g</span>
	<span class="l">l</span>
	<span class="e">e</span>
</body>
```
### 通配符选择器
```
*{
		font-size: 100px;
		color: red;

	}
```
### 交集选择器
```
div.test[标签+类选择器]
div#test[标签+id选择器]

```
### 后代选择器
```
类选择器
/*.box{
 	font-size:40px;
	color:red;
}
后代选择器[标签+标签]
 div span{
   	font-size: 50px;
 }*/
 类+标签
  /*.box span{
   	background-color: blue;
 }*/
 /* .box .miss{
     	color:red;
   }*/
     .box span{
     	color:red;
     }
```

### 子代选择器
```
div>span{
		color:red;
		font-size:40px;
	}
p>span{
	color:green;
	font-size:60px;
}
```

子代和后带的区别就是，后代不论隔了多少代，子代仅仅是一代。
### 并集选择器
```
.box,#miss,span,h1{
	font-size:100px;
	color: #fff;
	background-color: green;
}
```
#### 选择器的优先级

默认样式<标签选择器<类选择器<id选择器<行内样式<!important
  0         1          10       100       1000    1000以上
  
  优先级是可以叠加的。