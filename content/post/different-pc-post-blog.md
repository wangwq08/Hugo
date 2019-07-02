---
title: "Different Pc Post Blog"
date: 2019-07-03T00:44:46+08:00
draft: false
categories: ["Hugo"]
tags: ["Hugo","BLog"]
---
## Background
Sometimes,I need to use different computers to post blog.

So, I wang to know how to implement it by hugo, It's a little complex for hexo, a blog I used before.

## Solution
* Create a repostirty to store gitname.github.io, the site files, in public
* Create a repostirty to store hugo config file.

## How to do
```
hugo new post/different.md
edit different.md
hugo server to local view
hugo to produce public
git add .
git commit -m "update blog"
git push

cp public to gitname.github.io
git add .
git commit -m "post blog"
git push
```


