# FastAPI กับ Nginx Load Balancing

โปรเจคนี้แสดงให้เห็นถึงการตั้งค่าหลายอินสแตนซ์ของแอปพลิเคชัน FastAPI ที่อยู่เบื้องหลัง Nginx Load Balancer โดยใช้ Docker

## สารบัญ

- [Docker](#Docker)
- [ความต้องการ](#ความต้องการ)
- [โครงสร้างโปรเจค](#โครงสร้างโปรเจค)
- [คำแนะนำในการตั้งค่า](#คำแนะนำในการตั้งค่า)
- [การติดตั้ง Nginx บน Windows 11](#การติดตั้ง-nginx-บน-windows-11)
- [การรันโปรเจค](#การรันโปรเจค)
- [การเข้าถึงแอปพลิเคชัน](#การเข้าถึงแอปพลิเคชัน)
- [หมายเหตุ](#หมายเหตุ)
  
## Docker
1.การตั้งค่า Restart Policy
ใน Docker มีการตั้งค่า Restart Policy ที่จะช่วยให้คอนเทนเนอร์สามารถรีสตาร์ทอัตโนมัติเมื่อเกิดปัญหา หรือตั้งให้คอนเทนเนอร์รันตลอดเวลาโดยไม่ต้องมาคอยเปิดปิดด้วยตนเอง:

always: ทำให้คอนเทนเนอร์รีสตาร์ทใหม่เสมอ ไม่ว่ามันจะหยุดทำงานเพราะสาเหตุใด
unless-stopped: คอนเทนเนอร์จะรันอัตโนมัติเว้นแต่จะมีการหยุดโดยผู้ใช้
on-failure: คอนเทนเนอร์จะรีสตาร์ทใหม่เมื่อเกิดการล้มเหลวเท่านั้น

คุณสามารถตั้งค่า Restart Policy ในไฟล์ docker-compose.yml ได้ตามตัวอย่างนี้:
```yml
services:
  fastapi_app1:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: fastapi_app1
    ports:
      - "8001:8000"
    restart: always  # ตั้งให้รีสตาร์ทเสมอ
```

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
   ```bash
FROM python:3.9-slim

WORKDIR /app

COPY ./app /app

RUN pip install fastapi uvicorn

EXPOSE 8000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```
## การติดตั้ง Nginx บน Windows 11
![FastAPI Nginx Docker Architecture](./images/system_architecture.png)

1.ดาวน์โหลด Nginx:
ไปที่ Nginx Official Website และดาวน์โหลดเวอร์ชันที่เหมาะสมกับ Windows

2.แตกไฟล์ Nginx:
แตกไฟล์ .zip ไปยัง directory ที่ต้องการ เช่น C:\nginx

3.รัน Nginx:
เปิด Command Prompt หรือ PowerShell และเปลี่ยน directory:
```bash
cd C:\nginx
start nginx
```
4. ตรวจสอบการทำงาน:
เปิดเว็บเบราว์เซอร์และไปที่ http://localhost

## การรันโปรเจค
เพื่อเริ่มบริการทั้งหมด ให้รันคำสั่งต่อไปนี้ในเทอร์มินัล:
```bash
docker-compose up -d
```
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
```bash
docker-compose up -d --build
```




