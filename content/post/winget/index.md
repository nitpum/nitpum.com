---
title: Winget คืออะไร? พร้อมวิธีติดตั้งและใช้งาน
slug: winget
author: nitpum
date: '2022-02-13T11:50:03.854Z'
tags: [winget, package-manager, windows]
---

## Winget คืออะไร

Winget คือ package manager หรือตัวจัดการโปรแกรมในเครื่องเรานั้นเอง ไม่ว่าจะเป็นการลงโปรแกรมใหม่, ลบโปรแกรม หรืออัพเดทโปรแกรมไปเป็นเวอร์ชันใหม่ ซึ่งที่ว่ามานี้ทำผ่าน command line ทั้งหมดเลย เรียกได้ว่าไม่ต้องแตะเมาส์กันเลยทีเดียว

ถ้าให้เทียบกับ OS อื่นฝั่ง macOS ก็คือ Homebrew หรือถ้าฝั่ง Linux ก็จะเป็น apt, yum, pacman ในส่วนของ Windows ก็จะเป็น winget นั้นเอง

ใครที่ยังนึกไม่ออกลองนึกถึง package manager ที่ใช้ในแต่ละภาษาดู อย่าง javascript มี npm, python มี pip, rust มี cargo, java มี maven, c# มี nuget ซึ่งอย่างที่รู้กันว่า package manager ของแต่ละภาษาก็จะคอยช่วยจัดการในการโหลดตัว dependecy ต่างๆ ที่จำเป็นมาให้ทำให้เราไม่ต้องมาจัดการเรื่องพวกนี้เอง แต่ว่านั้นก็เป็น package manager ระดับภาษาใช่ไหมละ winget นั้นใหญ่กว่านั้นที่จะจัดการระดับโปรแกรมในเครื่องนั้นเอง

สำหรับใครที่สนใจเบื้องหลังการทำงานของ winget Microsoft ได้เปิดเผยซอร์สโค้ดไว้บน [Github](https://github.com/microsoft/winget-cli) แล้วสามารถเข้าไปอ่านโค้ดได้เลย

{{< notice note >}}

แต่ใช่ว่า Windows จะไม่เคยมี package manager มาก่อน เพราะจริงๆ ก็มีทั้ง [Scoop](https://scoop.sh/), [Chocolatey](https://chocolatey.org/) และ [AppGet](https://appget.net/) อยู่ก่อนหน้านี้แล้ว แต่ทั้งนี้ก็ไม่ใช่ของ Microsoft เอง

{{</ notice >}}

## ประโยชน์ของ Winget

แล้วมันต่างจากโหลดโปรแกรมมาลงเองยังไง? สมมุติว่าเราอยากลงโปรแกรม 10 โปรแกรม ตามปกติเราก็ต้องเข้า Google พิมพ์ค้นโปรแกรมที่เราจะลงและกดดาวน์โหลดโปรแกรมมาลงเองทีละตัว แต่ถ้าเราใช้ winget ก็แค่เปิด cmd แล้วพิมพ์คำสั่งเหล่านี้ลงไป

```bat
winget install Google.Chrome
winget install Discord.Discord
winget install SlackTechnologies.Slack
winget install Microsoft.VisualStudioCode
winget install Git.Git
winget install Golang.Go
winget install OpenJS.NodeJS
winget install EclipseAdoptium.Temurin.16
winget install Microsoft.dotnet
winget install Docker.DockerDesktop
```

กด Enter ที่เหลือปล่อย winget จัดการได้เลย เดี๋ยวมันจะไปโหลดโปรแกรมมาลงให้

ด้วยความที่คำสั่งที่พิมพ์เป็นตัวหนังสือทำให้เราสามารถก๊อปปี้เก็บเอาไปเปิดดูเวลาลง Windows ใหม่ได้ 
หรืออยากให้เพื่อนลงโปรแกรมแบบเดียวกันก็ส่งเป็นข้อความไปให้ได้

นอกจากนี้เรายังเอาคำสั่งพวกนี้ไป[สร้างเป็นสคริปต์เก็บไว้](#ทำสครปตลงโปรแกรม)เอาไปรันที่อื่นได้เลยจะได้ไม่ต้องก๊อปวางคำสั่ง

ข้อดีอีกอย่างคือ เราไม่ต้องไปหาลิงก์ดานว์โหลดตามเว็บไซต์ต่างๆ เองที่อาจโหลดผิดลิงก์หรือโดนฝั่งไวรัสมากับไฟล์ติดตั้ง ในส่วนนี้ winget เองก็ยังมีการเช็คค่า hash ป้องกันการปลอมแปลงไฟล์ระหว่างโหลดให้อีกด้วย


## ติดตั้ง

Winget ใช้ได้ตั้งแต่ Windows 10 ขึ้นไป (Windows 10, Windows 11) ใครที่ใช้ Windows ต่ำกว่านี้ไม่สามารถลง Winget ได้

สำหรับ Windows 10 จะลงได้เฉพาะเวอร์ชัน 1709 (build 16299) ขึ้นไป เช็คได้ด้วยการเปิด Run (กดปุ่ม Start + R) จากนั้นพิมพ์ `winver` แล้วกด Enter จะมีหน้าต่างบอกเวอร์ชันขึ้นมา ให้ดูตรง `version` ถ้าเป็น 1709 หรือมากกว่านั้นแสดงว่าลงได้

ส่วน Windows 11 ปกติจะลงพร้อมตอนติดตั้งวินโด้อยู่แล้วไม่ต้องทำอะไรเพิ่ม แต่ถ้าเครื่องไหนไม่มีก็ทำตามด้านล่างได้เลย

ทั้ง Windows 10 และ 11 สามารถติดตั้งได้จาก Microsoft Store ค้นหาในนั้นว่า `App Installer` หรือจะกดจาก[ลิงก์นี้](https://www.microsoft.com/en-us/p/app-installer/9nblggh4nns1)ก็ได้ กดเข้าไปแล้วกด Get และ Install แค่นี้ก็เรียบร้อยพร้อมใช้งาน

## วิธีใช้งาน

เปิด Command Prompt หรือ Powershell ขึ้นมาแล้วพิมพ์คำสั่งที่เราต้องการได้เลย

### ค้นหารายชื่อโปรแกรม

เช็คดูว่าโปรแกรมที่อยากลงมีใน winget หรือยังด้วยคำสั่งนี้

```bat
winget search <package>
```

อย่างถ้าอยากรู้ว่ามี VSCode หรือเปล่าก็พิมพ์แบบนี้

```bat
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

เราจะได้ตารางที่แบ่งคอลลัมมาให้ตามนี้
- **Name** คือ ชื่อโปรแกรมที่เรียกกันทั่วไป
- **Id** คือ ไอดีเฉพาะของโปรแกรมนั้นที่ไม่ซ้ำกับโปรแกรมอื่น สาารถเอาไปใช้อ้างอิงตอนพิมพ์คำสั่งอื่นได้
- **Version** คือ เวอร์ชันล่าสุดที่ติดตั้งได้
- **Match** คือ คำที่เราค้นไปตรงกับโปรแกรมนี้ยังไง
- **Source** คือ โหลดโปรแกรมนี้ได้จาก repository ไหนได้บ้าง

### ติดตั้งโปรแกรม

อยากจะลงโปรแกรมอะไรก็พิมพ์คำสั่งแบบนี้ได้เลย

```bat
winget install <package>
```

สมมุติอยากลง VSCode ก็พิมพ์แบบนี้

```bat
winget install vscode
```

กรณีที่มีชื่อโปรแกรมคล้ายกันเยอะ เราสามารถเจาะจงโปรแกรมได้ด้วย `--id <id>`

```bat
winget install --id <id>

:: ตัวอย่าง
winget install --id Microsoft.VisualStudioCode
```

หรือถ้าอยากลงโปรแกรมเวอร์ชันที่ต้องการก็สามารถระบุเลขเวอร์ชันได้ด้วย `--version <version>`

```bat
winget install <package> --version <version>

:: ตัวอย่าง
winget install vscode --version 1.64.0

:: หรือจะใช้คู่กับ --id <id> ก็ได้
winget install --id Microsoft.VisualStudioCode --version 1.64.0
```

### อัพเดทโปรแกรม

อัพเดทโปรแกรมเป็นเวอร์ชันล่าสุด

```bat
winget upgrade <package>

:: ตัวอย่าง
winget upgrade vscode
```

อัพเดทโปรแกรมไปเวอร์ชันที่ต้องการด้วย `--version <version>`

```bat
winget upgrade <package> --version <version>

:: ตัวอย่าง
winget upgrade vscode --version 1.64.0
```

### ลบโปรแกรม

```bat
winget uninstall <package>
::ตัวอย่าง
winget uninstall vscode

:: หรือจะใช้ --id <id> ก้ได้
winget uninstall --id Microsoft.VisualStudioCode
```

### แบ็คอัพรายชื่อโปรแกรม (Export)

winget เองสามารถเซฟลิตส์โปรแกรมออกมาเป็นไฟล์เพื่อใช้แบ็คอัพได้ กรณีที่เราลงวินโดใหม่ก็ import ไฟล์นี้แล้วเดี๋ยว winget จะลงโปรแกรมให้ตามในไฟล์เลย

สำหรับคำสั่งเราแค่ระบุที่อยู่ที่อยากให้เซฟไฟล์ไว้พร้อมกับใส่ชื่อไฟล์ ส่วนนามสกุลไฟล์จะใส่เป็นอะไรก็ได้ (ข้างในจะใช้ฟอตแมตเป็น JSON)

```bat
winget export <filepath>

:: ตัวอย่าง
winget export D:\winget.json
```

### ลงโปรแกรมจากแบ็คอัพ (Import)

กรณีที่เราลงวินโดใหม่ก็ import ไฟล์นี้แล้วเดี๋ยว winget จะลงโปรแกรมให้ตามในไฟล์เลย

```bat
winget import <filepath>

:: ตัวอย่าง
winget import D:\winget.json
```

## ทำสคริปต์ลงโปรแกรม

นอกเหนือจาก export กับ import ที่ Winget มีมาให้แล้ว ด้วยความที่ทุกคำสั่งมันก็เป็นแค่ตัวหนังสือธรรมดา เราเลยสามารถเซฟเก็บเป็นไฟล์ได้

แต่ถ้าเซฟเป็น .bat ก็จะเปลี่ยนจากไฟล์ text ธรรมดาเป็นไฟล์สคริปต์ที่แค่กดเปิดก็จะรันตามคำสั่งที่เราพิมพ์เอาไว้ให้เลย เวลาจะใช้ก็แค่กดดับเบิ้ลคลิกเพื่อรันไฟล์แค่นั้น ไม่ต้องก็อปคำสั่งเอามาวางบน cmd เองอีกต่อไป

ส่วนวิธีทำก็ง่ายมักๆ เปิด Text Editor ตัวไหนก็ได้ขึ้นมา (Notepad, VSCode, Notepad++ หรืออื่นๆ) จากนั้นก็พิมพ์คำสั่งลงไป โดยที่หนึ่งบรรทัดคือหนึ่งคำสั่ง เช่น อยากลง VSCode และ Git ก็จะเป็นแบบนี้

```bat
winget install vscode
winget install git
```

ที่เหลือก็แค่เซฟเป็นไฟล์ .bat ก็เสร็จแล้ว จะเอาไฟล์นี้ไปใช้ที่ไหนก็ได้ ก๊อปใส่ Flash drive ไปรันเครื่องเพื่อนก็ยังได้ เวลาจะใช้ก็แค่กดดับเบิ้ลคลิกแล้วเดี๋ยวที่เหลือมันรันตามคำสั่งให้เลย

อ๋อ จริงๆ มันใช้ได้ทุกคำสั่งเลยนะไม่ได้เฉพาะแค่ install อย่างเดียว อย่างถ้าอยากลบ Discord ก็พิมพ์เพิ่มไปเป็นแบบนี้

```bat
winget install VSCode
winget install git
winget uninstall discord
```