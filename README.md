# ปุ๊กปิ๊ก — สัตว์เลี้ยงพกพา

เกมเลี้ยงสัตว์ดิจิทัลสไตล์เครื่องเกมพกพายุค 90 ทำงานในไฟล์ HTML ไฟล์เดียว
ไม่มี dependency ไม่ต้องต่อเน็ต เล่นออฟไลน์ได้ทั้งหมด

- ไข่สุ่มได้ 100 ใบ และวิวัฒนาการได้ 100 ร่าง
- **ช่องบันทึก 4 ช่อง** เลี้ยงพร้อมกันได้ 4 ตัว สลับไปมาได้จากเมนูตั้งค่า
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

## Deploy ขึ้น GitHub Pages

รีโปนี้มี workflow `.github/workflows/pages.yml` ที่ deploy ให้ทุกครั้งที่ push เข้า `main`
เหลือเปิดสวิตช์ครั้งเดียว (GitHub ไม่ยอมให้ workflow เปิด Pages ให้ตัวเองในครั้งแรก):

1. เข้า **Settings → Pages** ของรีโป
2. ที่ **Source** เลือก **GitHub Actions**
3. ไปที่แท็บ **Actions → Deploy to GitHub Pages → Run workflow** (หรือรอ push ครั้งถัดไป)

จะได้ URL `https://bmsjib5-ux.github.io/pukpik/`

> ถ้าเลือก Source เป็น *Deploy from a branch* (`main` / `/ (root)`) ก็ใช้งานได้เหมือนกัน
> แต่ให้ลบ `.github/workflows/pages.yml` ทิ้ง ไม่งั้น workflow จะขึ้นล้มเหลวทุกครั้งที่ push

## โครงสร้างไฟล์

| ไฟล์ | หน้าที่ |
| --- | --- |
| `index.html` | ตัวเกมทั้งหมด (HTML + CSS + JS + ไอคอน ในไฟล์เดียว) |
| `render.yaml` | Blueprint สำหรับ deploy เป็น static site บน Render |
| `.github/workflows/pages.yml` | Deploy ขึ้น GitHub Pages ทุกครั้งที่ push เข้า `main` |

## ช่องบันทึก

เปิด **ตั้งค่าและตัวเลือก → ช่องบันทึก** แล้วกดเลือกช่อง 1–4 ได้เลย

- ช่องว่างจะเริ่มฟักไข่ใบใหม่ให้ทันที ช่องที่มีข้อมูลจะเล่นต่อจากเดิม
- ตัวที่กำลังเล่นอยู่จะถูกบันทึกให้ก่อนสลับช่องเสมอ
- ปุ่ม **ลบ** ต้องกดสองครั้ง (ครั้งที่สองขึ้นว่า “ยืนยัน?”) กันลบพลาด
- ชื่อ อายุ และสถานะแยกกันของแต่ละช่อง ส่วนการตั้งค่า (ความยาก ความเร็ว เสียง) ใช้ร่วมกันทุกช่อง

เก็บใน `localStorage` คีย์ `pukpik.save.v2.<0-3>`, `pukpik.slot`, `pukpik.opts`
เซฟรุ่นเก่า (`pukpik.save.v1`) จะถูกย้ายมาไว้ช่องที่ 1 ให้อัตโนมัติในการเปิดครั้งแรก
