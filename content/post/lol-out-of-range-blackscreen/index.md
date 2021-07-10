---
title: 'LoL แก้หน้าจอ Out of Range หรือจอดำ Black screen '
date: 2017-06-29T12:30:00.004+07:00
draft: false
aliases: [ "/2017/06/lol-out-of-range-blackscreen.html" ]
tags : [blog, game, แก้ปัญหา, เกม, hwo-to, league of legends, LoL]
disableToc: true
---
  
ปัญหานี้แก้ด้วยการปรับหน้าจอเกมออกจากโหมดเต็มหน้าจอ(Full screen) เป็นโหมด Borderless หรือ โหมด Window โดยวิธีการก็ทำได้ดังนี้  

วิธีแก้
-------

**วิธีที่ 1 :** กดปุ่ม **Alt + Enter** ในขณะที่จอดำ เพื่อให้ตัวเกมออกจากโหมดเต็มจอ(Full screen)  
**วิธีที่ 2 :** หากวิธีที่ 1 ไม่ได้ผลให้ให้ทำตามดังต่อไปนี้  

  

1.  เข้าไปในโฟลเดอร์เกม League of Legends ที่ติดตั้งไว้  
    โดยปกติแล้วจะอยู่ที่ **C:/Program Files (x86)/GarenaLoLTH/**
2.  จากนั้นเข้าไปที่ **/Apps/LoLTH/Game/Config**
3.  เปิดไฟล์ **game.cfg** ด้วย Notepad
4.  ค้นหาคำว่า **WindowMode**
5.  ให้แก้จาก **WindowMode=0** เป็น **WindowMode=2** ดังรูป {{< figure src="WindowMode2.jpg" >}}
6.  จากนั้น **save** และ **เปิดเกมใหม่** ก็เรียบร้อยแล้วครับ  
    แต่อย่าลืมไปลองทดสอบดูก่อนนะครับ :)