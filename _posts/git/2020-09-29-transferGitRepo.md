---
layout: post
title:  "Git Repository 옮기기"
date:   2020-09-29T10:02:52-05:00
author: miz
categories: Git
---

# Git Repository 옮기기

1. Origin Git 에서 clone 받기
`git clone --mirror {origin repo}`

2. 보낼 url로 주소 변경
`git remote set-url origin {이동할 repo}`

3. push
`git push --mirror`