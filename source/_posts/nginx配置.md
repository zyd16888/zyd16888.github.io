---
title: nginx配置
copyright: true
abbrlink: 2bee8b90
notshow: false
description: nginx常用配置记录
image:
  - 'https://data.singlelovely.cn/images/20200130185945.gif!CoverPicture'
date: 2020-01-30 19:14:00
tags: 
- Linux
- Ubuntu
categories: Linux
password:
photos:
sticky:
---

最近折腾的web应用比较多，在nginx使用中踩了不少坑，记录一下，以便以后查询

### 安装

```
apt update
apt install -y nginx
```

### 配置文件路径

<span id = "font-blue"> /etc/nginx/conf.d </span>

建议每个站点单独建一个 `***.conf` 放在此目录

### ssl证书位置

默认相对目录为 <span id = "font-blue">/etc/nginx</span> ，建议新建一个目录来存放，如 /etc/nginx/cert，
则在配置中填写为： `cert/证书名`

<div class="note success"><p>亦可将证书放在其他地方，配置文件中使用绝对路径</p></div>

### http配置

```json
server {
    listen      80;                        # 站点监听端口
    server_name zfile.singlelovely.cn ;    # 站点域名
    root        /www/test;                  # 网站根目录
    index       index.html index.htm index.jsp;
}
```

### https配置

```json
server {
        listen          443;
        server_name     zfile.singlelovely.cn;
        ssl             on;
        root            /www/test;
        index       index.html index.htm index.jsp
        ssl_certificate         cert/1_zfile.singlelovely.cn_bundle.crt;
        ssl_certificate_key     cert/2_zfile.singlelovely.cn.key;
        ssl_session_timeout     5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
}
```

### 反向代理配置

```json
location / {
                proxy_pass      http://127.0.0.1:666;
                index index.html index.htm;
                proxy_redirect off;
                proxy_buffer_size 4k;
                proxy_buffers 4 32k;
                proxy_busy_buffers_size 64k;
                proxy_send_timeout 300;
                proxy_read_timeout 300;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
        }
```

### http 强制重定向到https

<p id = "div-border-left-purple">rewrite ^ https://$http_host$request_uri? permanent;</p>

### 检查配置问题

<span id = "font-green">nginx -t</span>

### 重启服务

<span id = "font-green">service nginx restart</span>
