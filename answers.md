# COE67-332 Lab L1

ชื่อ: Nontaphat Petgorn  
รหัสนักศึกษา: 67115253

## Q1: เครื่องมือ

จากการรัน flutter doctor พบว่ายังไม่ได้ติดตั้ง Visual Studio แต่เนื่องจากงานนี้เป็นการพัฒนาแอปบน Android จึงไม่จำเป็นต้องติดตั้งเพิ่ม

ตอนเปิด Emulator พบปัญหา Windows Hypervisor Platform ยังไม่ได้เปิดใช้งาน ผมแก้ไขโดยเปิดใช้งานผ่าน Android Studio และรีสตาร์ตเครื่อง จากนั้นใช้คำสั่ง flutter devices ตรวจสอบว่า Flutter มองเห็น Emulator หรือไม่ นอกจากนี้ยังพบปัญหา Gradle และ NDK จึงตั้งค่า Gradle และติดตั้ง NDK เวอร์ชันที่โปรเจกต์ต้องการผ่าน SDK Manager จนสามารถรันแอปได้

## Q2: Hot Reload และ Hot Restart

จากการทดลองกด Like จำนวน 3 ครั้ง แล้วเปลี่ยนข้อความ AppBar เป็น Lab L1 done เมื่อกด r ข้อความ AppBar เปลี่ยนไป แต่จำนวน Likes ยังเป็น 3 เท่าเดิม เพราะ Hot Reload ยังคงเก็บค่า State เดิมไว้

เมื่อกด R จำนวน Likes กลับเป็น 0 เพราะ Hot Restart เป็นการเริ่มต้นแอปใหม่ ทำให้ค่า State กลับไปเป็นค่าเริ่มต้น

## Q3: โค้ดและ Git

การเพิ่มค่า _likes++ ต้องเรียกผ่าน setState() เพราะเป็นการบอกให้ Flutter เรียก build() อีกครั้ง เพื่อให้ตัวเลขที่แสดงบนหน้าจอเปลี่ยนตามค่าของตัวแปร

Commit ที่เลือก: Add like counter with setState

Commit นี้เปลี่ยน HomePage จาก StatelessWidget เป็น StatefulWidget และเพิ่มตัวแปร _likes ฟังก์ชัน _like() ข้อความแสดงจำนวน Likes และปุ่ม Like ที่สามารถกดเพิ่มจำนวนได้

## ตารางผลการทดสอบ

| ประเภท | การทดสอบ | ผลที่คาดหวัง | ผลจริง |
|---|---|---|---|
| Normal | เปิดแอป | แสดง Title ไอคอน ชื่อ และ Likes: 0 | แสดงข้อมูลครบและ Likes: 0 |
| Normal | กด Like หนึ่งครั้ง | Likes: 1 | Likes: 1 |
| Boundary | กด Like เร็ว ๆ 20 ครั้ง | Likes: 20 ไม่มี Error | Likes: 20 และแอปทำงานปกติ |
| Boundary | หมุนจอเป็นแนวนอน | อยู่กลางจอ ไม่ Overflow | แสดงผลกลางจอได้ปกติ ไม่พบ Overflow |
| Reload | กด Like 3 ครั้ง แล้วกด r และ R | หลัง r ได้ 3 หลัง R ได้ 0 | หลัง r ได้ 3 หลัง R ได้ 0 |
| Failure | ปิด Emulator แล้ว flutter run -d emulator-5554 | ไม่พบอุปกรณ์ | แสดงข้อความ No supported devices found |

## การใช้ AI

ใช้ ChatGPT ช่วยอธิบายขั้นตอนตามเอกสารอาจารย์ ช่วยตรวจสอบโค้ด แนะนำวิธีแก้ปัญหา Flutter, Gradle และ Emulator รวมถึงช่วยเรียบเรียงคำตอบจากผลการทดสอบที่ผมได้ลงมือทำจริง