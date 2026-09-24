# เว็บติดตั้งแยกจากเว็บกล้องเดิม

สร้าง repository ใหม่ชื่อ `pathum-water-install` แบบ Public แล้วเปิด GitHub Pages
จาก branch `main`, folder `/(root)` จะได้เว็บ:

https://saravuthpongsalee.github.io/pathum-water-install/

เว็บกล้องเดิมที่ https://saravuthpongsalee.github.io/pathum-water/ ไม่ต้องแก้ไข
และยังอัปเดตภาพตาม workflow ของเดิมต่อไป เว็บใหม่มีเฉพาะหน้าแฟลช USB
กับลิงก์กลับไปที่เว็บกล้อง ไม่มีซอร์ส `.ino` อยู่ในชุด ZIP นี้

## ตั้งเว็บติดตั้ง (เจ้าของทำครั้งเดียว)

1. เข้า https://github.com/new สร้าง repository ชื่อ `pathum-water-install`
   เลือก Public ติ๊ก Add a README file แล้วกด Create repository
2. ในหน้า Code กด Add file → Upload files เปิดโฟลเดอร์ที่แตก ZIP นี้
   เลือกไฟล์/โฟลเดอร์ **ภายใน** ทั้งหมดแล้วลากลงหน้าเว็บ อย่าอัปโหลด ZIP ทั้งก้อน
   กด Commit changes ต้องเห็น `index.html`, `manifest.json`, `firmware/.gitkeep`
   ที่รากของ repository
3. เข้า Settings → Pages เลือก Source `Deploy from a branch`, Branch `main`,
   Folder `/(root)` แล้วกด Save รอเผยแพร่เว็บ

เว็บใหม่จะยังซ่อนปุ่มติดตั้งจนกว่า `firmware/merged.bin` จะมีอยู่จริง

## สร้างไฟล์โปรแกรมและทดสอบ

1. ใน repository โปรแกรมเดิม `pathum-water` ให้รัน workflow
   `Build ESP32-CYD firmware for web install` โดย **ไม่ติ๊ก publish**
   ถ้ายังไม่มี workflow นี้ให้อัปโหลดไฟล์ `build-firmware.yml` ที่ได้รับก่อนหน้านี้
   ที่ `.github/workflows/build-firmware.yml`
2. ดาวน์โหลด Artifact `pathum-cyd-st7789-test` จากงานที่ขึ้นสีเขียว แตก ZIP
   จะได้ `merged.bin` (ไม่ใช่ .hex)
3. ทดสอบกับบอร์ด ESP32-CYD จอ ST7789 + XPT2046 ของเจ้าของก่อน
   ที่ https://espressif.github.io/esptool-js/ โดยเลือกไฟล์ `merged.bin`
   และ flash address `0x0` ตรวจจอ/สัมผัส/Wi-Fi และภาพกล้อง
4. ไปที่ repository ใหม่ `pathum-water-install` คลิก `firmware` →
   Add file → Upload files เลือกเฉพาะ `merged.bin` และ Commit changes
   รอ GitHub Pages เผยแพร่ commit แล้วรีเฟรชหน้าเว็บติดตั้ง

## ผู้ใช้ทั่วไป

ต่อบอร์ดรุ่นที่ตรงกันด้วยสาย USB ส่งข้อมูล → เปิดเว็บติดตั้งด้วย Chrome/Edge
บนคอม → กดติดตั้ง → เลือกพอร์ต COM → รอจนเสร็จ เมื่อเปิดเครื่องให้มือถือ
ต่อ Wi-Fi `PATHUM-XXXXXXXX` ตามรหัสบนจอ เปิด `http://192.168.4.1`
กรอก Wi-Fi 2.4 GHz และ URL ภาพกล้องเดิม:

https://saravuthpongsalee.github.io/pathum-water

**ขอบเขตความเป็นส่วนตัว:** repository เดิม `pathum-water` ยังเป็น Public
และเคยมีไฟล์ `.ino` ดังนั้นผู้อื่นอาจยังเปิดดูซอร์สเดิมได้ เว็บติดตั้งใหม่
ไม่ได้แจก `.ino` แต่ไม่ได้ทำให้ซอร์สใน repository เดิมกลายเป็นความลับ
ไฟล์ไบนารีที่แจกยังสามารถถูกวิเคราะห์ได้
