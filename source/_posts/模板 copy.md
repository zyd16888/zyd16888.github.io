---
title: jupyter notebook美化与配置自动补全
copyright: false
abbrlink: 256ed997
notshow: false
tags:
  - python
categories: python
description: 是时候需要给生活点颜色看看了
date: 2019-08-18 00:30:00
password:
image:
- "https://data.singlelovely.cn/CoverPicture/256ed997.webp!CoverPicture"
photos:
sticky:
---

## 具体配置请参看以下文章

https://blog.csdn.net/az9996/article/details/88621028

## 记录下我自己的配置

```js
jt -t oceans16 -lineh 140  -tf ptmono -f firacode -ofs 12 -fs 13 -nfs 12 -T -N
```

## 上述文章中的错误更改

按原文中的方法安装 `jupyter_contrib_nbextensions`和`jupyter_nbextensions_configurator` 时，会报以下错误

```js
(jupyter) λ conda install jupyter_contrib_nbextensions
Collecting package metadata (current_repodata.json): done
Solving environment: failed with current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: failed

PackagesNotFoundError: The following packages are not available from current channels:

  - jupyter_contrib_nbextensions

Current channels:

  - https://repo.anaconda.com/pkgs/main/win-64
  - https://repo.anaconda.com/pkgs/main/noarch
  - https://repo.anaconda.com/pkgs/r/win-64
  - https://repo.anaconda.com/pkgs/r/noarch
  - https://repo.anaconda.com/pkgs/msys2/win-64
  - https://repo.anaconda.com/pkgs/msys2/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

    https://anaconda.org

and use the search bar at the top of the page.
```

然后按照提示去官网查询，找到响应的包，会看到 `Info: This package contains files in non-standard labels.` 就是不在标准标签中的意思。

![](https://data.singlelovely.cn/images/20190818002421.png)

然后需要用以下命令安装

```js
conda install -c conda-forge jupyter_contrib_nbextensions
conda install -c conda-forge jupyter_nbextensions_configurator
```

安装时候注意网络环境，不正确的网络异常的慢

![](https://data.singlelovely.cn/images/20190818002516.png)