---
title: "Add Gitalk"
date: 2022-04-11T14:23:25+08:00
---
# 普通的网页增加gitalk的支持
gitalk会根据issuse的id来确定支持的哪个issuse,这个id就是创建的时间，这种做法是even的做法，但是这种做法可能会有问题，对与支持自己创建的issue，会不会有更好的办法呢

```html
    <div id="gitalk-container"></div>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js" crossorigin="anonymous"></script>
    <script type="text/javascript">
      var gitalk = new Gitalk({
        id: '2022-03-14 22:10:48 \u002b0800 CST',
        title: 'About',
        clientID: '3c363d50efbac96d4ccf',
        clientSecret: 'be359f87cb1cfef9defe74bfdcc4d36b254d4af9',
        repo: 'hugopages',
        owner: 'taontech',
        admin: ['taontech'],
        body: decodeURI(location.href)
      });
      gitalk.render('gitalk-container');
    </script>
    <noscript>Please enable JavaScript to view the <a href="https://github.com/gitalk/gitalk">comments powered by gitalk.</a></noscript>

```

> **gitalk** 会根据当前链接来创建issue,但是我们的issue需要自己创建，而gitalk只是后期使用。所以可能需要增加后续工作来完美适配
> Gitalk的UI比较好看，暂时不需要修改。
