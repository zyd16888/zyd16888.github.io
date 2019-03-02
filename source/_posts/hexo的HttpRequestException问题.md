---
title: hexo的HttpRequestException问题
tags:
  - hexo
categories: hexo
copyright: true
abbrlink: b04d82e3
date: 2018-03-05 16:15:08
password:
---

今天同步hexo的时候突然出现了这样的报错

```
fatal: HttpRequestException encountered.
   ▒▒▒▒▒▒▒▒ʱ▒▒▒▒
bash: /dev/tty: No such device or address
error: failed to execute prompt script (exit code 1)
fatal: could not read Username for 'https://github.com': No error
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: fatal: HttpRequestException encountered.
   ��������ʱ����
bash: /dev/tty: No such device or address
error: failed to execute prompt script (exit code 1)
fatal: could not read Username for 'https://github.com': No error

    at ChildProcess.<anonymous> (H:\hexo\node_modules\hexo-util\lib\spawn.js:37:17)
    at emitTwo (events.js:126:13)
    at ChildProcess.emit (events.js:214:7)
    at ChildProcess.cp.emit (H:\hexo\node_modules\cross-spawn\lib\enoent.js:40:29)
    at maybeClose (internal/child_process.js:925:16)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:209:5)
```

这个问题困扰了很久，解决办法是更改` 站点配置文件 `

原来是
```
deploy:
  type: git
  repository: https://github.com/zyd16888/zyd16888.github.io.git
  branch: master

```
改成
```
deploy:
  type: git
  repository: git@github.com:zyd16888/zyd16888.github.io.git
  branch: master
```

问题解决···········出错原因表面看上去是应为https协议问题，改成ssh协议就行，不过hexo应该是支持https协议的········




