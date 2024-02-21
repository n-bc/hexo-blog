---
title: 留言板
---
<div id="container"></div>
<link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
<script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
  id: 'location.href', // 可选。默认为 location.href
  owner: 'n-bc',  //改你自己的名字
  repo: 'Comments',  //专门储存评论一个GitHub仓库
  oauth: {
    client_id: '575f1eaa65a674d1b159', //改为你自己的，下同
    client_secret: '9c4b5759b5979020171977b973075bffddc94aef', 
  },
})
gitment.render('container')
</script>