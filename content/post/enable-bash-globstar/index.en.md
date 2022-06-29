---
title: How to enable bash globstar **
author: nitpum
date: 2022-06-02T07:06:35.205Z
lastmod: 2022-06-29T18:45:20.329Z
tags: []
---

Unlike Zsh, globstar `**` is not enabled by default in bash.

We can enable by use shopt command (**SH**ell **OPT**ion)

```bash
shopt -s globstar
```
