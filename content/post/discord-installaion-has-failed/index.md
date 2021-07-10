---
title: 'แก้ปัญหา Discord ลงไม่ได้ Installaion has failed'
date: 2017-06-17T20:11:00.004+07:00
draft: false
aliases: [ "/2017/06/discord-installaion-has-failed.html" ]
tags : [blog, วิธีการ, game, แก้ปัญหา, article, discord, how-to, ติดตั้งโปรแกรม]
disableToc: true
---
  
สวัสดีครับบทความนี้จะมาบอก**วิธีแก้ปัญหา** สำหรับใครที่ติดตั้ง Discord แล้วพบปัญหา **Installation has failed**  เพื่อนผมพึง Reset this PC เพื่อล้างคอมลง Windows ใหม่แล้วเจอปัญหานี้ก็เลยแชร์วิธีการแก้เผื่อมีประโยชน์กับคนที่ติดปัญหานี้เหมือนกัน  

[![](https://4.bp.blogspot.com/-5G8tFZbxAic/WUUfl_kUVrI/AAAAAAAAB3k/TsXFNN3GPeEB3R3BF-GdAWUH9w3Oh-5MwCLcBGAs/s320/error.jpg)](https://4.bp.blogspot.com/-5G8tFZbxAic/WUUfl_kUVrI/AAAAAAAAB3k/TsXFNN3GPeEB3R3BF-GdAWUH9w3Oh-5MwCLcBGAs/s1600/error.jpg)

  
## สาเหตุ

ปัญหานี้เกิดจากการที่มีตัวไฟล์ของโปรแกรม Discord อยู่บนเครื่องอยู่แล้วแต่ตัวโปรแกรมไม่สมบูรณ์หรือเสียหาย ส่วนมากมักจะเจอกับคนที่พึ่งลง Windows ใหม่ หรือ Reset Windows มาหรือมีไฟล์โปรแกรมเก่าค้างอยู่ในเครื่อง  

## วิธีแก้

ต้องลบตัวไฟล์โปรแกรมที่มีอยู่ทั้งหมดออกไปครับ (โดยปกติแล้วจะอยู่ที่ %AppData%/Discord และ %AppData%/../local/Discord)  

1.  เช็คให้แน่ใจว่าโปรแกรมไม่ได้ค้างเปิดอยู่ในเครื่องรวมไปถึง**ไม่ได้เปิดในบราวเซอร์**ด้วยครับ เช็คได้จาก **Task manager** ครับ (กดปุ่ม Ctrl + Shift + Esc)  
    อย่าลืมกด **More details ด้วยนะครับ**  
    ถ้าเปิดอยู่ก็กด End task ไปครับ  
    
    [![](https://1.bp.blogspot.com/-eMBkioQR0yA/XKm-VI736QI/AAAAAAAAF5M/-2cBv9YhICIVo6_SINeGDyDeF6q1ARJTwCLcBGAs/s320/task-manager-more-details.png)](https://1.bp.blogspot.com/-eMBkioQR0yA/XKm-VI736QI/AAAAAAAAF5M/-2cBv9YhICIVo6_SINeGDyDeF6q1ARJTwCLcBGAs/s1600/task-manager-more-details.png)
    
      
    [![](https://1.bp.blogspot.com/-KQ0yB4Ls94U/WUUfqC2CopI/AAAAAAAAB3o/_LcMlmOQ0CUgmNs4s81m7JhQSu8-7VoLACLcBGAs/s500/taskmanger.jpg)](https://1.bp.blogspot.com/-KQ0yB4Ls94U/WUUfqC2CopI/AAAAAAAAB3o/_LcMlmOQ0CUgmNs4s81m7JhQSu8-7VoLACLcBGAs/s1600/taskmanger.jpg)
2.  เมื่อโปรแกรมไม่ได้เปิดอยู่ก็เริ่มลบโปรแกรมกันครับ
3.  เปิด **Run** ขึ้นมา (กดปุ่ม Start + R) (ปุ่ม Start คือปุ่มรูป ธง ด้านซ้ายล่างของแป้นพิมพ์ครับ)
4.  พิมพ์ในช่องว่า **%appdata%** แล้วกด **OK**  
    [![](https://3.bp.blogspot.com/-9ISF6BT7kEU/WUUfunuEDxI/AAAAAAAAB3s/wYHvbtUtmPcwhjU0x6VIX3GMjMuMW7IzwCLcBGAs/s320/windows_run.jpg)](https://3.bp.blogspot.com/-9ISF6BT7kEU/WUUfunuEDxI/AAAAAAAAB3s/wYHvbtUtmPcwhjU0x6VIX3GMjMuMW7IzwCLcBGAs/s1600/windows_run.jpg)
5.  จะขึ้นหน้าต่างใหม่ขึ้นมา จากนั้นหาโฟลเดอร์ **Discord** แล้ว **Delete** ทิ้งไปเลยครับ  
    (ถ้าลบไม่ได้แสดงว่าตัวโปรแกรมยังเปิดอยู่ครับให้ปิดไปก่อน)
6.  จากนั้นเปิด **Run** ขึ้นมาอีกทีครับ
7.  คร่าวนี้พิมพ์ว่า **%appdata%/../Local** แล้วกด **OK**
8.  จะมีหน้าต่างขึ้นมาหาโฟลเดอร์ **Discord** แล้ว **Delete** ทิ้งไปครับ
9.  **Restart** คอมใหม่ แค่นี้ก็เรียบร้อยแล้วครับ