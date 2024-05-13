# Postman-101

[Link สำหรับใช้ในการขอ Request ใช้ใน Workshop นี้](https://reqres.in/)

GET -- รับข้อมูลมาแสดงผล
POST -- สร้างข้อมูลใหม่ - แนบข้อมูลที่จะเพิ่ม โดย กดที่ RAW และเลือกข้อมูลแบบ JSON หลังจากบันทึกข้อมูลแล้ว ส่ง Response กลับมาเป็น 201 
PUT -- Update ข้อมูลที่มีทุก field
PATCH -- Update ข้อมูลเฉพาะบาง field 
DELETE -- ลบ Response กลับมาเป็น 204

---
Params ส่วนของคิวรี่สตริง
Authorization การยืนยันตัวตน เนื่องจากบางเจ้าไม่ได้เปิดใช้งานฟรี
Headers อ้างอิงตาม api 
Body แนบข้อมูลอะไรมาบ้าง
Scripts ถูกทำงานก่อนจะส่ง Request ไป
Tests หลังจากส่ง Response กลับมา จะให้ทำงาน Scripts อะไร

---
Collection Runner รันไฟล์ครั้งเดียวโดยไม่ต้องเปิดไฟล์ รัน ตามลำดับ
โดยคลิกที่ Collection ที่ต้องการรัน กด RUN Collection เรียงตาม R

---
#### Variable
Local -- ทำงานเฉพาะไฟล์ Script
Data -- มาจาก ไฟล์ด้านนอก
Environment -- Environment ที่กำหนด การเข้าถึง Variable
Collection -- เฉพาะ Collection
Global -- ทุกส่วนเข้าถึงได้
Postman -- ค่าที่ Postman สร้างไว้ให้ได้ใช้งานได้เลย

##### การสร้าง ตัวแปร Global 
Environment quick look --> เลือก Global 
ตั้งชื่อ ตัวแปร และใส่ค่าเริ่มต้น ในครั้งแรก ค่า Current จะดึงมาจาก Initial โดยตรง
เมื่อมีการแก้ไข ต้องการเปลี่ยนค่อยมาใส่ค่าที่ Current value ใหม่

##### การสร้าง ตัวแปร Collection
คลิกที่ชื่อของ Collection
ไปที่ tab Variables และตั้งชื่อ ใส่ข้อมูล Initial value

##### การสร้าง ตัวแปร Environmen
คลิกที่ Environmen หรือ Environment quick look
เลือก Environment ใสตัวแปร
เมื่อมีการเรียกใช้ ให้เปลี่ยนตรง Environment

##### การสร้าง ตัวแปร Local Variable
เขียนตรง Pre-request เพื่อนำมาใช้งานเฉพาะ Script ตัวนี้โดยตรง
ให้ Body เรียกใช้งาน เนื่องจาก Body ทำงานหลังจาก Pre-request ทำงานเสร็จ
(Pre-request ทำงานก่อนส่ง requrest และ requrest ที่ส่งไปมี body อะไรบ้าง นำ body ไปทำงานที่ตัว API)
Pre-request --> pm.variables.set(" ") เช่น
pm.variables.set("user1", "jojo")
pm.variables.set("job1", "Tester")
วิธีเรียกใช้ใน Body
```JSON
{
    "name": "{{user1}}",
    "job": "{{job1}}"
}
```
##### การเรียกใช้ตัวแปร Dynamic Variable 
ค่าที่ Postman สร้างไว้ให้ได้ใช้งานได้เลย มีเครื่องหมาย $ อยู่ด้านหน้า

[Link สำหรับดูชื่อที่จะใช้ตัวแปร](https://learning.postman.com/docs/writing-scripts/script-references/variables-list/)
```JSON
{
    "name": "{{$randomFirstName}}",
    "job": "{{$randomJobTitle}}"
}
```

---
#### Data Driven
ใช้ไฟล์ข้างนอก นำมาใช้งาน โดยคลิกที่ Collection ที่ต้องการรัน กด RUN Collection ส่วนของ Data ให้เลือกไฟล์ที่จะนำเข้ามา
ตอนยิง Request ให้อ้างอิงจากไฟล์ที่ import เข้ามา
ติ๊กถูกที่ Persist responses for a session เพื่อ ให้ส่ง responses กลับมาด้วย
```JSON
{
    "email": "{{email}}",
    "password": "{{password}}"
}
```
{{email}}, {{password}} คือชื่อหัวคอลัมน์

---
#### Authorization
ตอนยิง Requrest ต้องเลือกรูปแบบการยืนยันตัวตน ผ่านการเลือก Type
เช่น API Key ป้อน Key Values หรือ Bearer Token
GitHub ใช้ Token เมื่อได้ Token มาแล้วให้ นำมาใส่ที่ Authorization

https://api.github.com/repos/OWNER/REPO
OWNER = ชื่อ Username Github
REPO = ชื่อ Repository
