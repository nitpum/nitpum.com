---
title: "บันทึก: Cups Proxmox ทำพรินเตอร์เซิฟเวอร์"
author: nitpum
date: 2026-03-15T15:05:31+07:00
lastmod: 2026-03-15T14:02:05.191Z
languageCode: th-TH
tags:
    - Linux
    - Container
    - Proxmox
---

พอดีมีเหตุให้ต้องลง CUPS หรือ printer server บน Proxmox ไว้เลยจะมาเขียนบันทึกไว้สักหน่อยเผื่อตัวผมเองหรือใครมาอ่านจะได้พอทำตามได้

ที่ไปที่มาคร่าวๆ คือ อยากได้พรินเตอร์เซิฟเวอร์ตรงกลางเวลาจะสั่งพิมพ์อะไรจะได้ไม่ต้องยกเครื่องไปต่อสาย หรือใช้มือถือสั่งพิมพ์แบบไร้สายได้เลย

เลยไปค้นข้อมูลเจอว่าจริงๆ มีระบบนี้มานานแล้วชื่อ [OpenPrinting CUPS](https://openprinting.github.io/cups/) แค่เอาไปลงก็ใช้ได้เลย

## Proxmox LXC

พอดีมีเครื่องเซิฟเวอร์ที่ลง Proxmox ไว้อยู่แล้ว แล้วก็ไม่อยากเอา CUPS ไปลงตรงๆ บนเครื่องด้วยอยากเอาใส่ container มากกว่า เลยจบด้วยการเอาไปลงใน unprivileged LXC บน Proxmox แล้ว passthrough USB เข้าไปใน PXC เอา

ผมเลือก Debian มาลงเพราะคุ้นเคยสุด ลงเสร็จหัวใจหลักสำคัญคือต้องไปเซ็ต passthrough USB ทำได้ด้วยการแก้ config lxc ที่ `etc/pve/lxc/<CTID>.conf` ใส่ 2 บรรทัดนี้เพิ่ม

```text
lxc.mount.entry: /dev/bus/usb dev/bus/usb none bind,optional,create=dir
lxc.cgroup2.devices.allow: c 189:* rwm
```

จริงๆ ถ้าจะให้ดีควรจำกัด USB ที่ส่งไปให้เหลือแต่ของ printer เท่านั้นได้กำจัด scope การทำงานหรือถ้าเกิดโดนแฮคมาจะได้ไม่เสียหายอะไรมาก

พอ restart container แล้วเข้าไปพิมพ์คำสั่งใน container 
```sh
lsusb
``` 
ควรจะเห็นรายชื่อ usb ที่ต่ออยู่ทั้งหมด หรือถ้ารัน `lpinfo -v` ก็จะได้ชื่อเครื่องพรินเตอร์เราอย่างของผมเป็น Brother ก็จะเห็นแบบนี้

```sh
direct usb://Brother/<Model-Code>?serial=<Serial>
```

## ลง CUPS

```sh
apt update
apt install cups cups-client cups-filters printer-driver-all
```

เปิด service

```sh
systemctl enable --now cups
```

แก้ config เพื่อให้สามารถ access มาดูสถานะได้แบบไม่ต้อง login แก้ไฟล์ `/etc/cups/cupsd.conf`  ตามนี้

```txt
Port 631
Browsing On
BrowseLocalProtocols dnssd
DefaultShared Yes

<Location />
  Order allow,deny
  Allow @LOCAL
</Location>
```

แก้เสร็จสั่ง restart service

```bash
systemctl restart cups
```

ตอนนี้ควรจะเข้า url cups ได้แล้วลองเข้าไป `http://<container-ip>:631` พวกหน้า info ไม่ควรจะติดล็อคอิน


## ลง Driver

จริงๆ ขั้นตอนนี้ไม่จำเป็นต้องทำก็ได้นะครับถ้าลง CUPS แล้ว driver ที่มีให้มาสามารถใช้ได้เลย เผอิญว่าเครื่อง Brother รุ่นที่ผมใช้ดันไม่มี driver ใน CUPS เลยจำเป็นต้องลงเพิ่มครับ

วิธีการก็ง่ายๆ ครับไปโหลด driver จากเว็บของ Brother เอง https://support.brother.com/g/b/productsearch.aspx?c=us_ot&lang=en ดีที่เขาทำ linux driver มาให้ด้วยแค่โหลด .deb มาลงก็ใช้ได้เลย

```sh
wget <download-deb-url>
dpkg -i <filename>.deb
```

แต่จะติดตรง driver เป็น 32 bit แต่ระบบเป็น 64 bit เลยต้องทำให้ระบบรองรับ

```sh
dpkg --add-architecture i386
apt update
```

พอลง driver เสร็จสั้ง restart อีกรอบ

```sh
systemctl restart cups
```

restart แล้วลองเข้าไปดู Web UI CUPS อีกทีดูตรง Manage printer จะขึ้นเครื่องพรินเตอร์ Brother มาให้เองเลยไม่ต้องทำอะไรเพิ่ม แต่ถ้าไม่ขึ้นก็กดเพิ่มไปตอนใส่ connection url ก็เอา `usb://Brother/<Model-Code>?serial=<Serial>` จากคำสั่ง `lpinfo -v` มา

## ทำ Auto discovery

จริงๆ ถึงขั้นตอนนี้เราสามารถสั่งพรินเตอร์ได้แล้วแหละแต่ว่าคอมและมือถือเราต้องไปกดเพิ่มพรินเตอร์เองแล้วเอาไอพีไปใส่ รู้สึกไม่ค่อยสะดวกเท่าไรอยากให้แบบอยู่ใน Network ขึ้นพรินเตอร์แล้วสั่งได้เลย

ลงคำสั่งด้านล่างเสร็จแล้วคอมกับมือถือเราจะข้นเครื่องพรินเตอร์เลยครับไม่ต้องทำอะไรเพิ่ม

```sh
apt install avahi-daemon
systemctl enable avahi-daemon
systemctl start avahi-daemon

apt install cups-browsed avahi-utils
```
