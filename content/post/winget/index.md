---
title: ติดตั้งและใช้งาน Winget
slug: winget
author: nitpum
date: '2022-01-23T11:50:03.854Z'
lastmod: 2019-08-22T15:20:28.000Z
draft: true
tags: [winget, windows, package-manager]
---

## Winget คืออะไร

## ประโยชน์ของ Winget

```bash
winget install <package>

winget install Google.Chrome
```

## ติดตั้ง

สำหรับ Windows 10 จะลงได้เฉพาะเวอร์ชัน 1709 (build 16299) ขึ้นไป เช็คได้ด้วยการเปิด Run (กดปุ่ม Start + R) จากนั้นพิมพ์ `winver` แล้วกด Enter จะมีหน้าต่างบอกเวอร์ชันขึ้นมา ให้ดูตรง `version` ครับ ถ้าเป็น 1709 หรือมากกว่านั้นแสดงว่าลงได้ครับ

ส่วน Windows 11 ปกติจะลงพร้อมตอนติดตั้งวินโด้อยู่แล้วไม่ต้องทำอะไรเพิ่ม แต่ถ้าเครื่องไหนไม่มีก็ทำตามด้านล่างได้เลย

ทั้ง Windows 10 และ 11 สามารถติดตั้งได้จาก Microsoft Store เลยครับ ค้นหาในนั้นว่า `App Installer` หรือจะกดจาก[ลิงก์นี้](https://www.microsoft.com/en-us/p/app-installer/9nblggh4nns1)ก็ได้ครับ จากนั้นกดติดตั้ง แค่นี้ก็เรียบร้อยพร้อมใช้งาน

## วิธีใช้งาน

```bat
winget install <package> 
```

```bat
winget search <package>
```