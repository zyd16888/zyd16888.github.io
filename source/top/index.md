---
title: TopX
comments: false
keywords: top,文章阅读量排行榜
description: 博客文章阅读量排行榜
---
<div id="top"></div>
<script src="https://cdn1.lncld.net/static/js/av-core-mini-0.6.4.js"></script>
<script>AV.initialize("8QMj0uOJdczOlxeHKH2i6Spb-gzGzoHsz", "AGFEQO5aIXQBAGF5mc5N2tHL");</script>
<script type="text/javascript">
  var time=0
  var title=""
  var url=""
  var query = new AV.Query('Counter');
  query.notEqualTo('id',0);
  query.descending('time');
  query.limit(1000);
  query.find().then(function (todo) {
    for (var i=0;i<1000;i++){
      var result=todo[i].attributes;
      time=result.time;
      title=result.title;
      url=result.url;
      var content="<a href='"+"https://www.singlelovely.cn"+url+"'>"+title+"</a>"+"<br />"+"<font color='#555'>"+"阅读次数："+time+"</font>"+"<br /><br />";
      document.getElementById("top").innerHTML+=content
    }
  }, function (error) {
    console.log("error");
  });
</script>
<p>LeanCloud 因实名认证问题（需要支付宝刷脸认证，但当前手机不支持刷脸，问题暂时无解），请求可能会出问题，如未正常显示，请谅解。。。</p>
<style>.post-description { display: none; }<style>