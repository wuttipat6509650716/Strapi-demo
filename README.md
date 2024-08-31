# Strapi
Strapi เป็นเครื่องมือที่ช่วยในการสร้าง API ด้วย javascript ผ่านการจัดการด้วยหน้า dashboard และยังเป็นโปรแกรม headless CMS ที่เป็นโอเพนซอร์ส เป็นการแยกการทำงานของ frontend, backend และ ฐานข้อมูล ออกจากกัน ทำให้สามารถควบคุมการทำงานในแต่ละส่วนได้

Use case : เว็บไซต์ แอปพลิเคชัน ฐานข้อมูล เชื่อมโยงกันระหว่าง frontend และ backend ได้ ตัวอย่าง เว็บแอปพลิเคชัน

องค์ประกอบ : เบื้องต้นส่วนประกอบหลักจะ ได้แก่ API, Database, Javascript, Plugins, Authentication & Authorization, Content-Type Builder, Content Management, Dynamic Zones, Webhook, File Storage and Media Library และ Headless CMS เป็นต้น

.gitignore เป็นไฟล์ที่ใช้บอก git ว่าไฟล์ใดบ้างที่ไม่ต้องนำขึ้น repository เนื่องจากอาจติดปัญหาด้านความปลอดภัย และ ขนาดของไฟล์ในการ clone รอบต่อไป เนื้อหาในไฟล์จะบอกถึงนามสกุลไฟล์ที่ไม่ต้องนำขึ้น repository

## ขั้นตอนการติดตั้ง Strapi
ขั้นตอนแรกจะต้องตรวจสอบ node.js ในเครื่องว่าติดตั้งหรือยัง
```bash
node --version
```
ขั้นตอนต่อไปเมื่อมี node.js ในเครื่องแล้วสามารถติดตั้ง Strapi ได้
```bash
npx create-strapi-app@latest my-project
```
ขั้นตอนต่อไปสามารถรันโปรเจค Strapi ได้โดย
```bash
npm run develop  
```

## ขั้นตอนการนำโค้ดขึ้น github ผ่าน ssh (Window)
ขั้นตอนแรกจะต้องตรวจสอบ git ในเครื่องว่าติดตั้งหรือยัง
```bash
git --version
```
ขั้นตอนต่อมาเปิด git bash มาสร้าง public key และ private key ผ่านคำสั่ง
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
แล้วนำ public key ไปเพิ่มใน setting -> SSH

จากนั้นให้โคลน repository ลงมาในเครื่องเราด้วยคำสั่ง
```bash
git clone git@github.com:~
```
ขั้นตอนต่อมานำไฟล์คงไปยังไฟล์ที่โคลนเพื่อนำมาอัพโหลดขึ้น git repositoty จากนั้นอัพโหลดโค้ดขึ้นผ่านคำสั่ง
```bash
git add .
git commit -m "strapi-demo"
git push origin main
```

## ขั้นตอนนำโค้ดลงมาใน EC2 และลองรันโปรเจค
instance ใน EC2 จะใช้ขนาด t2.medium

ขั้นตอนแรกจะต้องตรวจสอบ git ในเครื่องว่าติดตั้งหรือยัง
```bash
git --version
```
ขั้นตอนต่อมาเปิด git bash มาสร้าง public key และ private key ผ่านคำสั่ง
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
แล้วนำ public key ไปเพิ่มใน setting -> SSH

จากนั้นให้โคลน repository ลงมาในเครื่องเราด้วยคำสั่ง
```bash
git clone git@github.com:~
```

### ขั้นตอนการรันโปรเจค

ในการโคลน repository เข้ามาแล้วเรายังไม่สามารถรัน Strapi ได้เนื่องจากตอนเรานำโค้ดขึ้น repository มีบางไฟล์ใดบ้างที่ไม่ต้องนำขึ้นที่อยู่ใน .gitignore เราจึงจำเป็นต้องนำ npm เข้ามาโดยใช้คำสั่ง
```bash
npm install
```
ต่อมาเป็นการสร้างไฟล์ .env เนื้อหาในไฟล์เบื้องต้น
```bash
HOST=0.0.0.0
PORT=1337
APP_KEYS="toBeModified1,toBeModified2"
API_TOKEN_SALT=tobemodified
ADMIN_JWT_SECRET=tobemodified
TRANSFER_TOKEN_SALT=tobemodified
JWT_SECRET=tobemodified
```

หลังจากขั้นตอนนี้สามารถลองรันโปรเจค Strapi ได้เลยโดยใช้คำสั่ง
```bash
npm run develop
```

## ขั้นตอนการทำให้ EC2 สามารถเข้าถึงผ่านอินเตอร์เน็ตได้

ต้องเข้าไปใน instance EC2 เซต Inbound rules ให้กำหนดค่า Custom TCP Port range ให้ตรงกับค่า Port ใน .env ของ Strapi จากนั้น Source ให้ตั้งค่า Anywhere-IPv4 

จากนั้นรัน Strapi ใน EC2 ใหม่และลองเข้าผ่าน Public IPv4 : Port

## แหล่งอ้างอิง

 1. morphosis. Strapi คืออะไร และทำไมถึงได้รับความนิยมในโลกของ Headless CMS [อินเตอร์เน็ต]. เข้าถึงได้จาก: https://morphos.is/th/blog/what-is-strapi-and-how-it-will-dominate-the-world-of-headless-cms [เข้าถึงเมื่อ 31 สิงหาคม 2567]
 2. Nitipat Lowichakornthikun. ลองเล่น Strapi — Headless CMS กัน  [อินเตอร์เน็ต]. เข้าถึงได้จาก https://medium.com/i-gear-geek/ลองเล่น-strapi-headless-cms-กัน-f26ff53ac069 [เข้าถึงเมื่อ 31 สิงหาคม 2567]
 3. Max Veerapat Kumchom. ออกแบบสร้าง APIs แบบโคตรเร็ว, จัดการเนื้อหาแบบโคตรง่าย ด้วย Strapi Headless CMS [อินเตอร์เน็ต]. เข้าถึงได้จาก https://medium.com/@themaxaboy/ออกแบบสร้าง-apis-แบบโคตรเร็ว-จัดการเนื้อหาแบบโคตรง่าย-ด้วย-strapi-headless-cms-da907437040 [เข้าถึงเมื่อ 31 สิงหาคม 2567]
 4. strapi. Installing from CLI [อินเตอร์เน็ต]. เข้าถึงได้จาก https://docs.strapi.io/dev-docs/installation/cli [เข้าถึงเมื่อ 31 สิงหาคม 2567]
 5. GitHub Docs. Generating a new SSH key and adding it to the ssh-agent [อินเตอร์เน็ต]. เข้าถึงได้จาก https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent [เข้าถึงเมื่อ 31 สิงหาคม 2567]
 6. Wasith T. (Bai-Phai). .gitignore ความสามารถของ git และการใช้งานอย่างง่าย [อินเตอร์เน็ต]. เข้าถึงได้จาก https://medium.com/odds-team/gitignore-ความสามารถของ-git-version-control-a77d1677a9d3 [เข้าถึงเมื่อ 31 สิงหาคม 2567]
