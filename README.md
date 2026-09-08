# ปุ๊กปิ๊ก — สัตว์เลี้ยงพกพา

เกมเลี้ยงสัตว์ดิจิทัลสไตล์เครื่องเกมพกพายุค 90 ทำงานในไฟล์ HTML ไฟล์เดียว
ไม่มี dependency ไม่ต้องต่อเน็ต เล่นออฟไลน์ได้ทั้งหมด

- ไข่สุ่มได้ 100 ใบ และวิวัฒนาการได้ 100 ร่าง
- บันทึกสถานะอัตโนมัติลง `localStorage` และเดินเวลาต่อให้แม้ปิดหน้าไว้
- ปุ่ม `A` เลื่อน · `B` เลือก · `C` ย้อนกลับ (คีย์บอร์ดกด A B C หรือเลข 1–6)
- บนมือถือกด “แชร์ → เพิ่มไปยังหน้าจอโฮม” เพื่อเปิดเล่นเหมือนแอป

## เล่นในเครื่องตัวเอง

เปิด `index.html` ด้วยเบราว์เซอร์ได้เลย หรือรันเซิร์ฟเวอร์เล็ก ๆ:

```bash
python3 -m http.server 8000
# แล้วเปิด http://localhost:8000
```

## Deploy ขึ้น Render

รีโปนี้มี `render.yaml` (Blueprint) พร้อมใช้งานเป็น **Static Site** อยู่แล้ว

1. เข้า https://dashboard.render.com → **New +** → **Blueprint**
2. เลือกรีโป `bmsjib5-ux/pukpik` แล้วกด **Apply**
3. Render จะสร้าง static site ชื่อ `pukpik` และให้ URL รูปแบบ
   `https://pukpik.onrender.com` (ถ้าชื่อซ้ำจะมีตัวห้อยต่อท้าย)

ตั้งค่าที่ใช้: `staticPublishPath: .` และ rewrite ทุก path ไปที่ `/index.html`
ทุกครั้งที่ push เข้า branch ที่ผูกไว้ Render จะ deploy ให้อัตโนมัติ

## โครงสร้างไฟล์

| ไฟล์ | หน้าที่ |
| --- | --- |
| `index.html` | ตัวเกมทั้งหมด (HTML + CSS + JS ในไฟล์เดียว) |
| `render.yaml` | Blueprint สำหรับ deploy เป็น static site บน Render |
