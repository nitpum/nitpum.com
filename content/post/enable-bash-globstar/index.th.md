---
title: เปิดให้ bash ใช้ globstar (**) ได้
author: nitpum
date: 2022-06-02T07:06:35.205Z
lastmod: 2022-06-29T18:45:31.937Z
tags: []
---

ปกติถ้าใครใช้ macOS ทำงานกับพวก container หรือ Linux อาจจะเจอปัญหาที่ว่าใช้ globstar (`**`, `**/*.ts`) ในเครื่องตัวเองได้ แต่เอาไปใช้ใน Linux ไม่ได้

นั้นก็เพราะว่าใน macOS นั้นใช้ Zsh ซึ่งเปิด globstar ไว้เป็นค่าเริ่มต้นอยู่แล้ว ต่างจาก bash ใน Linux ที่จะปิดไว้

ซึ่งถ้าเราอยากใช้ใน bash ก็สามารถเปิดใช้งานด้วยสำสั่ง shopt (**SH**ell **OPT**ion)

```bash
shopt -s globstar
```
