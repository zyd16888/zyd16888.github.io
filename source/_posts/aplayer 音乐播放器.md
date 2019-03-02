---
title: aplayer 音乐播放器
copyright: false
abbrlink: a84d1ef1
date: 2018-04-06 11:33:18
tags:
- hexo
categories: hexo
password:
---

hexo插入音乐，以前用网易云音乐可以直接生成外链播放器，但版权保护了以后，好多音乐都不能生成外链播放了。

关于外链播放器，网上找了很久，好多解决方案都是把音乐放网盘，然后自己写一个播放插件加入到页面中，这个办法是不错，但它不适用于hexo这种依赖引擎自动渲染的网站。

是可以把js等放在模板中，渲染的时候调用，但不是所有的网页都要插入音乐，放在模板中无疑会拖慢渲染速度，而且为了这个小东西，自己去改模板，有点复杂了。

aplayer提供了一个不错的解决办法，[hexo-tag-aplayer](https://github.com/MoePlayer/hexo-tag-aplayer)插件,可以绕过版权问题


## 安装

```
npm install --save hexo-tag-aplayer
```

## 依赖

+ APlayer.js > 1.8.0
+ Meting.js > 1.1.1

## 使用

### 直接使用办法

```
{% aplayer title author url [picture_url, narrow, autoplay, width:xxx, lrc:xxx] %}
```

注：此方法不支持一键调用资源，需要手动获取链接后填写，或者开启 Hexo 的 [文章资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html#%E6%96%87%E7%AB%A0%E8%B5%84%E6%BA%90%E6%96%87%E4%BB%B6%E5%A4%B9) 功能，将图片、音乐文件、歌词文件放入与文章对应的资源文件夹中，然后直接引用：

```
{% aplayer "Caffeine" "Jeff Williams" "caffeine.mp3" "picture.jpg" "lrc:caffeine.txt" %}
```

### MeingJS 支持 

[MetingJS](https://github.com/metowolf/MetingJS) 是基于[Meting API](https://github.com/metowolf/Meting) 的 APlayer 衍生播放器，引入 MetingJS 后，播放器将支持对于 QQ音乐、网易云音乐、虾米、酷狗、百度等平台的音乐播放。

（目前QQ音乐失效，因为QQ音乐屏蔽掉了歌曲ID）
> 虾米音乐部分失效，无法解析 （2018.8.10）

如果使用 MetingJS，请在 Hexo 配置文件 `_config.yml` 中设置：

```yaml
aplayer:
  meting: true
```

接着就可以通过 **{**% meting ...%**}** 在文章中使用 MetingJS 播放器了：

```
<!-- 简单示例 (id, server, type)  -->
{% meting "108138" "netease" "song" %}
```
{% meting "108138" "netease" "song" %}

```
<!-- 进阶示例 -->
{% meting "11100236" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}
```

{% meting "11100236" "netease" "playlist"  "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}

有关  **{**% meting %**}**  的选项列表如下:

| 选项            | 默认值           | 描述                                       |
| ------------- | ------------- | ---------------------------------------- |
| id            | **必须值**       | 歌曲 id / 播放列表 id / 相册 id / 搜索关键字          |
| server        | **必须值**       | 音乐平台: `netease`, `tencent`, `kugou`, `xiami`, `baidu` |
| type          | **必须值**       | `song`, `playlist`, `album`, `search`, `artist` |
| mode          | `circulation` | 列表播放模式, `circulation`, `random`, `single`, `order` |
| autoplay      | `true`        | 自动播放，移动端浏览器暂时不支持此功能                      |
| mutex         | `true`        | 该选项开启时，如果同页面有其他 aplayer 播放，该播放器会暂停       |
| listmaxheight | `340px`       | 播放列表的最大长度                                |
| preload       | `auto`        | 音乐文件预载入模式，可选项： `none`, `metadata`, `auto` |
| theme         | `#ad7a86`     | 播放器风格色彩设置                                |

关于如何设置自建的 Meting API 服务器地址，以及其他 MetingJS 配置，请参考章节[自定义配置](#%E8%87%AA%E5%AE%9A%E4%B9%89%E9%85%8D%E7%BD%AE30-%E6%96%B0%E5%8A%9F%E8%83%BD)

### PJAX 兼容

若在 Hexo 中使用了 PJAX，可能需要自己手动清理 APlayer 全局实例：

```js
$(document).on('pjax:start', function () {
    if (window.aplayers) {
        for (let i = 0; i < window.aplayers.length; i++) {
            window.aplayers[i].destroy();
        }
        window.aplayers = [];
    }
});
```

## 自定义配置

在 Hexo 配置文件  `_config.yml` 中配置：

```yaml
aplayer:
  script_dir: some/place                        # Public 目录下脚本目录路径，默认: 'assets/js'
  style_dir: some/place                         # Public 目录下样式目录路径，默认: 'assets/css'
  cdn: http://xxx/aplayer.min.js                # 引用 APlayer.js 外部 CDN 地址 (默认不开启)
  style_cdn: http://xxx/aplayer.min.css         # 引用 APlayer.css 外部 CDN 地址 (默认不开启)
  meting: true                                  # MetingJS 支持
  meting_api: http://xxx/api.php                # 自定义 Meting API 地址
  meting_cdn: http://xxx/Meing.min.js           # 引用 Meting.js 外部 CDN 地址 (默认不开启)
  asset_inject: true                            # 自动插入 Aplayer.js 与 Meting.js 资源脚本, 默认开启
  externalLink: http://xxx/aplayer.min.js       # 老版本参数，功能与参数 cdn 相同
```
如不需要自定义脚本，请不用在`_config.yml` 中配置这些内容。

## 故障排除

### 标签参数空格问题

在 Hexo 标签中，用户可能无法直接在标签参数中[加入空格](https://github.com/hexojs/hexo/issues/1455)

如果遇到这类问题，请直接将参数用双引号括起来使用，如下所示：

```
{% aplayer "Caffeine" "Jeff Williams" "caffeine.mp3" "autoplay" "width:70%" "lrc:caffeine.txt" %}
```

### 重复载入 Aplayer.js 资源脚本问题
(5.10以上版本的hexo不存在此问题)
本插件通过 `after_render:html`过滤器 , 将 `APlayer.js` 和 `Meting.js` 插入到使用了本插件标签 的 HTML 文件中:

```html
<html>
  <head>
    ...
    <script src="assets/js/aplayer.min.js"></script>
    <script src="assets/js/meting.min.js"></script>
  </head>
  ...
</html>
```

但是 `after_render:html` 在一些情形下可能无法被正常触发:

- [Does not work with hexo-renderer-jade](https://github.com/hexojs/hexo-inject/issues/1)
- `after_render:html` 似乎在 Hexo 服务器模式默认配置中无法被调用 (`hexo server`), 遇到这种情况用户可能需要使用 `hexo-server` 的静态文件解析模式 ( `hexo server -s`) .

如果在博客生成过程中，插件发现 `after_render:html` 没有被调用，那么插件将会通过 `after_post_render` 过滤器来植入脚本。但是使用 `after_post_render` 会有重复载入 `APlayer.js` 的情况（例如当一个页面中存在多篇博客时），以及一些非文章页面将无法使用本插件。

如果想完全解决这个问题，用户可能需要自己在主题文件中手动加入 `Aplayer.js` 与 `Meting.js`，同时关闭插件的自动脚本插入功能：

```yaml
aplayer:
  asset_inject: false
```
<center>END</center>

&emsp;
&emsp;
&emsp;

手动插入详见：[Hexo音乐播放完美支持https和多平台](https://www.tiexo.cn/aplayer/)
建议使用插件，手动插入不利于后期维护及排错······
本文原链接：https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md  
基于原文，有删改。