# Lab L1 Answers

## Q1 - เครื่องมือ
- **ปัญหาที่เจอใน flutter doctor:** พบปัญหา `[X] Android toolchain - Unable to locate Android SDK` และตอนรันแอปครั้งแรกพบปัญหา `Package ndk 28.2.13676358 not found`
- **เครื่องมือ/เอกสารที่ใช้แก้:** ใช้ **SDK Manager** ในโปรแกรม Android Studio เข้าไปกำหนดตำแหน่งโฟลเดอร์ Android SDK และติดตั้ง **Android SDK Command-line Tools (latest)** รวมถึง **NDK (Side by side)** เวอร์ชัน 28.2.13676358 และตรวจสอบผ่านคำสั่ง `flutter doctor`

## Q2 - Reload
- **ผลของ `r` (Hot Reload):** เมื่อกด `r` ข้อความใน AppBar อัปเดตเป็นคำใหม่ แต่ค่า `Likes` ยังคงเป็น **3** เหมือนเดิม เพราะ Hot Reload จะฉีดโค้ดที่แก้ไขเข้าไปใน Dart VM โดยยังคงรักษา State (`_likes`) เดิมในหน่วยความจำเอาไว้
- **ผลของ `R` (Hot Restart):** เมื่อกด `R` ค่า `Likes` ถูกรีเซ็ตกลับเป็น **0** เพราะ Hot Restart จะทำลาย State เดิมทั้งหมดและเริ่มต้นรันแอปใหม่ตั้งแต่ฟังก์ชัน `main()`

## Q3 - โค้ด และ Git
- **ทำไม `_likes++` ต้องใช้ `setState`:** เพราะการเปลี่ยนค่าตัวแปร `_likes++` เพียงอย่างเดียวจะเปลี่ยนแค่ค่าในหน่วยความจำ แต่หน้าจอจะไม่วาดใหม่ การครอบด้วย `setState()` เป็นการแจ้งให้ Flutter framework ทราบว่าข้อมูลภายใน State เปลี่ยนแปลงแล้ว เพื่อสั่งเรียกเมธอด `build()` ให้วาด UI แสดงตัวเลขใหม่บนหน้าจอ
- **อธิบาย 1 Commit:** เลือก commit `"Add like counter with setState"` เป็นการเปลี่ยนคลาส `HomePage` จาก `StatelessWidget` เป็น `StatefulWidget` เพิ่มตัวแปร `_likes` ฟังก์ชัน `_like()` และเพิ่มปุ่ม `FilledButton` เพื่อให้ผู้ใช้กดเพิ่มจำนวน Like และอัปเดตตัวเลขบนหน้าจอได้

## ตารางทดสอบ
| ประเภท | input หรือการกระทำ | ผลที่คาดหวัง | ผลจริง |
| :--- | :--- | :--- | :--- |
| Normal | เปิดแอป | title ไอคอน ชื่อ "Likes: 0" | แสดงแถบ title, ไอคอนคน, ชื่อ-รหัส และ "Likes: 0" ถูกต้อง |
| Normal | กด Like หนึ่งครั้ง | "Likes: 1" | ตัวเลขเปลี่ยนเป็น "Likes: 1" ทันที |
| Boundary | กด Like เร็ว ๆ 20 ครั้ง | "Likes: 20" ไม่มี error | แสดง "Likes: 20" ได้ปกติ ไม่มี error |
| Boundary | หมุนจอเป็นแนวนอน | ยังอยู่กลางจอ ไม่ overflow | เนื้อหาจัดกึ่งกลางจอปกติ ไม่มีแถบเตือน overflow |
| Reload | กด 3 ครั้ง แล้ว r แล้ว R | หลัง r ได้ 3 - หลัง R ได้ 0 | หลังกด r ยังคงเป็น 3 และหลังกด R รีเซ็ตกลับเป็น 0 |
| Failure | ปิด emulator แล้ว flutter run | ข้อความว่า ไม่พบ device | ระบบแจ้งว่าไม่พบ Android device |

## การใช้ AI
- ใช้ AI (Gemini) ช่วยอธิบายขั้นตอนการตั้งค่า Android SDK/NDK, ลำดับคำสั่ง Git ในแต่ละ commit และแนวทางการตรวจสอบโครงสร้างโค้ด Flutter โดยพิมพ์และทดสอบรันโค้ดด้วยตนเองทุกขั้นตอน
