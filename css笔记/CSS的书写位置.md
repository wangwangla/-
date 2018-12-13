---
title: CSS的书写位置
user: 见贤思齐
date: 2018-12-13
---

#### 书写位置

 - 行内写法
 - 外部写法
 - 本页面中写

#### 举例

行内：
``` css
<h1 style="font-size:30px; color:red;">test</h1>
```
外链式
```css
	<link rel="stylesheet" href="test.css">
```
本页面中写
```
<style type="text/css">
 .box{
	width: 300px;
	height: 100px;
	background-color: #888;
 }
 .box p{
	height: 50px;
	background-color: red;
 }

</style>
```
