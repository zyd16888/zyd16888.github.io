---
title: hexo优化基于NexT6.4
copyright: ture
abbrlink: 13c8d3a0
notshow: false
tags: 
- hexo 
categories: hexo
date: 2018-08-02 21:07:40
password: 
description: 增加6.0+的新特性,去掉部分过时的功能
image: 
- "https://data.singlelovely.cn/xsj/2018/8/9/hexo-next-optimization-title.jpg"
sticky:  
---

安装的插件：

#### RSS

npm install hexo-generator-feed --save

#### 字数统计

##### next主题为5.x版本

安装 ：npm install hexo-wordcount --save

然后在主题配置文件中启用

##### next主题为6.03+版本

安装：npm install hexo-symbols-count-time --save

打开 ：~\blog\_config.yml

添加

```yml
symbols_count_time:
  symbols: true
  time: true
  total_symbols: true
  total_time: false
```

然后在主题配置文件中启用

#### 自定义站点内容搜索

安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：

 npm install hexo-generator-searchdb --save
编辑 站点配置文件，新增以下内容到任意位置：

search:
  path: search.xml
  field: post
  format: html
  limit: 10000
编辑 主题配置文件，启用本地搜索功能：

\# Local search
local_search:
  enable: true
  
#### 链接持久化

npm install hexo-abbrlink --save

permalink: post/:abbrlink.html
permalink_defaults:
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32
  rep: hex    # 进制：dec(default) and hex

#### 修改标签云

```[swig] 位置：\blog\themes\next\layout\page.swig
{{ tagcloud({min_font: 13, max_font: 31, amount: 1000, color: true, start_color: '#9733EE', end_color: '#FF512F'}) }}
```

修改对应参数值即可，参数说明见 [Hexo 官方文档](https://hexo.io/zh-cn/docs/helpers.html#tagcloud)，颜色可以参考[这个网站](https://uigradients.com)，自己去纠结……

#### 末尾版权信息

hexo next自带版权开启

```yml
#Declare license on posts
#版权信息
post_copyright:
  enable: true
  license: CC BY-NC-SA 4.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh
```

配置文件路径：\hexo\themes\next\layout\_macro\post-copyright.swig

```diff
+{% if page.copyright %}
<ul class="post-copyright">
  <li class="post-copyright-author">
    <strong>{{ __('post.copyright.author') + __('symbol.colon') }}</strong>
    {{ post.author | default(config.author) }}
  </li>
  <li class="post-copyright-link">
    <strong>{{ __('post.copyright.link') + __('symbol.colon') }}</strong>
    <a href="{{ post.url | default(post.permalink) }}" title="{{ post.title }}">{{ post.url | default(post.permalink) }}</a>
  </li>
  <li class="post-copyright-license">
    <strong>{{ __('post.copyright.license_title') + __('symbol.colon') }} </strong>
    {{ __('post.copyright.license_content', theme.post_copyright.license_url, theme.post_copyright.license) }}
  </li>
</ul>
+{% endif %}
```

布局文件路径：\hexo\themes\next\layout\_macro\post.swig

#### 侧栏加入已运行的时间

我们都有自己的生日，都知道自己的岁数，那为什么不给博客加上，让读者知道博客的年纪呢？操作很简单，而且不是精确到年而是精确到秒，233333～

首先要加入下面代码：

```html 文件位置:~/blog/themes/next/layout/_custom/sidebar.swig
<div id="days"></div>
<script>
function show_date_time(){
window.setTimeout("show_date_time()", 1000);
BirthDay=new Date("05/27/2017 15:13:14");
today=new Date();
timeold=(today.getTime()-BirthDay.getTime());
sectimeold=timeold/1000
secondsold=Math.floor(sectimeold);
msPerDay=24*60*60*1000
e_daysold=timeold/msPerDay
daysold=Math.floor(e_daysold);
e_hrsold=(e_daysold-daysold)*24;
hrsold=setzero(Math.floor(e_hrsold));
e_minsold=(e_hrsold-hrsold)*60;
minsold=setzero(Math.floor((e_hrsold-hrsold)*60));
seconds=setzero(Math.floor((e_minsold-minsold)*60));
document.getElementById('days').innerHTML="已运行"+daysold+"天"+hrsold+"小时"+minsold+"分"+seconds+"秒";
}
function setzero(i){
if (i<10)
{i="0" + i};
return i;
}
show_date_time();
</script>
```

上面Date的值记得改为你自己的，且按上面格式，然后修改：

```diff 文件位置：~/blog/themes/next/layout/_macro/sidebar.swig
        {# Blogroll #}
        {% if theme.links %}
          <div class="links-of-blogroll motion-element {{ "links-of-blogroll-" + theme.links_layout | default('inline') }}">
            <div class="links-of-blogroll-title">
              <i class="fa  fa-fw fa-{{ theme.links_icon | default('globe') | lower }}"></i>
              {{ theme.links_title }}&nbsp;
              <i class="fa  fa-fw fa-{{ theme.links_icon | default('globe') | lower }}"></i>
            </div>
            <ul class="links-of-blogroll-list">
              {% for name, link in theme.links %}
                <li class="links-of-blogroll-item">
                  <a href="{{ link }}" title="{{ name }}" target="_blank">{{ name }}</a>
                </li>
              {% endfor %}
            </ul>
+        {% include '../_custom/sidebar.swig' %}
          </div>
         {% endif %}

-        {% include '../_custom/sidebar.swig' %}
```

这样就可以了！当然，要是不喜欢颜色，感觉不好看，就可以在上文所提的`custom.styl`加入：

```styl 文件位置：~/blog/themes/next/source/css/_custom/custom.styl
// 自定义的侧栏时间样式
#days {
    display: block;
    color: rgb(7, 179, 155);
    font-size: 13px;
    margin-top: 15px;
}
```

#### 修改页面宽度

打开　\themes\next\source\css\_variables\custom.styl
添加
```
$main-desktop                   = 1200px
$content-desktop                = 900px
```
以上适用于（NexT5.x版本），6.0+应该写
```
$content-desktop-large          = 830px

```

#### 修改模板文件（增加div，布局调整，避免互相影响）

**~\blog\themes\next\layout\_macro\post.swig**

```diff
-  <div class="post-block">
+  <div class="post-block index">
```

**~\blog\themes\next\layout\_macro\post-collapse.swig**

```diff
{% macro render(post) %}
+ <div class="post-block archives_title">
  <article class="post post-type-{{ post.type | default('normal') }}" itemscope itemtype="http://schema.org/Article">
    <header class="post-header">
	`
	`
	`
    </header>
  </article>
+ </div>
{% endmacro %}

```

#### 评分上面加文字

**~/blog/themes/next/layout/_macro/post.swig**

```diff
        {% if theme.rating.enable %}
          <div class="wp_rating">
+             <div style="color: rgba(0, 0, 0, 0.75); font-size:13px; letter-spacing:3px">(&gt;来评分吧&lt;)</div>
            <div id="wpac-rating"></div>
          </div>
        {% endif %}
```

然后 Ctrl + F 搜索rating，找到这段，对比我给出的，在绿色这行所示的位置，加上自己想要的说明和样式即可。

#### 压缩文件

gulp.js 是基于流的自动化构建工具，我们可以使用 Gulp 为 Hexo 压缩文件
首先任意目录全局安装：

```npm
npm install gulp -g
```

然后到站点文件夹根目录：

```npm
 npm install gulp-minify-css --save
 npm install gulp-uglify --save
 npm install gulp-htmlmin --save
 npm install gulp-htmlclean --save
 npm install gulp-imagemin --save
```

打开　\blog\

新建　gulpfile.js

写入

```javascript
var gulp = require('gulp');

//Plugins模块获取
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');

// 压缩css文件
gulp.task('minify-css', function() {
  return gulp.src('./public/**/*.css')
  .pipe(minifycss())
  .pipe(gulp.dest('./public'));
});
// 压缩html文件
gulp.task('minify-html', function() {
  return gulp.src(['./public/**/*.html','!./public/**/politics/*'])
  .pipe(htmlclean())
  .pipe(htmlmin({
    removeComments: true,
    minifyJS: true,
    minifyCSS: true,
    minifyURLs: true,
  }))
  .pipe(gulp.dest('./public'))
});
// 压缩js文件
gulp.task('minify-js', function() {
    return gulp.src(['./public/**/.js','!./public/js/**/*min.js'])
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
});
// 压缩 public/images 目录内图片
gulp.task('minify-images', function() {
    gulp.src('./public/images/**/*.*')
        .pipe(imagemin({
           optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
           progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
           interlaced: false, //类型：Boolean 默认：false 隔行扫描gif进行渲染
           multipass: false, //类型：Boolean 默认：false 多次优化svg直到完全优化
        }))
        .pipe(gulp.dest('./public/uploads'));
});
// 默认任务
gulp.task('default', [
  'minify-html','minify-css','minify-js','minify-images'
]);

```

#### 文末结束标记

打开　\themes\next\layout\_macro\

新建　passage-end-tag.swig

写入

```swig
{% if theme.passage_end_tag.enabled %}
<div style="text-align:center;color: #ccc;font-size:15px;"><br/><br/><br/>
-------------文章结束啦 ~\(≧▽≦)/~ 感谢您的阅读-------------</div>
<br/>

```

打开　\themes\next\layout\_macro\post.swig

查找　wechat

添加，如下内容

```diff
   {#####################}

+  <div>
+  {% if not is_index %}
+    {% include 'passage-end-tag.swig' %}
+  {% endif %}
+  </div>

    {% if theme.wechat_subscriber.enabled and not is_index %}
```

打开　\themes\next\_config.yml

添加

```yml

# 文章末尾添加“本文结束”标记
passage_end_tag:
  enabled: true


```

#### Live2d看板娘

{% note primary %}
live2d官方[文档](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md)
{% endnote %}

安装  npm install --save hexo-helper-live2d

下载模型包：[live2d-widget-models](https://github.com/xiazeyu/live2d-widget-models)

解压 

将`packages`中的文件放到`node_modules`中

打开  ~\blog\_config.yml

添加

```yml
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-miku  #模板目录，在node_modules里
  display:
    position: left
    width: 150
    height: 300
  mobile:
    show: false
```

#### 引入自定义文件（用于样式定制）

打开　\themes\next\layout\_custom\

新建　custom.swig

打开　\themes\next\layout\_layout.swig

在 \</body> 前添加

```
{% include '_custom/custom.swig' %}
```

#### 评论输入打字礼花及震动特效

下载　 activate-power-mode.js

放置　activate-power-mode.js 至 CDN

打开　\themes\next\layout\_custom\custom.swig

添加

```javascript
<!-- 打字礼花及震动特效 -->
<script type="text/javascript" src="https://qianling-1254036047.cos.ap-chengdu.myqcloud.com/js/activate-power-mode.js"></script>
<script>
    POWERMODE.colorful = true; // ture 为启用礼花特效
    POWERMODE.shake = false; // false 为禁用震动特效
    document.body.addEventListener('input', POWERMODE);
</script>
```

#### 添加emoji

<div class ="note success"><p>参考自 ：<a href="https://www.jianshu.com/p/57e22584b277#emoji%E6%8F%92%E4%BB%B6">emoji插件</a></p></div>

#### 站点地图生成

安装

```npm
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save

```

在<span id="inline-blue">站点配置文件</span>中启用

```yml
# 自动生成sitemap
sitemap:
path: sitemap.xml
baidusitemap:
path: baidusitemap.xml
```

#### 文章加密码

##### 方式一：修改模板配置文件（不推荐）

<span id = "font-blue">打开</span> ~\blog\themes\next6.4\layout\_partials\head\

<span id = "font-blue">新建</span> password.swig

<span id = "font-blue">写入</span>

```javascript

<script>
    (function () {
        if ('{{ page.password }}') {
            if (prompt('请输入文章密码') !== '{{ page.password }}') {
                alert('密码错误！');
                if (history.length === 1) {
                    location.replace("https://www.singlelovely.cn"); // 这里替换成你的首页
                } else {
                    history.back();
                }
            }
        }
    })();
</script>
```
<span id = "font-blue">然后打开</span>~\blog\themes\next6.4\layout\_partials\head\head.swig

<span id = "font-blue">写入</span>
```diff
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=2"/>
<meta name="theme-color" content="{{ theme.android_chrome_color }}">

+ {% if not is_index %}
+   {% include 'password.swig' %}
+ {% endif %}

{% if theme.needmoreshare2.enable %}
```
<span id = "font-red">最后</span> 在需要加密的文章前面增加属性<span id="inline-yellow"> password </span>

##### 方式二 ：使用插件进行加密

<span id = "font-blue">插件地址：</span> https://github.com/MikeCoder/hexo-blog-encrypt

#### 首页文章摘要图

##### 方式一：只在首页显示，文章中不显示

<span id = "font-blue">打开</span> ~\blog\themes\next6.4\layout\_macro\post.swig

<span id = "font-blue">搜索：</span> <span id="inline-green"> post.description</span>

<span id = "font-blue">下面添加：</span> 
```

{% if post.image %}
            <div class="out-img-topic">
              <img src={{ post.image }} class="img-topic" />
            </div>
 {% endif %}

```
然后在<span id = "font-blue">文章</span> 中写：
```
image: 
- "http://oz2tkq0zj.bkt.clouddn.com/17-11-9/52323298.jpg"
```
##### 方式二：首页和文章中都显示

<span id = "font-blue">直接</span>在<span id = "font-blue">文章</span> 中写（默认支持）：
```
photos: 
- "http://oz2tkq0zj.bkt.clouddn.com/17-11-9/52323298.jpg"
```

#### 文章置顶

<span id = "font-blue">打开</span>　\blog\node_modules\hexo-generator-index\lib\generator.js

<span id = "font-blue">将内容修改为　</span>

```javascript
'use strict';
var pagination = require('hexo-pagination');
module.exports = function(locals){
  var config = this.config;
  var posts = locals.posts;
    posts.data = posts.data.sort(function(a, b) {
        if(a.sticky && b.sticky) { // 两篇文章sticky都有定义
            if(a.sticky == b.sticky) return b.date - a.date; // 若sticky值一样则按照文章日期降序排
            else return b.sticky - a.sticky; // 否则按照sticky值降序排
        }
        else if(a.sticky && !b.sticky) { // 以下是只有一篇文章sticky有定义，那么将有sticky的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.sticky && b.sticky) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排
    });
  var paginationDir = config.pagination_dir || 'page';
  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};

```
<span id = "font-blue">使用方法</span>

在文章中添加 sticky 值，数值越大文章越靠前，如

```
title: hexo优化基于NexT6.4
copyright: false
abbrlink: 13c8d3a0
notshow: false
tags: 
- hexo 
categories: hexo
date: 2018-08-02 21:07:40
password: 
description: 增加6.0+的新特性,去掉部分过时的功能
image: 
- "https://data.singlelovely.cn/xsj/2018/8/9/hexo-next-optimization-title.jpg"
sticky: 10

```