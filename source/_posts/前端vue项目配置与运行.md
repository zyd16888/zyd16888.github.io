---
title: 前端vue项目配置与运行
copyright: false
abbrlink: ead1bac9
notshow: false
description: 简单说明一下配置运行过程，及其中的坑
date: 2020-08-27 08:18:00
tags:
categories:
password:
image:
photos:
sticky:
---


## 环境依赖

- 必需：
    - Node.js
    - npm
    - vue-cli 

- 可选：
    - IntelliJ IDEA （建议安装）
        - 必须安装 `Ultimate` 版， `Community` 版不支持 web 相关功能。
        > tips: 教育网邮箱可以官网申请一年 Ultimate 激活码

## 软件安装

1. Node.js
    - 下载地址 ： https://nodejs.org/dist
    - 建议安装 v10 ~ v12 间的版本，版本过低或者过高都会出现一些奇怪的问题：见下文。
2. npm 
    - node.js 中集成
3. vue-cli
    - 打开命令行执行 `npm install vue-cli`

## 项目运行

### 使用命令行运行

1. 克隆项目到本地，新建分支并切换

```git
git clone http://222.129.11.38/Waver/vue.git

cd vue

git checkout -b run_dev
```

2. 安装依赖包（以admin为例）

```git
cd admin

npm install
```

3. 启动项目并运行

    - 首先查看一下 `package.json` 中 scripts 下面配置的启动项
    - ![](https://data.singlelovely.cn/images/20200826220010.png)
    - 根据启动项执行不同的命令，如在本例中就是： `npm run dev` 启动项目
    - 如未报错的话，则会看到以下内容
    - ![](https://data.singlelovely.cn/images/20200826215832.png)

### IntelliJ IDEA 中运行

1. 安装 `vue.js` 插件
    - ![](https://data.singlelovely.cn/images/20200826220135.png)

2. 导入项目
    - File -> Open -> 选中vue文件夹 -> 点击ok
    - ![](https://data.singlelovely.cn/images/20200826220049.png)

3. 安装依赖项
    - 根据弹出的提升点击 `npm install`
    - ![](https://data.singlelovely.cn/images/20200826220215.png)
    - 如未弹出，则手动在命令行进入当前目录后执行 `npm install`

4. 配置运行环境
    - 点击上方工具栏的 `Edit Configurations`
    - ![](https://data.singlelovely.cn/images/20200826220251.png)
    - 添加一个 npm 运行环境
    - ![](https://data.singlelovely.cn/images/20200826220443.png)
    - 配置运行参数
    - ![](https://data.singlelovely.cn/images/20200826220502.png)
    - 然后点击运行即可

## 连接后端服务

> 需要修改的文件有 `baseurl.config.js` 与 `vue.config.js`

配置相关内容，可以参考 webpack [官方文档](https://www.webpackjs.com/configuration/)

主要内容如下：

```javascript baseurl.config.js
exports.BASE_URL = {
  'development': 'http://platform.imch.com.cn/',  // 本地环境
  'production': {
    '127.0.0.1': 'http://platform.imch.com.cn/', // 本地打包请求地址
    '192.168.1.200': 'http://192.168.1.200:8093/', // 200测试机请求接口地址
    '220.249.8.102': 'http://220.249.8.102:22334/', // 潞电外网请求接口地址
    'localhost': 'http://yjzx.lddq.com:8285',  // 潞电外网请求接口地址
    '192.168.0.155': 'http://192.168.0.155:8285' // 潞电内网请求接口地址
  },
}
exports.IMG_URL = {
  //'localhost': 'http://file.imch.com.cn', // 本地环境
  //'127.0.0.1': 'http://file.imch.com.cn', // 本地环境
  //'192.168.1.200': 'http://192.168.1.200:6003', // 200测试机
  'localhost': 'http://yjzx.lddq.com:22333', // 潞电外网地址
  //'192.168.0.155': 'http://192.168.0.155:22333' // 潞电内网地址
}
```

```javascript vue.config.js
devServer: {
        /* 自动打开浏览器 */
        open: true,
        /* 设置为0.0.0.0则所有的地址均能访问 */
        // host: 'localhost',
        host: '0.0.0.0',
        port: 8081,
        https: false,
        hotOnly: false,
        /* 使用代理 */
        proxy: {
            '/api': {
                /* 目标代理服务器地址 */
                // target: 'http://192.168.1.200:8093',
                // target: 'http://192.168.1.84:8081',
                //target: target,
                target: "http://yjzx.lddq.com:8285",
                /* 允许跨域 */
                changeOrigin: true,
                pathRewrite: {
                    '^/api': ''
                }
            },
        },
    },

```

## 一些问题的解决

### 运行时报错：cannot find module @babel/compat-data/corejs3-shipped-proposals

![](https://data.singlelovely.cn/images/20200826220807.png)

Node.js 版本兼容问题导致，详细问题可查看：[issues](https://github.com/storybookjs/storybook/issues/10477)、[stackoverflow](https://stackoverflow.com/questions/61238650/i-am-having-an-issue-with-babel-building-angular-app-for-production)

解决方法：
1. 更换 node 版本
2. 编辑 `package.json` 文件，在 `"devDependencies"` 下添加一行，然后执行`npm install`
```json
"@babel/compat-data": "7.9.0"
```
3. 控制台执行以下命令
```
npm install -D babel-loader @babel/core @babel/preset-env webpack
```

### 页面控制台报错：Cross-Origin Read Blocking

`baseurl.config.js` 文件中配置的地址冲突所造成的跨域问题，将不需要的地址注释掉即可

详细问题原因可以查看：[stackoverflow](https://stackoverflow.com/questions/61238650/i-am-having-an-issue-with-babel-building-angular-app-for-production)

### 运行是无法编译

偶发性问题，可以根据报错参数，具体查询 nodejs 的[文档](https://nodejs.org/api/errors.html#errors_common_system_errors)



&ensp;
&ensp;
&ensp;

> 写的比较仓促，有问题请及时反馈。



