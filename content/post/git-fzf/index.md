---
title: checkout git branch ให้ง่ายขึ้นด้วย fzf
author: nitpum
date: 2023-03-12T14:18:06+07:00
lastmod: 2023-03-12T13:37:16.234Z
draft: true
tags:
  - git
  - fzf
  - cli
---

เชื่อว่าแต่ละคน แต่ละทีมก็จะมีวิธีการตั้งชื่อ branch ในรูปแบบที่ต่างกันไม่ว่าจะเป็น `JIRA-23-navbar`, `feat/navbar` และแบบอื่นๆ

ปกติเวลาเราจะ checkout/switch ไป branch นั้นๆ ต้องพิมพ์ชื่อ branch เองทั้งหมดซึ่งบางทีก็ยาวทำให้เสียเวลาหรือไม่ก็ใช้ autocomplete ช่วย แต่ถ้าชื่อ branch มันคล้ายกันอย่าง `JIRA-23-navbar` กับ `JIRA-33-menu` ยิ่งทำให้ autocomplete ยากขึ้นไปอีก

แทนที่เราจะมานั่งพิมพ์เองหรือใช้ autocomplete เรามาทำให้มัน search ชื่อ branch ได้น่าจะง่ายกว่า

## fzf

fzf เป็น cli ใช้สำหรับ fuzzy search ซึ่งในเคสนี้เราสามารถเอามาใช้ในการ search ชื่อ branch ได้โดยที่ไม่ต้องพิมพ์เป๊ะตรงตามตัวอักษร

เริ่มจากการติดตั้งตัว fzf ก่อนเลย

```bash
# Ubuntu
sudo apt install fzf
# macOS
brew install fzf
```

ทดลองใช้ด้วยคำสั่ง

```bash
git branch -a | fzf
```

- `git branch -a` คือ ให้ list ชื่อ branch มาทั้งหมดรวมถึงที่อยู่บน remote ด้วย
- จากนั้นส่ง output จาก git branch เข้า fzf เพื่อเอาไปทำ fuzzy search

```bash
git checkout $(git branch -a | fzf)
```

## git alias

```bash
alias gco="git checkout $(git branch -a | fzf)"
alias grbi="git rebase -i $(git branch -a | fzf)"
```
