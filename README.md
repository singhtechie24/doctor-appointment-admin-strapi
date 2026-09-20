# 🏥 Glowing Smiles — Headless CMS Backend API (Strapi v4)

[![Strapi](https://img.shields.io/badge/Strapi-v4.23-purple?style=for-the-badge&logo=strapi)](https://strapi.io/)
[![Node.js](https://img.shields.io/badge/Node.js-20.x-green?style=for-the-badge&logo=node.js)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=for-the-badge&logo=supabase)](https://supabase.com/)
[![Cloudinary](https://img.shields.io/badge/Cloudinary-Asset_CDN-blue?style=for-the-badge&logo=cloudinary)](https://cloudinary.com/)
[![Render](https://img.shields.io/badge/Render-Cloud_Host-black?style=for-the-badge&logo=render)](https://render.com/)

The production headless Content Management System and REST API backend for the **Glowing Smiles Doctors & Clinic** appointment booking ecosystem. Built with **Strapi v4**, connected to a hosted **Supabase PostgreSQL** database via connection pooling, and integrated with **Cloudinary** for medical asset delivery.

---

## 🌐 Live Service & Links

* **Frontend Web Application:** [https://doctor-appointment-booking-web-nextjs-two.vercel.app](https://doctor-appointment-booking-web-nextjs-two.vercel.app)
* **Frontend Repository:** [Doctor-Appointment-Booking-Web-Nextjs](https://github.com/singhtechie24/Doctor-Appointment-Booking-Web-Nextjs)
* **Backend Deployment:** Deployed on Render Web Service (Node.js 20 & Supabase PostgreSQL Connection Pooler)

---

## 📊 Content Models & Schema Architecture

| Content Type | Key Attributes | Relationships |
| :--- | :--- | :--- |
| **`Doctor`** | `Name`, `Address`, `Year_of_Experience`, `About`, `StartTime`, `EndTime` | Many-to-Many with `Category`, Media relation with `Image` (Cloudinary) |
| **`Category`** | `Name` | Many-to-Many with `Doctor`, Media relation with `Icon` (Cloudinary) |
| **`Appointment`** | `UserName`, `Email`, `Date`, `Time`, `Note` | Many-to-One with `Doctor` |
| **`Slider`** | `Title`, `Link` | Media relation with `Image` (Cloudinary) |

---

## 🚀 Key REST API Endpoints

| Method | Endpoint | Description | Access |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/doctors?populate=*` | List all doctors with specialty categories & pictures | Public |
| `GET` | `/api/doctors/:id?populate=*` | Retrieve specific doctor profile & consultation slots | Public |
| `GET` | `/api/categories?populate=*` | List all medical categories with icons | Public |
| `GET` | `/api/appointments?filters[doctor][id][$eq]=:id&filters[Date][$eq]=:date` | Check booked slots to prevent collision | Public |
| `POST`| `/api/appointments` | Schedule a new patient appointment | Public |
| `GET` | `/api/appointments?filters[Email][$eq]=:email&populate=*` | Fetch user appointment history | Public |
| `DELETE`| `/api/appointments/:id` | Cancel an existing appointment | Public |

---

## 🛠️ Tech Stack & Infrastructure

* **Framework:** Strapi v4.23.1
* **Database Driver:** `pg` (PostgreSQL Client with native SSL)
* **Cloud Database:** Supabase PostgreSQL Session Pooler (`port 5432`)
* **Media Provider:** `@strapi/provider-upload-cloudinary`
* **Hosting Platform:** Render Web Service (Node 20 runtime)

---

## ⚙️ Local Development Setup

### 1. Clone Repository
```bash
git clone https://github.com/singhtechie24/doctor-appointment-admin-strapi.git
cd doctor-appointment-admin-strapi
```

### 2. Configure Environment (`.env`)
Create a `.env` file in the root directory:
```env
HOST=0.0.0.0
PORT=1337
APP_KEYS=your_app_keys
API_TOKEN_SALT=your_token_salt
ADMIN_JWT_SECRET=your_jwt_secret
TRANSFER_TOKEN_SALT=your_transfer_salt
JWT_SECRET=your_jwt_secret

DATABASE_CLIENT=postgres
DATABASE_HOST=aws-1-eu-west-1.pooler.supabase.com
DATABASE_PORT=5432
DATABASE_NAME=postgres
DATABASE_USERNAME=postgres.your_project_id
DATABASE_PASSWORD=your_db_password
DATABASE_SSL=true
DATABASE_SSL_REJECT_UNAUTHORIZED=false

CLOUDINARY_NAME=your_cloudinary_name
CLOUDINARY_KEY=your_cloudinary_key
CLOUDINARY_SECRET=your_cloudinary_secret
```

### 3. Install & Start
```bash
npm install
npm run develop
```
Strapi Admin panel will open at `http://localhost:1337/admin`.

---

## 📄 License
This project is open source and available under the [MIT License](LICENSE).
