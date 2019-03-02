---
title: hexo页面布局修改
tags:
  - hexo
categories: hexo
copyright: true
abbrlink: 8b3b02a7
date: 2018-04-03 20:00:59
password:
---

&emsp;&emsp;主要是为了解决about页面的文章目录自动弹出的问题

这个问题困扰了很久，今天下雨天，正好静心看看文档，解决一下这个问题

`注：本文以next主题为例`

next主题采用的是Swig模板，Swig模板可以参考 [Swig中文文档](http://www.iqianduan.net/blog/how_to_use_swig)

### 主题介绍

#### 更换主题
创建 Hexo 主题非常容易，只要在 themes 文件夹内，新增一个任意名称的文件夹，并修改  _config.yml 内的 theme 设定，即可切换主题。一个主题可能会有以下的结构：

     ├── _config.yml      //这个是主题配置项文件
     ├── languages        //这个是语言文件
     ├── layout           //这个是模板文件
     ├── scripts           
     └── source     
	 
1.Layout
布局文件夹。用于存放主题的模板文件，决定了网站内容的呈现方式，Hexo 内建 Swig 模板引擎，您可以另外安装插件来获得 EJS、Haml 或 Jade 支持，Hexo 根据模板文件的扩展名来决定所使用的模板引擎。

     layout.ejs   - 使用 EJS
	 layout.swig  - 使用 Swig

2.source
资源文件夹，除了模板以外的 Asset，例如 CSS、JavaScript 文件等，都应该放在这个文件夹中。文件或文件夹开头名称为 _（下划线线）或隐藏的文件会被忽略。
如果文件可以被渲染的话，会经过解析然后储存到 public 文件夹，否则会直接拷贝到 public 文件夹。

#### 模板
模板决定了网站内容的呈现方式，每个主题至少都应包含一个 index 模板，以下是各页面相对应的模板名称：

| 模板  |  用途    |   回调  |
| -- | ---- | ---- |
| index | 首页 |     |
|    post   |   文章   |  index   |
|    page   |   分页   |  index   |
|   archive    |  归档    |  index   |
|   category  |   分类归档   |  archive   |
|    tag   |   标签归档   |  archive   |

#### 局部模板
局部模板让您在不同模板之间共享相同的组件，例如页首（Header）、页脚（Footer）或侧边栏（Sidebar）等，可利用局部模板功能分割为个别文件，让维护更加便利。举例来说：
```
{% codeblock partial/header.ejs %}
<h1 id="logo"><%= config.title %></h1>
{% endcodeblock %}

{% codeblock index.ejs %}
<%- partial('partial/header') %>
<div id="content">Home page</div>
{% endcodeblock %}

```
生成：
~~~
<h1 id="logo">My Site</h1>
<div id="content">Home page</div>
~~~


#### 修改

知道了模板对应的具体内容，就可以着手进行修改了，next主题页面模板大多使用局部模板进行组合，只需要增加或者减少组件的引用，就可以实现页面布局的修改。


### 参考资料

Hexo官方网站 : https://hexo.io/

>  
> **暂时就这么多了，具体的没深入看**
>    