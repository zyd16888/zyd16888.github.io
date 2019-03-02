---
title: 深入理解python语言（绘制蟒蛇）
copyright: true
abbrlink: fa0e7c88
tags:
  - python
categories: python
date: 2018-06-10 11:53:22
password:
---

{% meting "108428" "netease" "song"  "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}

## turtle库的使用
+ turtle绘图体系的python实现
	+ 标准库
	+ 入门图形绘制函数

+ 绘制窗体
	+ 单位：像素
	+ 启动窗体的位置大小： turtle.setup(weight,height,startx,starty)

+ 空间坐标体系
	+ 坐标位置：中心为（0，0）左x轴，右y轴
	+ 直线：turtle.goto(x,y)
	+ 海龟坐标：
		+ 无论朝向哪个角度都为前进方向，左侧为左侧方向，右侧为右侧方向
		+ turtle.fd(d)  #向海龟的正前方向运行
		+ turtle.bk(d) #向海龟的正后方向运行
		+ turtle.circle(r,angle) #以海龟当前位置左侧的一个点为圆心曲线运行
			+ turtle.circle(40,80) #以40像素为半径绘制80°的弧线

+ 角度坐标体系
	+ x轴正方向为0°，y轴正方向为90°
	+ turtle.seth(angle) 改变当前海龟的行进角度，不绘制信息
	+ 当前海龟向左或向右变向
		+ turtle.left(angle)
		+ turtle.right(angle)
			+ angel 旋转角度

+ RGB色彩体系
	+ turtle.colormode(mode)
		+ 1.0：RGB小数值模式
		+ 255：RGB整数值模式
		
+ 方向控制函数
	+ turtle.seth(45)
	+ turtle.left(angle)
	+ turtle.right(angle)

+ 画笔控制函数
	+ 画笔操作后一直有效，一般成对出现
		+ turtle.penup()  简写  turtle.pu()
			+ 画笔抬起，海龟飞行
		+ turtle.pendown()  简写   turtle.pd()
			+ 落下画笔，海龟爬行
	+ turtle.pencolor(color)
		+ 颜色字符串：turtle.pencolor("purple")
		+ RGB小数值：turtle.pencolor(0.63,0.13,0.94)
		+ RGB元组值：turtle.pencolor((0.63,0.13,0.94))
	+ turtle.pensize()
		+ 画笔宽度

+ 运动控制函数
	+ turtle.forward(0)  简写  turtle.fd(d)
		+ 向前行进，海龟走直线
		+ d 行进距离，可以为负数
		
	+ turtle.circle(r,extent=None) 
		+ 根据半径r绘制extent角度的弧形
		+ r默认圆心在海龟左侧r距离的位置
		+ extent绘制弧度，默认为360°
        
+ import 用法
	+ import<库名>
		+ <库名>.<函数名>(<函数参数>)

	+ from<库名>import<函数名>
	+ from<库名>import *
	+ <函数名>(<函数参数>)
	+ import<库名>as<库别名>	
	+ <库别名>.<函数名>

+ 循环语句
	+ for <变量> in range(<函数名>) 
		+ <被执行的循环语句>
	- <变量>表示每次循环的计数，0到<次数>-1
	```python
	for i in range(5)
		print("hello:",i)
	```
	+ range()函数
		+ 产生循环计数序列
		- range(N)
			- 产生0到N-1的整数序列，共N个
		- range(M,N)
			- 产生 M 到 N-1 的整数序列，共 N-M个

## 附
```python
import turtle
turtle.setup(650,350,200,200)
turtle.penup()
turtle.fd(-250)
turtle.pendown()
turtle.pensize(25)
turtle.pencolor("green")
turtle.seth(-40)
for i in range(4):
    turtle.circle(40,80)
    turtle.circle(-40,80)
turtle.circle(40,80/2)
turtle.fd(40)
turtle.circle(16,180)
turtle.fd(40 * 2/3)
turtle.done()


```
			