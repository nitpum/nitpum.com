---
title: อัพเดท Git ให้เป็นเวอร์ชันล่าสุดบน Ubuntu และ WSL
author: nitpum
date: '2022-02-19T16:53:19.439Z'
lastmod: '2022-02-19T18:17:31.396Z'
tags:
  - git
  - ubuntu
  - wsl
  - windows
---

ปกติ Ubuntu จะลง Git มาให้อยู่แล้ว หรือถ้าอยากอัพเดทก็สั่ง `apt install` ได้เลย ปัญหาคือ package repository ของ Ubuntu นั้นไม่ได้มี Git เวอร์ชันล่าสุดเสมอ ทำให้ถ้าเราอยากจะลงเวอร์ชันใหม่เราจะทำไม่ได้

โพตส์นี้เลยจะมาแชร์วิธีอัพเดท Git ใน Ubuntu ซึ่งวิธีนี้ยังใช้ได้กับ Windows Subsystem for Linux (WSL) ที่เป็น Ubuntu อีกด้วย (เอาจริงๆ ก็น่าจะใช้ได้กับ Ubuntu-based Distro ทั้งหมดแหละพวก Linux Mint, Elementary OS, Pop!\_OS, Kubuntu แต่ผมไม่ได้ลองเทสดูนะ แต่คิดว่าน่าจะได้หมด)

## เพิ่ม PPA ของ Git โดยตรง

อย่างที่บอกไปว่า package repository ของ Ubuntu ไม่ได้มี Git เวอร์ชันล่าสุดเสมอ วิธีแก้ก็คือเพิ่ม package repository ของ Git โดยตรงมา เพื่อที่เราจะได้อัพเดทเป็นเวอร์ชันล่าสุดได้

```sh
sudo add-apt-repository ppa:git-core/ppa
```

## ลงเวอร์ชันใหม่

พอเพิ่ม package repostiory ของ Git แล้วให้เราอัพเดทลิตส์แพ็ตเกจสักหน่อย Ubuntu จะได้รู้ว่าโหลด Git เวอร์ชันใหม่จาก package repository ของ Git เองได้

```sh
sudo apt update
```

เสร็จแล้วก็ลง Git เวอร์ชันใหม่เลย

```sh
sudo apt instal git
```

ลงเสร็จแล้วลองเช็คดูด้วยว่าได้เป็นเวอร์ชันล่าสุดหรือยัง

```sh
git version
```

**อ้างอิง**

- [Download Git for Linux and Unix](https://git-scm.com/download/linux)
