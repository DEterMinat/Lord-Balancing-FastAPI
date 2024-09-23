# FastAPI กับ Nginx Load Balancing

โปรเจคนี้แสดงให้เห็นถึงการตั้งค่าหลายอินสแตนซ์ของแอปพลิเคชัน FastAPI ที่อยู่เบื้องหลัง Nginx Load Balancer โดยใช้ Docker

## สารบัญ

- [ความต้องการ](#ความต้องการ)
- [โครงสร้างโปรเจค](#โครงสร้างโปรเจค)
- [คำแนะนำในการตั้งค่า](#คำแนะนำในการตั้งค่า)
- [การติดตั้ง Nginx บน Windows 11](#การติดตั้ง-nginx-บน-windows-11)
- [การรันโปรเจค](#การรันโปรเจค)
- [การเข้าถึงแอปพลิเคชัน](#การเข้าถึงแอปพลิเคชัน)
- [การหยุดบริการ](#การหยุดบริการ)
- [หมายเหตุ](#หมายเหตุ)

## ความต้องการ

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

## โครงสร้างโปรเจค

## คำแนะนำในการตั้งค่า

1. **โคลน Repository** (ถ้ามี):
   ```bash
   git clone <repository-url>
   cd my_fastapi_docker_project

2. สร้างแอปพลิเคชัน FastAPI:
วางโค้ด FastAPI ของคุณใน app/app.py

3. กำหนดค่า Nginx:
ปรับเปลี่ยนไฟล์ nginx/nginx.conf ตามที่ต้องการ

4.สร้าง Dockerfile:
ตรวจสอบว่า Dockerfile ของคุณตั้งค่าไว้ดังนี้:
FROM python:3.9-slim

WORKDIR /app

COPY ./app /app

RUN pip install fastapi uvicorn

EXPOSE 8000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]

## การติดตั้ง Nginx บน Windows 11
1.ดาวน์โหลด Nginx:
ไปที่ Nginx Official Website และดาวน์โหลดเวอร์ชันที่เหมาะสมกับ Windows

2.แตกไฟล์ Nginx:
แตกไฟล์ .zip ไปยัง directory ที่ต้องการ เช่น C:\nginx

3.รัน Nginx:
เปิด Command Prompt หรือ PowerShell และเปลี่ยน directory:
bash:
cd C:\nginx
start nginx

4. ตรวจสอบการทำงาน:
เปิดเว็บเบราว์เซอร์และไปที่ http://localhost

## การรันโปรเจค
เพื่อเริ่มบริการทั้งหมด ให้รันคำสั่งต่อไปนี้ในเทอร์มินัล:

docker-compose up -d

คำสั่งนี้จะสร้าง Docker images และเริ่มคอนเทนเนอร์ที่กำหนดใน docker-compose.yml

การเข้าถึงแอปพลิเคชัน
คุณสามารถเข้าถึงแอปพลิเคชัน FastAPI และ Nginx Load Balancer ที่ URL ดังนี้:

FastAPI App 1: http://localhost:8001
FastAPI App 2: http://localhost:8002
FastAPI App 3: http://localhost:8003
Nginx Load Balancer: http://localhost


## หมายเหตุ
ตรวจสอบให้แน่ใจว่า Docker กำลังทำงานก่อนที่จะรันคำสั่ง
หากคุณทำการเปลี่ยนแปลงโค้ดหรือการกำหนดค่า คุณอาจต้องสร้างคอนเทนเนอร์ใหม่โดยใช้:

docker-compose up -d --build


### การใช้งาน

- คัดลอกข้อความด้านบนและวางลงในไฟล์ **README.md** ใน directory ของโปรเจคของคุณ
- ปรับเปลี่ยนข้อมูลต่าง ๆ ตามความต้องการ เช่น URL ของ repository หรือคำอธิบายเพิ่มเติมเกี่ยวกับโปรเจค

หากมีคำถามเพิ่มเติมหรือต้องการให้ช่วยเหลืออะไร แจ้งได้เลย!


