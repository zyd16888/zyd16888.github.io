---
title: about页面不显示右侧文章目录sidebar
copyright: true
abbrlink: 106fc1c3
tags:
  - hexo
categories: hexo
date: 2018-06-04 18:01:12
password:
---

{% meting "356039117" "xiami" "playlist"  "mutex:false" "listmaxheight:340px" "preload:none" "theme:#7FFF00"%}

&emsp;&emsp;next主题添加about页面后，会默认显示以#开头的的文章目录界面，原因是next主题中并没有给about页面设置模板，而是使用了post也就是文章页面的模板。
&emsp;&emsp;这样带来的后果就是，about页面显得很丑，而精心制作的站点介绍页面没有办法直观的展示出来，解决办法有以下三个：
### 方法一
页面内不要使用#这种标题的形式

### 方法二
删除代码：
路径：`hexo\themes\next\layout\post.swig`
删除以下代码：
```
{% block script_extra %}
  {% include '_scripts/pages/post-details.swig' %}
{% endblock %}
```


### 方法三
修改代码
路径：`next/layout/_macro/sidebar.swig `
```
//line 17
{% if display_toc and toc(page.content).length > 1 and page.type != 'about' %}
//line 28
{% if not display_toc or toc(page.content).length <= 1 or page.type == 'about' %}
//line 141
{% if display_toc and toc(page.content).length > 1 and page.type != 'about' %}
```
行数不一定完全准确，可以用搜索查找字符串