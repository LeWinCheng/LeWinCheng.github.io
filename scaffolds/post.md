---
title: {{ title }}
date: {{ date }}
tags: 
categories: 
---









<div id="container"></div>
<link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
<script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
  // id: '页面ID', // 可选。默认为 location.href
  owner: 'LeWinCheng',
  repo: 'lewincheng.github.io',
  oauth: {
    client_id: '57f0000a9cf9df46f0c3',
    client_secret: 'af983206a45da29a131790baa0d076dbc8589de0',
  },
})
gitment.render('container')
</script>