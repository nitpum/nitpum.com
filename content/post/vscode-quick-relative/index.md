---
title: Vscode Quick Open Relative เปลี่ยนไฟล์เร็วขึ้น ไม่ต้องใช้เมาส์
author: nitpum
date: 2022-08-30T15:30:11Z
lastmod: 2022-08-30T19:36:43.099Z
tags:
  - vscode
  - vscode-extension
toc: false
---

เวลาใช้ VSCode ช่วงที่เขียนโค้ดเพลินๆ มือก็ไม่ค่อยอยากปล่อยออกจากคีย์บอร์ดเท่าไร แต่มันก็จะมีช่วงที่ต้องปล่อยมือไปจับเมาส์เพื่อเปิดไฟล์อื่น ถึงจะเสียเวลาไม่มากแต่ก็ต้องยกมืออกแล้วเลื่อนไปจับเมาส์แล้วค่อยเลื่อนมือกลับมาที่คีย์บอร์ดอีกทีทำให้ชัดใจอยู่พอสมควร ส่วนใหญ่เลยจะใช้ `Ctrl + P` พิมพ์หาชื่อไฟล์ไม่ก็พิมพ์ path ไฟล์ไปแทน

ข้อเสียคือ บางทีก็แค่อยากเปิดไฟล์ในโฟลเดอร์เดียวกันกับไฟล์ปัจจุบันที่เปิดอยู่ แต่ชื่อไฟล์มันซ้ำกับที่อื่นเลยต้องพิมพ์ path แทน แต่ path ดันยาว ตรงนี้ก็จะทำให้เสียเวลาไปอีก

เผื่อนึกภาพไม่ออกขอยกตัวอย่างด้วย Project structure ตามด้านล่างนี้ละกัน

```bash
project
|- src
	|- components
		|- Button
			|- index.tsx
			|- index.test.tsx
			|- types.ts
			|- styled.ts
			|- constants.ts
		|- Card
			|- index.tsx
			|- index.test.tsx
			|- styled.ts
	|- hooks
		|- useDoSomething
			|- index.ts
			|- index.test.ts
	|- utils
		|- extractIdFromData
			|- index.ts
			|- index.test.ts
|- scripts
|- build
|- ...
```

ตัวอย่างนี้จะเป็น Project structure ของ React (โพสต์นี้ขอไม่พูดถึงนะว่าแบบนี้มันดียังไง) แต่จะเห็นได้ว่าโค้ดจะถูกเก็บเอาไว้ที่ `src/` แล้วข้างในจะแบ่งของออกตามประเภท (components, hooks, utils) เข้าไปข้างในอีกก็จะแบ่งเป็นโฟลเดอร์ตามหน้าที่อีกที `src/components/Button` แล้วในนั้นค่อยเป็นไฟล์โค้ดจริงๆ ที่เกี่ยวกับเรื่องนั้นๆ `src/components/Button/index.ts`

ทีนี้เนี่ยถ้ากำลังเขียนโค้ดที่ `src/components/Button/index.ts` แล้วอยากจะสลับไปเขียนเทสก็ต้องพิมพ์ path ไปที่ `src/components/Button/index.test.ts` อยากแก้ style ต่อก็พิมพ์ไปที่ `src/components/Button/styled.ts` อีกที ซึ่งมันช้าพอสมควร

{{< video src="without-quick-relative" >}}

## Quick Open Relative

[Quick Open Relative](https://marketplace.visualstudio.com/items?itemName=gpaul.quickOpenRelative) เป็นส่วนเสริมตอนที่เรากดเปิดไฟล์ด้วย `Ctrl + P` ตัว Quick Open Relative จะเติม path ของไฟล์ปัจจุบันที่เราเปิดอยู่ให้เลย ช่วยให้เราไม่ต้องมานั่งพิมพ์ path เอง ที่เหลือคือเราจะพิมพ์ต่อเองหรือจะกดลูกศรเลือกไฟล์เอาเลยก็ได้

{{< video src="with-quick-relative" >}}

แต่ว่าโดย default แล้วส่วนเสริมนี้ไม่ได้ตั้งปุ่มรัดมาให้ เราต้องไปตั้งปุ่มรัดเอง

1. File > Preference > Keyboard Shortcuts
2. ค้นว่า `quickOpenRelative.quickOpenRelative`
3. กดแก้ไข ตั้งปุ่มที่ต้องการ เช่น `Ctrl + P`
4. จริงๆ เท่านี้ก็เรียบร้อยแล้ว แต่ส่วนตัวไม่อยากให้มันทำงานตลอดทุกครั้งที่กด `Ctrl + P` เลยจะเพิ่มเงื่อนไขให้มันหน่อย
   ให้ทำงานแค่ตอนที่เราโฟกัสอยู่ที่ไฟล์เท่านั้น ถ้าไม่ได้โฟกัสไฟล์เช่นกำลังโฟกัส terminal อยู่หรือกำลังดู git history ก็ให้เปิด `Ctrl + P` ปกติแทน
   คลิกขวา > Change When Expression > ใส่เป็น `editorTextFocus`
5. เสร็จสมบูรณ์

หรือใครที่ตั้งค่าด้วย `keybindins.json` ก็ก็อปอันนี้ไปใช้ได้เลย

```json
{
	"key": "ctrl+p",
	"command": "quickOpenRelative.quickOpenRelative",
	"when": "editorTextFocus"
}
```

เท่านี้ก็ช่วยทำให้เราสลับไปเปิดไฟล์อีกเร็วขึ้นแล้ว!!!

{{< video src="even-quicker" >}}
