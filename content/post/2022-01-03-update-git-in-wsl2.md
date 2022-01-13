---
title: Update git in WSL2
slug: update-git-in-wsl2
description: null
author: null
date: '2022-01-03T07:17:03.683Z'
lastmod: 2019-08-22T15:20:28.000Z
draft: true
tags: []
categories: []
---

This article is use WSL2 + Ubuntu

## Add PPA

Ubuntu package repository จะไม่ได้ git version ใหม่ 

Add PPA ของ Git เพื่อเอา latest version โดยตรง [ref](https://git-scm.com/download/linux)

```sh
sudo add-apt-repository ppa:git-core/ppa
```

## Install new version

```sh
sudo apt update
sudo apt instal git
```

Check result
```sh
git version
```



