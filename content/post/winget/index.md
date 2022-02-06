---
title: ติดตั้งและใช้งาน Winget
slug: winget
author: nitpum
date: '2022-02-06T11:50:03.854Z'
lastmod: 2019-08-22T15:20:28.000Z
draft: true
tags: [winget, windows, package-manager]
---

## Winget คืออะไร

Winget เป็น package manager หรือตัวจัดการโปรแกรมในเครื่องเรา ไม่ว่าจะเป็นการลงโปรแกรมใหม่, ลบโปรแกรมที่เคยติดตั้งออกไปแล้ว หรือเป็นอัพเดทโปรแกรมไปเป็นเวอร์ชันใหม่ ซึ่งทั้งหมดที่ว่ามานี้เราสามารถทำได้ด้วยการพิมพ์คำสั่ง winget ผ่าน command line โดยที่เราไม่จำเป็นต้องแตะเมาส์เลยด้วยซ้ำ 

ใครที่ยังนึกไม่ออกลองนึกถึง package manager แต่ละภาษา อย่าง javascript มี npm, python มี pip, rust มี cargo, java มี maven, c# มี nuget ทั้งหมดนี้เทียบได้กับ winget เลย แต่ตัว winget จะทำหน้าที่จัดการโปรแกรมทั้งเครื่องมากกว่าจะจัดการแค่เฉพาะภาษานั้นๆ

ถ้าเทียบกับ OS อื่นอย่าง Linux คือ apt, yum, pacman และ macOS คือ homebrew ตอนนี้ของ Windows ก็จะเป็น winget นั้นเอง

จริงๆ Windows เองก็มี package manager อยู่ก่อนหน้าแล้วทั้ง [Scoop](https://scoop.sh/) และ [Chocolatey](https://chocolatey.org/) แต่ทั้งคู่นั้นสร้างโดยชุมชนไม่ใช่ของ Microsoft โดยตรง

แต่ winget นั้นเ Microsoft เป็นคนสร้างขึ้นมาเองและสนับสนุนโดยตรง พร้อมทั้งเปิดเผยซอร์สโค้ดไว้บน [Github](https://github.com/microsoft/winget-cli) ทำให้ winget ดูจะมีอนาคตมากกว่าตัวอื่น

## ประโยชน์ของ Winget

บางคนอาจจะนึกไม่ออกว่ามันต่างจากโหลดโปรแกรมมาลงเองยังไง สมมุตว่าเราพึ่งลงวินโดใหม่ยังไม่ได้ลงโปรแกรมอะไรเลย ตามปกติเราก็ต้องไปไล่โหลดมาลงเองทีละตัว แต่ถ้าเราใช้ winget เราก็แค่เปิด cmd ขึ้นแล้วพิมพ์คำสั่งเหล่านี้ลงไป

```bat
winget install Google.Chrome
winget install Discord.Discord
winget install Microsoft.VisualStudioCode
winget install Git.Git
winget install Golang.Go
winget install OpenJS.NodeJS
winget install Docker.DockerDesktop
winget install Valve.Steam
```

กด Enter แล้วปล่อย winget ทำงาน เดี๋ยวมันจะไปโหลดโปรแกรมมาลงให้เราเองแค่นี้ก็ไม่ต้องเสียเวลาเข้าเว็บไปโหลดทีละโปรแกรมมาลงเองแล้ว หรือถ้าขี้เกียจพิมพ์เราก็อปคำสั่งพวกนี้เก็บไว้ใช้ได้ 

นอกจากนี้เรายังสามารถก็อปคำสั่งส่งต่อให้เพื่อนเราได้ 

ในกรณีที่เราอยากให้เพื่อนลงโปรแกรมที่ต้องการไม่ต้องไป
หรืออยากให้เพื่อนลงโปรแกรมแบบเดียวกันก็ส่งคำสั่งเป็นข้อความไปให้ได้ เพื่อนก็แค่ก็อปคำสั่งไปใช้

นอกจากนี้เรายังเอาคำสั่งพวกนี้ไป[สร้างเป็นสคริปไปรันที่อื่น](#เกบสครปตเปนไฟลไปใชทอน)ได้ง่ายๆ อีกด้วย


## ติดตั้ง

สำหรับ Windows 10 จะลงได้เฉพาะเวอร์ชัน 1709 (build 16299) ขึ้นไป เช็คได้ด้วยการเปิด Run (กดปุ่ม Start + R) จากนั้นพิมพ์ `winver` แล้วกด Enter จะมีหน้าต่างบอกเวอร์ชันขึ้นมา ให้ดูตรง `version` ครับ ถ้าเป็น 1709 หรือมากกว่านั้นแสดงว่าลงได้

ส่วน Windows 11 ปกติจะลงพร้อมตอนติดตั้งวินโด้อยู่แล้วไม่ต้องทำอะไรเพิ่ม แต่ถ้าเครื่องไหนไม่มีก็ทำตามด้านล่างได้เลย

ทั้ง Windows 10 และ 11 สามารถติดตั้งได้จาก Microsoft Store เลยครับ ค้นหาในนั้นว่า `App Installer` หรือจะกดจาก[ลิงก์นี้](https://www.microsoft.com/en-us/p/app-installer/9nblggh4nns1)ก็ได้ครับ จากนั้นกดติดตั้ง แค่นี้ก็เรียบร้อยพร้อมใช้งาน

## วิธีใช้งาน

เปิด Command Prompt หรือ Powershell ขึ้นมาแล้วพิมพ์คำสั่งที่เราต้องการได้เลย

### คำสั่งค้นหารายชื่อโปรแกรม

ณ ตอนนี้ที่เขียนบทความด้วยความที่ winget ยังเปิดตัวมาได้ไม่นาน บางโปรแกรมอาจจะยังไม่มีใน repository ของ winget แนะนำให้ลองค้นใน winget ดูก่อนครับว่ามีโปรแกรมที่เราต้องการหรือเปล่า

เราสามารถเช็คได้ด้วยคำสั่งด้านล่างนี้เลย

```bat
winget search <package>

:: ตัวอย่าง 
winget search vscode
```

ผลลัพธ์จะได้ประมาณนี้

```bat
Name                                  Id                                  Version      Match                    Source
----------------------------------------------------------------------------------------------------------------------
Microsoft Visual Studio Code          Microsoft.VisualStudioCode          1.64.0       Moniker: vscode          winget
MrCode                                zokugun.MrCode                      1.62.3.21323 Tag: vscode              winget
VSCodium                              VSCodium.VSCodium                   1.64.0       Tag: vscode              winget
微信开发者工具                        Tencent.wechat-devtool              1.05.2108130 Tag: vscode              winget
Huawei QuickApp IDE                   Huawei.QuickAppIde                  11.4.2       Tag: vscode              winget
TheiaBlueprint                        EclipseFoundation.TheiaBlueprint    1.16.0       Tag: vscode              winget
Microsoft Visual Studio Code Insiders Microsoft.VisualStudioCode.Insiders 1.65.0       Moniker: vscode-insiders winget
```

จากผลลัพธ์
- Name คือ ชื่อโปรแกรมที่เรียกกันทั่วไป
- Id คือ id เฉพาะของโปรแกรมนั้นที่ไม่ซ้ำกับโปรแกรมอื่น สามารถเอาไปใช้บอกตอนลงโปรแกรมได้กรณีที่ชื่อโปรแกรมซ้ำกัน
- Version คือ เวอร์ชันล่าสุดที่ติดตั้งได้
- Match

### คำสั่งติดตั้งโปรแกรม

```bat
winget install <package>

:: ตัวอย่าง
winget install vscode
```

กรณีที่มีชื่อโปรแกรมคล้ายกันหลายอัน เราสามารถเจาะจงให้ลงโปรแกรมได้ด้วยการบอก `package-id`

```bat
winget install --id <package-id>

:: ตัวอย่าง
winget install --id Microsoft.VisualStudioCode
```

หรืออยาก


```bat
winget install --id <package-id> --version <version>

:: ตัวอย่าง
winget install --id Microsoft.VisualStudioCode --version 1.64.0
```

### คำสั่งลบโปรแกรม

```bat
winget 
```