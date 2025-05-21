# Frontend JwtAuthDemo

Frontend สำหรับระบบ **JWT Authentication** ที่เชื่อมต่อกับ Backend [JwtAuthDemo API]([https://github.com/AssaniIndraprasitdhi/backend-jwt-auth.git]) โดยใช้ React + Vite พร้อมจัดการการเข้าสู่ระบบและเก็บ Token ด้วย `localStorage` หรือ `httpOnly Cookie`

## 🚀 Features

- หน้า **Login** และ **Register**
- เชื่อมต่อ API JWT Authentication
- บันทึก JWT Token และตรวจสอบสิทธิ์ผู้ใช้
- Route ป้องกันสำหรับผู้ที่ login แล้วเท่านั้น
- รองรับการเพิ่ม Role, Profile, Refresh Token ในอนาคต

## 🛠 Tech Stack

- **React 18**
- **Vite**
- **Tailwind CSS** (หรือ DaisyUI/ShadCN ตามที่คุณเลือก)
- **React Hook Form + Zod** (สำหรับ Form Validation)
- **Axios** (สำหรับเรียก API)
- **React Router DOM** (สำหรับจัดการ Routing)
- **Context API** (สำหรับเก็บ User State)

## 📦 Getting Started

### 1. Clone Repository

```bash
git clone https://github.com/AssaniIndraprasitdhi/frontend-jwt-auth.git
cd frontend-jwt-auth
