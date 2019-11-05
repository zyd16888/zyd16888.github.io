---
title: JavaWeb复习笔记
copyright: true
abbrlink: 7e6d3dbd
notshow: false
tags:
  - Java
  - 学习
categories: Java
description: 完全根据PPT复习范围整理，如发现错误请在评论区留言，会及时修改
image:
  - 'https://data.singlelovely.cn/CoverPicture/3c115208.jpg!CoverPicture'
date: 2019-05-29 00:20:00
password:
photos:
sticky:
---

{% meting "40962509" "netease" "playlist" "mutex:true" "listmaxheight:340px" "preload:none" "theme:#00CED1" %}

## 第一章开发任务概述

### Web应用

- B/S结构：适用于大中型应用程序，极少事务逻辑在前端(Browser)实现，主要事务逻辑在服务器端(Server)实现。这种结构的程序简化了客户端的功能负载，减轻了应用维护与升级的成本和工作量，降低了用户的总体成本，但应用服务器运行负荷较重。

### 客户端开发技术

1、HTML技术

HTML(HyperText Markup Language，超文本标记语言）是一种用于表示网上信息的符号标记语言。

2、CSS技术

CSS(Cascading Style Sheets，层叠样式表）技术是一种定义样式结构（如字体、颜色、位置等）的语言，用于描述网页上的信息格式和显示的方式。

 3、JavaScript技术

JavaScript是一种广泛应用于客户端的脚本语言，通过嵌入到HTML中来实现自身的功能；通过控制网页元素的行为和CSS代码中的样式定义，为网页增添了诸如表单内容验证、动画显示效果等交互能力，可以使静态网页具备一定的动态效果。
服务器端开发技术

### 服务器端开发技术

1、Servlet技术
<p id = "div-border-left-yellow">
Servlet是以Java技术为基础的服务器端应用程序组件，与运行在浏览器端的Applet相对应。Serv」et是被Web服务器（如Tomcat)加载和执行，而Applet则是被浏览器加载和执行。Servlet通过Web服务器接收客户端浏览器发来的请求，执行预定的功能，然后将执行结果返回给客户端的浏览器。Servlet可以使用服务器端的所有Java 类库资源，所以理论上其功能可以无限扩展。
</p>
2、JSP技术
<p id = "div-border-left-yellow">
JSP(Java Server Page)是建立在Servlet规范提供的功能之上的一种动态网页技术。
</p>
3、JavaBean技术
<p id = "div-border-left-yellow">
JavaBean是Java组件技术的核心，它是Java平台上实现重用的软件组件模型。JavaBean是一种特殊的Java类，需要满足一定的规范要求。
</p>
4、JDBC技术
<p id = "div-border-left-yellow">
JDBC(Java DataBase Connectivity)是一种用于执行SQL语句的Java API （Application Programming Interface，应用编程接口)，由一组Java语言编写的类和接口组成。
</p>

### HTTP请求/响应机制

处理过程包括以下步骤：

- 浏览器向Web服务器发送请求报文。
- 服务器解析接收到的请求，定位请求资源，做相应处理，然后封装好响应报文，回送给浏览器。
- 浏览器收到响应报文，解析HTML、图片等静态内容，渲染网页呈现给用户，解析DOM(Document Object Model，文档对象模型）树，脚本引擎执行脚本代码，完成DOM 操作、CSS属性更改、发送AJAX(Asynchronous JavaScript And XML，异步JavaScript 和XML)请求等功能。

<span id = "font-green">HTTP主要有以下特点：</span>

- 简单快速<br>
- 灵活<br>
- 无连接<br>
- 无状态<br>
- 支持B/S及C/S模式

## 第二章 用户界面设计

### 用户界面元素开发

```html
<!-- 无序列表 -->
<ul>
    <li>Coffee</li>
    <li>Milk</li>
</ul>
<!-- 文本段落 -->
<p>This is a paragraph</p>
<p>This is another paragraph</p>
<!-- 块、行内元素、图片 -->
<div>
<span>
<img src="boat.gif" alt="Big Boat">
<!-- 表单  -->
<form>
 First name:<br>
<input type="text" name="firstname">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form>
<!-- 下拉列表框  -->
<select>
  <option value ="volvo">Volvo</option>
  <option value ="saab">Saab</option>
  <option value="opel">Opel</option>
  <option value="audi">Audi</option>
</select>
<!--多行文本框-->
<textarea rows="3" cols="20">
    在w3school，你可以找到你所需要的所有的网站建设教程。
</textarea>
<!--表格-->
<table border="1">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>
<!-- 超链接 -->
<a href="http://www.w3school.com.cn">W3School</a>
<!-- HTML文件的基本结构、HTML标记格式 -->
略
```

### 界面布局设计

#### 什么是css

CSS是Cascading Style Sheets(层叠样式表）的缩写，是一种美化网页的技术。它的引入使HTML网页美工设计不再烦琐。

#### CSS选择器格式

1、标记选择器：直接针对HTML标记定义样式。
<div class="note info">
HTML标记名{标记属性：属性值; 标记属性：属性值; 标记属性: 属性值;...}
</div>
2、类别选择器：
<div class="note info">
.类别选择器名{标记属性: 属性值; 标记属性: 属性值; 标记属性: 属性值;...;}
<HTML 标记名 class = "类别选择器名">
</div>
3、ID选择器：
<div class="note info">
#ID选择器名{标记属性：属性值; 标记属性: 属性值; 标记属性: 属性值;...;}
<HTML 标记名 id="ID选择器名">
</div>
4、伪元素选择器：指对同一HTML元素的各种状态来定义样式的一种方式。
<div class="note info">
HTML标记：伪元素{样式}
</div>

#### 在HTML中使用CSS的方法

1、嵌入式：将样式表嵌入到HTML标记的属性中，把样式的定义直接作为标记的style属性值。格式如下：

```html
    <HTML 标记 style = "属性名：属性值">
```

(2)头部式：把样式定义在HTML页面的头部，用\<style>标记进行声明。这样定义的样式在整个页面中都可以使用。基本格式如下：

```html
    <style>
        样式定义
    </style>
```

(3)外部式：当在很多网页里都要使用相同的样式时，可以使用外部样式表的形式。

```html
< link href= "" rel= "stylesheet"  type= "text/css"  />
```

#### DIV+CSS布局的实现思路

可以使用DIV+CSS 来实现网页布局，实现路是先用\<div>标记对整个页面进行分块，然后再利用CSS样式对每个div分块进行布局设置，最后在各个div分块中添加内容。

### 客户端功能开发

#### JavaScript概述

JavaScript是一种简单的脚本语言，由浏览器解释执行，简单、易学、易用。其最基本的两个特点是基于对象和事件驱动。

所谓基于对象，是指JavaScript支持使用对象，但是没有提供面向对象语言的所有功能，不是完全的面向对象编程语言。

事件驱动指JavaScript程序的运行机制。它把GUl(图形用户界面）中的用户动作封装为各种事件，例如单击按钮、移动鼠标、按下键盘等都是事件，当某个事件发生时，就会触发相应的事件处理程序运行。

#### JavaScript脚本的使用方式

JavaScript代码可以直接嵌入到HTML文件中使用，嵌入方式主要有三种：嵌入标记事件属性、使用脚本语句块、链接独立的脚本文件。

#### 对象

JavaScript中的对象由属性和方法构成，主要有三种类型：内置对象、浏览器提供的对象和自定义对象。

- Date对象：用于处理日期和时间，需要先创建才能使用。
- window对象：代表当前浏览器窗口所有JavaScript全局对象、函数和变量均自动成为window对象的成员。
    - window对象提供了多个属性和函数用于对浏览器窗口进行操作。
    - window对象的常用函数有：alert(警告对话框)、confirm(确认对话框）、prompt(消息框)、open(打开新窗口）、print(打印网页内容）等。
    - 因为window对象是JavaScript中最顶级的对象，所以在使用当前窗口对象的函数时，可以省略函数前的window，即可以直接使用alert()，而不需要用window.alert()。
- document对象：属于HTML DOM(Document Object Model，文档对象模型）。当网页被加载时，浏览器会创建当前页面的DOM模型。DOM的最顶层就是HTML文档，document对象就代表当前HTML文档，通过它可以访问页面中的所有元素。

<span id = "font-blue"><span id = "font-green">document</span>对象的常用方法如下:</span>

- write(字符串）：将字符串或数值显示在显示器上。
- getElementById()：返回对指定id的第一个对象的引用。

## 第三章 web应用开发基础

### 开发环境和运行环境

略

### jsp基本概念

#### 运行机制

当浏览器向服务器发出请求访问一个JSP页面时，所请求的JSP文件会被服务器端的JSP引擎转化为一个Java类，并被编译成一个字节码文件，再装载到Java虚拟机中运行，最后把运行产生的输出作为对本次请求的响应返回给浏览器。

#### Web应用目录结构

按照Java EE规范的规定，一个典型的Java Web应用包含四个部分：

- 公开文件夹，存放能够被用户访问的资源，包括.jsp、.htm、.js、.css、.jpg等文件。
- WEB-INF/web.xml文件，应用的部署描述文件。
- WEB-INF/classes文件夹，存放编译好的Java类文件(.class)。
- WEB-INF/lib文件夹，存放Java类库文件(.jar)。

### jsp基础语法

jap脚本代码：Java代码片段，可以实现业务逻辑处理，也可以产生输出。例如：

```java
<%
    SimpleDateFormat df = new SimpleDateFormat("yyyy-M-d HH:mm:ss");
%>
```

jsp声明：在声明中定义的变量和方法都会成为转义后的Java类的成员变量及类成员方法，声明的类则成为内部类。语法格式如下：

```java
    <%! 变量或方法、类的声明 %>
```

jsp表达式：一种简单的输出形式。

```java
    <% = 表达式 %>
```

#### jsp指令

<span id = "font-red">page指令</span>称为页面指令，用来定义JSP页面的全局属性，该配置会作用于整个页面。

- <span id = "font-purple">language</span>属性：设置当前页面中编写JSP脚本使用的语言，默认值为java。
- <span id = "font-purple">import</span>属性：用来导入程序中要用到的包或类，可以有多个值，无论是Java核心包中自带的类还是用户自行编写的类，都要在import中引入，才能使用。
- <span id = "font-purple">errorPage</span>属性：用于指示一个JSP文件的相对路径，以便在页面出错时，转到这个JSP文件来进行处理。与此相适应，需要将这个JSP文件的isErrorPage属性设为true。
- <span id = "font-purple">isErrorPage</span>属性：指示一个页面是否为错误处理页面。设置为true时，在这个JSP页面中的内建对象exception将被定义，其值将被设定为呼叫此页面的JSP页面的错误对象，以处理该页面所产生的错误。
- <span id = "font-purple">contentType</span>属性：设置发送到客户端文档的响应报头的MIME（Multipurpose Internet Mail Extention）类型和字符编码。
- <span id = "font-purple">pageEncoding</span>属性：设置JSP页面字符的编码，常见的编码类型有ISO-8859-1、gb2312和GBK等。默认值为ISO-8859-1。

用法示例：

```jsp
<%@page language="java" %>
<%@page import="包名.类名"%>
<%@page import="包名.*"%>
<%@ page pageEncoding="gb2312"%>
```

<span id = "font-red">include指令</span>：在JSP中，可以使用include指令来包含其他jsp文件。

<span id = "font-red">taglib指令</span>：声明用户使用自定义的标签，将标签库描述符文件导入到jsp页面。

```jsp
 <%@ taglib (uri="tigLibURL" 或 tagDir="tagDir") prefix="tagPrefix" %>
```

属性：

- <span id = "font-purple">uri</span>属性:定位标签库描述符的位置。唯一标识和前缀相关的标签库描述符，可以使用绝对或相对URL。
- <span id = "font-purple">tagDir</span>属性：指示前缀将被用于标识在WEV-INF/tags目录下的标签文件。
- <span id = "font-purple">prefix</span>属性：标签的前缀，区分多个自定义标签。不可以使用保留前缀和空前缀，遵循XML命名空间的命名约定。

#### JSP标记

<span id = "font-green">\<jsp:include></span>用于将HTML或者jsp动态内容插入到当前的jsp页面中。

<span id = "font-green">\<jsp:param></span>用于向被包含的页面传递参数。

<span id = "font-green">\<jsp:forward></span>用于实现页面请求的转发，可以把对当前jsp页面的请求转发到同一web应用中的另一个资源。

```jsp
<%@include file="文件的URL"%>
<jsp:forward page="接受参数页面的URL">
    <jsp:param name=“参数名 value = "参数值"/>
<jsp:forward/>

```

## 第四章 流程控制与数据传递

### jsp内置对象

|内置对象名称|类型|作用域|用途|
|---|:--:|:---|---|
|request|javax.servlet.httpServletRequest|Request|代表了客户端的请求信息，接受通过HTTP协议传送到服务器的数据。(乱码处理)|
|response|javax.servlet.http.HttpServletResponse|Page|对客户端的响应，将JSP容器处理过的对象传回到客户端。(页面重定向)|
|session|javax.servlet.http.HttpSession|Page|在第一个JSP页面被装载时自动创建，完成会话期管理。（存取属性值，保存用户的信息）|
|out|javax.servlet.jsp.jspWriter|Page|在Web浏览器内输出信息，并且管理应用服务器上的输出缓冲区。|

**<center><span id = "font-blue">request对象主要方法</span></center>**

|方法声明|功能简介|
|:---|:---|
setAttribute(String name,Object) | 设置名字为name的request的參数值
getAttribute(String name) | 返回由name指定的属性值
getAttributeNames() | 返回request对象全部属性的名字集合，结果是一个枚举的实例
getCookies() | 返回client的全部Cookie对象，结果是一个Cookie数组
getCharacterEncoding() | 返回请求中的字符编码方式
getContentLength() | 返回请求的Body的长度
getHeader(String name) | 获得HTTP协议定义的文件头信息
getHeaders(String name) | 返回指定名字的request Header的全部值，结果是一个枚举的实例
getHeaderNames() | 返回所以request Header的名字，结果是一个枚举的实例
getInputStream() | 返回请求的输入流，用于获得请求中的数据
getMethod() | 获得client向server端传送数据的方法
getParameter(String name) | 获得client传送给server端的有name指定的參数值
getParameterNames() | 获得client传送给server端的全部參数的名字，结果是一个枚举的实例
getParameterValues(String name) | 获得有name指定的參数的全部值
getProtocol() | 获取client向server端传送数据所根据的协议名称
getQueryString() | 获得查询字符串
getRequestURI() | 获取发出请求字符串的client地址
getRemoteAddr() | 获取client的IP地址
getRemoteHost() | 获取client的名字
getSession([Boolean create]) | 返回和请求相关Session
getServerName() | 获取server的名字
getServletPath() | 获取client所请求的脚本文件的路径
getServerPort() | 获取server的port号
removeAttribute(String name) | 删除请求中的一个属性

**<center><span id = "font-blue">response对象常用方法</span></center>**

|方法声明|功能简介|
|:---|:---|
void setContentType(String type) | 设置响应数据的MIME类型
String getContentType() | 取得响应数据的MIME类型
void setHeader(String name, String value) | 设置指定的响应报头
void sendRedirect() | 重定向客户的请求到指定页面
void addCookie(Cookie cookie) | 给客户端添加一个Cookie对象，以保存客户端的信息
PrintWriter getWriter() | 返回一个输出字符流
void flushBuffer() | 清空缓冲区，强行把Buffer的内容写到客户端浏览器

**<center><span id = "font-blue">session对象常用方法</span></center>**

|方法声明|功能简介|
|:---|:---|
getAttribute(String name) | 获取session对象中名为name的属性值，不存在则为null
removeAttribute(String name) | 删除session对象中名为name的属性
setAttribute(String name, Object value) | 设置session对象属性，属性名为name，属性值为value
getCreationTime() | 获取session对象的创建时间，返回1970年1月1日至今的毫秒数（Unix时间戳）
getLastAccessTime() | 获取session对象对应客户端的最近发送请求的时间，返回1970年1月1日至今的毫秒数
invalidate() | 销毁session对象中的信息，session本身不会被销毁
getMaxInactiveInterval() | 获取会话超时时间，单位为秒
setMaxInactiveInterval(int interval) | 设置会话超时时间，单位为秒

### Cookie机制

Cookie是Web服务器产生并嵌入在HTTP响应报头中的一小段文本。浏览器在收到一个Cookie后会把它保存到特定的文件夹下，并在接下来再次访问同一个Web服务器时，自动在请求报头中携带该Cookie，供服务器读取使用，从而弥补HTTP无状态的不足。基于这一工作机制，可以实现用户识别、应用定制等功能。

一个Cookie包含一个名称和值，以及一些可选的属性，如路径、最长存活时间等。Java提供了javax.servlet.http.Cookie类来支持Cookie机制的实现。可以使用response 对象的addCookie()方法向浏览器发送Cookie，使用request对象的getCookie()方法获取请求中的所有Cookie。

**<center><span id = "font-blue">cookie类的主要方法</span></center>**

|方法声明|功能简介|
|:---|:---|
String geyName() | 获取cookie的名称
String getValue() | 获取cookie的值
void setValue(String value) | 在cookie创建后，为cookie赋予新的值
int getMaxAge() | 获取cookie的有效时间，以秒为单位，-1表示cookie将一直持续下去，直到浏览器关闭
String getPath() | 返回cookie适用的路径
void setPath(String uri) | 设置cookie的适用路径。如不指定，则当前页面的同目录与子目录下所有RRL都返回cookie

### 控制流和数据流的实现

1、jsp页面间的流程控制

- 超链接
- 表单提交
- 页面重定向
- 请求转发

2、jsp页面间的数据传递

- 表单传参
- url传参
- <jsp:param>标记传参
- 作用域传参

## 数据库访问

### 数据库访问代码模板

```jsp
<%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>
<%@ page import="java.sql.*" %>

<%

    String driver = "com.mysql.jdbc.Driver";

    // URL指向要访问的数据库名test1
    String url = "jdbc:mysql://127.0.0.1:3306/test";

    // MySQL配置时的用户名
    String user = "root";

    // Java连接MySQL配置时的密码
    String password = "111";

    try {
        // 1 加载驱动程序
        Class.forName(driver);

        // 2 连接数据库
        Connection conn = DriverManager.getConnection(url, user, password);

        // 3 用来执行SQL语句
        Statement statement = conn.createStatement();

        // 要执行的SQL语句
        String sql = "select * from login";

        //处理执行结果
        ResultSet rs = statement.executeQuery(sql);
        String name = null;
        String mima=null;
        while (rs.next()) { 
        name = rs.getString("userName"); 
        mima = rs.getString("passWord"); 
        out.println(name+"\t"+mima); 
        }
        rs.close();
        conn.close();
    } catch (ClassNotFoundException e) {
        System.out.println("Sorry,can`t find the Driver!");
        e.printStackTrace();
    } catch (SQLException e) {
        e.printStackTrace();
    } catch (Exception e) {
        e.printStackTrace();
    }

%>

```

### JDBC技术

#### 基础概念

Java语言访问数据库的一种规范,是一套API

JDBC (Java Database Connectivity) API，即Java数据库编程接口，是一组标准的Java语言中的接口和类，使用这些接口和类，Java客户端程序可以访问各种不同类型的数据库。比如建立数据库连接、执行SQL语句进行数据的存取操作。

#### DriverManager类

处理驱动程序的加载和建立新数据连接。

```java
connection.getConnection(String url, String user, String password)
Connection con = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:name", "scott","tiger");
```

#### Connection接口

代表Java程序与数据库间的连接，用于提供创建语句以及管理连接及其属性方法。

**<center><span id = "font-blue">Connection接口常用方法</span></center>**

|方法声明|功能简介|
|:---|:---|
Statement createStatement() | 创建一个Statement对象，用于将SQL语句发送到数据库，通常在执行无参数的SQL语句时创建该实例
PrepareStatement prepareStatement() | 通常在执行包含参数的SQL语句时创建该实例，并对SQL语句进行预编译处理
void close() | 关闭数据库连接

```java
 Statement st = con.createStatement();
```

#### Statement接口

用于执行静态SQL语句并返回它所生成结果的对象。

**<center><span id = "font-blue">Statement接口常用方法</span></center>**

|方法声明|功能简介|
|:---|:---|
ResultSet executeQuery(String sql) | 执行指定的静态select语句，并返回一个永远不为null的ResultSet实例
int executeUpdate(String sql) | 执行指定的静态INSET、UPDATE或DELETE语句，并返回一个int型数值，未同步更新记录的条数

```java
 ResultSet rs = st.executeQuery(sql);
```

#### PreparedStatement接口

继承自Statement，表示预编译的SQL语句的对象，预编译SQL效率高且支持参数查询

#### ResultSet接口

用于表示数据库结果集的数据表，通常由执行查询数据库的语句生成，其中存放了查询结果。

在ResultSet对象中具有指向当前数据行的游标，可以在<span id = "font-green">while</span>循环中使用<span id = "font-green">next()</span>方法来迭代处理结果集。

**<center><span id = "font-blue">ResultSet接口常用的获取列值方法</span></center>**

|返回类型|方法名称|返回类型|方法名称|
|:---|:---|:---|:---|
byte | getByte(inc columnIndex) | byte | getByte(String columnLabel)
Date | getDate(inc columnIndex) | Date | getDate(String columnLabel)
double | getDouble(inc columnIndex) | double | getDouble(String columnLabel)
float | getFloat(inc columnIndex) | float | getFloat(String columnLabel)
int | getInt(inc columnIndex) | int | getInt(String columnLabel)
long | getLong(inc columnIndex) | long | getLong(String columnLabel)
String | getString(inc columnIndex) | String | getString(String columnLabel)

```java
while(rs.next()){
    int id = rs.getInt("id");
    String username = rs.getString("username");
    String gender = rs.getString("gender");
    java.sql.Date hiredate = rs.getDate("hiredate");
    System.out.println(id+"#"+username+"#"+gender+"+hiredate);
}
```

## 重构程序功能

### JavaBean技术

#### JavaBean编写规范

- 是一个公共类
- 具有无参数的公共构造方法
- 具有公共的setter和getter方法来供外部存取其私有属性
- 需要放在命名包里，不能放在默认包中

#### JavaBean的编译

略

#### 使用JavaBean

- <span id = "font-green">\<jsp:useBean></span> 装载一个将在JSP页面中使用的JavaBean。
    - scope，作用域

```jsp
<jsp:useBean id="name" class="package.class"   scope="page | request | session | application" />  
```

- <span id = "font-green">\<jsp:setProperty></span> 获取指定的JavaBean的值。
    - 详解见[jsp:useBean的用法](https://blog.csdn.net/u011024652/article/details/52012435)

```jsp
//自动匹配赋值
<jsp:setProperty name="JavaBean实例名" property="*" />
//自动匹配指定属性
<jsp:setProperty name="JavaBean实例名" property="JavaBean属性名" />
//手动设置属性值
<jsp:setProperty name="JavaBean实例名" property="JavaBean属性名" value="BeanValue" />
//通过获取request的参数来为相应的属性赋值，其中param为参数名
<jsp:setProperty name="JavaBean实例名" property="JavaBean属性名" param="request对象中的参数名" />
```

- <span id = "font-green">\<jsp:getProperty></span> 获取指定Javabean对象的属性值。

#### JavaBean实例

```jsp login.jsp
<%@ page language="java" import="java.util.*" contentType="text/html; charset=utf-8" %>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    <title>My JSP 'login.jsp' starting page</title>
        <meta http-equiv="pragma" content="no-cache">
        <meta http-equiv="cache-control" content="no-cache">
        <meta http-equiv="expires" content="0">   
        <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
        <meta http-equiv="description" content="This is my page"> 
  </head>
  <body>
    <h1>系统登录</h1>
    <hr>
    <form name="loginForm" action="dologin.jsp?mypass=999999" method="post">
      <table>
        <tr>
          <td>用户名：</td>
          <td><input type="text" name="username" value=""/></td>
        </tr>
        <tr>
          <td>密码：</td>
          <td><input type="password" name="password" value=""/></td>
        </tr>
        <tr>
          <td colspan="2" align="center"><input type="submit" value="登录"/></td>
        </tr>
      </table>
    </form>
  </body>
</html>
```

```jsp dologin.jsp
<%@ page language="java" import="java.util.*" contentType="text/html; charset=utf-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">

    <title>My JSP 'dologin.jsp' starting page</title>

        <meta http-equiv="pragma" content="no-cache">
        <meta http-equiv="cache-control" content="no-cache">
        <meta http-equiv="expires" content="0">   
        <meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
        <meta http-equiv="description" content="This is my page">

  </head>
  <body>
    <jsp:useBean id="myUsers" class="com.po.Users" scope="page"/>
    <h1>setProperty动作元素</h1>
    <hr>
   <!--根据表单自动匹配所有的属性 -->
   <jsp:setProperty name="myUsers" property="*"/> 

   <!--根据表单匹配所有部分的属性 -->
   <jsp:setProperty name="myUsers" property="username"/> 

   <!--根表单无关，通过手工赋值给属性 -->
   <jsp:setProperty name="myUsers" property="username" value="lisi"/>
   <jsp:setProperty name="myUsers" property="password" value="888888"/>

   <!--通过URL传参数给属性赋值 -->
   <jsp:setProperty name="myUsers" property="username"/>
   <jsp:setProperty name="myUsers" property="password" param="mypass"/>

   <!-- 使用传统的表达式方式来获取用户名和密码 -->
       用户名：<%=myUsers.getUsername() %><br>
       密码：<%=myUsers.getPassword() %><br>

   <!-- 使用getProperty方式来获取用户名和密码 -->
      用户名：<jsp:getProperty name="myUsers" property="username"/> <br>
      密码：<jsp:getProperty name="myUsers" property="password"/><br>
   <br>
   <br>
  </body>
</html>
```

## 重构程序界面

### EL和JSTL

EL语法格式

     ${EL表达式}

运算符：略

**<center><span id = "font-blue">EL常用内置对象</span></center>**

|内置对象|描述|
|:---|:---|
pageScope | 取得 page 范围的属性名称所对应的值，${pageScope.name}等同与pageContext.getAttribute(“name”);
requstScope | 取得 request 范围的属性名称所对应的值，${requestScope.name}等同与request.getAttribute(“name”)；
sessionScope | 取得 session 范围的属性名称所对应的值，${sessionScope.name}等同与session.getAttribute(“name”)；
applicationScope | 取得 application 范围的属性名称所对应的值，${applicationScope.name}等同与application.getAttribute(“name”)；
param | 可以用来获取参数，${param.username} 等同于request.getParameter("username"); 返回 Slring[] 类型的值
paramValues | ${paramValues.hobby} 如同 ServletRequest.getParameter Values(String name)， 返回 string[] 类型的值

<span id = "inline-blue">在JSP中使用JSTL的步骤如下</span>
<p id = "div-border-left-purple">
1. 首先需要到http：//tomcat.apache.org/taglibs/standard/ 下载JSTL标记库的jar包。<br>
2. 然后将获取到的JSTL标记库的jar包，复制到Web应用中的WEB-INF\lib文件夹下。<br>
3. 最后在JSP页面中用taglib指令设置标记前缀，即可使用JSTL标记。<br>
</p>
JSTL标记：

- <span id = "font-green">\<c:out></span> 用来显示一个表达式的结果，与<%= %>作用相似，它们的区别就是<c:out>标签可以直接通过"."操作符来访问属性
    - <span id = "font-purple">value</span>：要输出的内容，必须
    - <span id = "font-purple">default</span>：输出的默认值，非必须，默认为主体中的内容
    - <span id = "font-purple">escapeXml</span>：是否忽略XML特殊字符，非必须，默认为true

```jsp
<c:out value="<string>" default="<string>" escapeXml="<true|false>"/>
```

- <span id = "font-green">\<c:set></span> 用于设置变量值和对象属性。
    - <span id = "font-purple">value</span>：要存储的值，非必须，默认为主体的内容
    - <span id = "font-purple">target</span>：要修改的属性所属的对象，非必须
    - <span id = "font-purple">property</span>：要修改的属性，非必须
    - <span id = "font-purple">var</span>：存储信息的变量，非必须
    - <span id = "font-purple">scope</span>：var属性的作用域，非必须，默认为Page
<div class="note warning">如果指定了target属性，那么property属性也需要被指定。</div>

```jsp
<c:set var="<string>" value="<string>"   target="<string>"   property="<string>"   scope="<string>"/>
```

- <span id = "font-green">\<c:if></span> 判断表达式的值，如果表达式的值为 true 则执行其主体内容。
    - <span id = "font-purple">test</span>：条件，必须
    - <span id = "font-purple">var</span>：存储条件结果的变量，非必须
    - <span id = "font-purple">scope</span>：var属性作用域，非必须

```jsp
<c:if test="<boolean>" var="<string>" scope="<string>">
   ...
</c:if>
```

- <span id = "font-green">\<c:choose></span> 与Java switch语句的功能一样，用于在众多选项中做出选择。
    - switch语句中有case，而<c:choose>标签中对应有<c:when>，switch语句中有default，而<c:choose>标签中有<c:otherwise>
    - <span id = "font-purple">test</span>：条件，必须

```jsp
<c:choose>
    <c:when test="<boolean>">
        ...
    </c:when>
    <c:when test="<boolean>">
        ...
    </c:when>
    ...
    ...
    <c:otherwise>
        ...
    </c:otherwise>
</c:choose>
```

- <span id = "font-green">\<c:forEach></span> 迭代一个集合中的对象。
    - <span id = "font-purple">items</span>：要被循环的信息，非必须
    - <span id = "font-purple">begin</span>：开始的元素（0=第一个元素，1=第二个元素），非必须，默认为0
    - <span id = "font-purple">end</span>：最后一个元素（0=第一个元素，1=第二个元素），非必须，默认为Last element
    - <span id = "font-purple">step</span>：每一次迭代的步长，非必须，默认为1
    - <span id = "font-purple">var</span>：代表当前条目的变量名称，非必须
    - <span id = "font-purple">varStatus</span>：代表循环状态的变量名称，非必须

```jsp
<c:forEach items="<object>" begin="<int>" end="<int>" step="<int>" var="<string>" varStatus="<string>">

<c:forEach var="i" begin="1" end="5">
   Item <c:out value="${i}"/><p>
</c:forEach>
```

### Servlet开发

#### HttpServlet类、方法

对于Web应用而言，Servlet主要是用于处理HTTP请求，所以更一般的编写Servlet方法是继承javax.servlet.http.HttpServlet类。

HttpServlet类是GeniricServle类的子类，通过调用指定到HTTP请求的方法来实现service(）方法。对于HTTP中定义的DELETE、HEAD、GET、POST、PUT等方法，分别调用doDelete(），doHead()、doGet()、doPost()、doPut(）等方法来处理相应的请求。

**<center><span id = "font-blue">HttpServlet类主要方法</span></center>**

|方法声明|功能简介|
|:---|:---|
void doGet(httpServletRequest request, HttpServletResponse, response) | 用来处理Http Get请求
void doPost(httpServletRequest request, HttpServletResponse, response) | 用来处理Http Post请求
void service(httpServletRequest request, HttpServletResponse, response) | 根据请求的类型，将请求导向doGet(),doPost()方法

#### 编写、编译Servlet

编写<span id = "font-green">Servlet</span>的一般步骤如下:
<p id = "div-border-left-purple" >
1. 导入javax.servlet包、javax.servlet.http包及其他必要的包。<br>
2. 继承HttpServlet类，并重写doPost（)和doGet（)方法。<br>
3. 在doPost(）和doGet()方法中依次实现获取请求参数、创建输出对象、设置响应类型、输出响应内容等功能。<br>
</p>
<span id = "font-blue">编译</span>和<span id = "font-blue">配置</span>Servlet:

- Servlet类编写完成之后，需要进行编译和部署。
- 编译Servlet之前需要先把Servlet API库文件添加到环境变量CLASSPATH 中。可以直接使用Tomcat发行版中包含的servlet-api.jar。向系统的CLASSPATH环境变量中增加下面的值（假定Tomcat安装目录为d:\tomcat)：
<div class="note success"> d: \tomcat\lib\servlet-api . jar</div>
- 然后打开命令行窗口，进入dem008应用中的src目录，使用下面的命令进行编译：
<div class="note success">javac -d  ..\classes  servlet\HelloServlet.java</div>

```xml web.xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app>
    <servlet>  
        <servlet-name>business</servlet-name>  
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>
    <servlet-mapping>  
        <servlet-name>LogOutServlet</servlet-name>  
        <url-pattern>/logout</url-pattern>  
    </servlet-mapping>
</web-app>
```

### MVC设计模式
<p id = "div-border-left-yellow">
 所谓设计模式，是针对典型问题所提供的一套成熟的解决方案。MVC就是一种流行的程序设计模式，它把程序理解为由模型层（Model)、视图层（View)和控制器层(Controller)三个部分组成。其中，模型层表示程序的业务逻辑和状态，包括业务模型和数据模型；视图层是程序的用户界面，用于显示模型数据；控制器层响应用户请求，根据请求内容来操作模型层并控制程序的流程，决定要向用户显示的视图。
</p>
Java Web应用开发也可以采用MVC设计模式，用JSP作为视图层，Servlet作为控制器层，JavaBean作为模型层。这样的开发形式实现了程序的分层结构，将功能实现、用户界面和流程控制分别由不同的模块来实现，并在各个模块之间实现了良好的解耦。(<span id = "font-blue">jsp Model2</span>)

在基于MVC的Web应用中，<span id = "font-blue">一次用户请求的处理过程</span>如下：

<span id = "inline-toc">1.</span> 浏览器发出请求；
<span id = "inline-toc">2.</span> 作为控制器的Servlet接收请求，并将请求以适当的方式分发给对应的业务模型JavaBean来处理；
<span id = "inline-toc">3.</span> 如果该业务需要与数据库交互，由JavaBean来访问数据库；
<span id = "inline-toc">4.</span> 模型层JavaBean将处理结果返回给控制器Servlet；
<span id = "inline-toc">5.</span> Servlet以适当的方式将结果数据传递给视图层JSP页面，并将控制流程转向该JSP页面；
<span id = "inline-toc">6.</span> 应用服务器将JSP生成的HTML作为响应返回给浏览器。
