# Sistem CRM CMLABS — Monitoring Leads & Sales

Sistem Customer Relationship Management (CRM) berbasis web untuk membantu proses monitoring leads dan sales pada PT CMLABS Indonesia Digital, dikembangkan menggunakan metode Scrum sebagai bagian dari Tugas Akhir.

---

## 1. Judul Tugas Akhir

**Pengembangan Sistem Customer Relationship Management (CRM) Berbasis Web untuk Monitoring Leads dan Sales pada CMLABS Menggunakan Metode Scrum**

---

## 2. Identitas Mahasiswa

| Keterangan | Informasi |
|------------|-----------|
| **Nama** | Reva Rahma Nadira |
| **NIM** | 221131004 |
| **Program Studi** | Sistem Informasi (S1) |
| **Fakultas** | Sains dan Teknologi |
| **Universitas** | Universitas Bhinneka Nusantara (UBHINUS) |

---

## 3. Dosen Pembimbing

| Keterangan | Informasi |
|------------|-----------|
| **Dosen Pembimbing** | Koko Wahyu Prasetyo |

---

## 4. Deskripsi Singkat Sistem

CMLABS merupakan perusahaan digital marketing yang sebelumnya mengelola data leads dan sales secara manual menggunakan spreadsheet serta berbagai media komunikasi terpisah, seperti Email, WhatsApp, dan Google Chat. Kondisi tersebut menyebabkan duplikasi data, kesulitan monitoring pipeline, serta keterlambatan penyusunan laporan.

Sebagai solusi, dikembangkan sistem **Customer Relationship Management (CRM)** berbasis web menggunakan metode **Scrum** yang dilaksanakan dalam **8 Sprint (88 hari kerja)**. Sistem mengintegrasikan seluruh proses monitoring leads dan sales ke dalam satu platform yang terdiri atas delapan modul utama berikut.

1. **Authentication & Role-Based Access Control (RBAC)**  
   Login dan pengelolaan hak akses berdasarkan empat role pengguna:
   - Admin
   - Executive
   - Sales Manager
   - Account Executive

2. **Leads Management**  
   Kanban Board dengan enam tahapan pipeline:
   - Approach
   - Cold Lead
   - Deck Request
   - Meeting
   - Deal
   - Recycle

   Mendukung fitur **drag-and-drop** untuk memindahkan leads antar tahap.

3. **Analytics Dashboard**  
   Menampilkan KPI dan visualisasi performa penjualan secara real-time.

4. **Team Management**  
   Pengelolaan data anggota tim sales.

5. **Profile Management**  
   Pengelolaan profil akun masing-masing pengguna.

6. **Lead Activity Timeline**  
   Riwayat aktivitas setiap leads, meliputi:
   - Catatan
   - Pengiriman Email
   - Agenda Telepon
   - Agenda Meeting
   - Tugas

7. **Sales Forecasting Dashboard**  
   Proyeksi pendapatan berdasarkan weighted probability pada setiap tahapan pipeline.

8. **Document Management**  
   Pembuatan dokumen bisnis secara otomatis dalam format `.docx`, meliputi:
   - Invoice
   - SPK
   - MoU

Sistem telah melalui proses **Black Box Testing** bersama Product Owner dengan seluruh skenario dinyatakan **Valid**, serta **User Acceptance Testing (UAT)** yang melibatkan **10 responden** dari empat role pengguna di CMLABS.

---

## 5. Teknologi yang Digunakan

| Kategori | Teknologi |
|-----------|-----------|
| **Framework** | Next.js 16 (App Router), React 19 |
| **Bahasa Pemrograman** | TypeScript |
| **Styling** | Tailwind CSS |
| **Authentication** | NextAuth.js v5 (Beta) |
| **ORM** | Prisma ORM v5.22 |
| **Database** | PostgreSQL (Neon Serverless / Docker Local) |
| **Drag & Drop** | @hello-pangea/dnd |
| **Chart & Visualisasi** | Recharts |
| **Document Generator** | docx, jsPDF, jsPDF-AutoTable |
| **Validation** | Zod |
| **Form Handling** | React Hook Form |
| **Data Fetching** | TanStack React Query |
| **Password Hashing** | bcryptjs |
| **Email Service** | Resend |
| **Testing** | Jest |
| **Deployment** | Docker, Vercel |

---

# 6. Cara Menjalankan Sistem

## 6.1 Menjalankan Menggunakan Docker (Direkomendasikan)

### Prasyarat

- Docker Desktop (Windows/macOS)
- atau Docker Engine + Docker Compose Plugin (Linux/Ubuntu)

### Clone Repository

```bash
git clone https://github.com/repssrahmaa/ta-sisteminformasi-221131004-crm-cmlabs.git
cd ta-sisteminformasi-221131004-crm-cmlabs
```

### Jalankan

```bash
docker compose up --build
```

Docker akan menjalankan proses berikut secara otomatis:

1. Menjalankan container PostgreSQL.
2. Menunggu database siap digunakan.
3. Menjalankan migrasi database.
4. Menjalankan proses seed data.
5. Menjalankan aplikasi CRM.

Setelah muncul log:

```text
✓ Ready
```

buka browser:

```text
http://localhost:3000
```

### Menghentikan Docker

```bash
docker compose down
```

Menghapus seluruh data database:

```bash
docker compose down -v
```

---

## 6.2 Menjalankan Tanpa Docker

### Prasyarat

- Node.js 20 LTS atau lebih baru
- npm
- PostgreSQL Database (misalnya Neon)

### Clone Repository

```bash
git clone https://github.com/repssrahmaa/ta-sisteminformasi-221131004-crm-cmlabs.git
cd ta-sisteminformasi-221131004-crm-cmlabs
```

### Install Dependency

```bash
npm install
```

### Buat File `.env`

```env
DATABASE_URL="postgresql://user:password@host:port/database"

NEXTAUTH_SECRET="isi-dengan-secret"

NEXTAUTH_URL="http://localhost:3000"

RESEND_API_KEY="re_xxxxxxxxxxxxxxxxx"
```

Generate `NEXTAUTH_SECRET`:

```bash
openssl rand -base64 32
```

### Jalankan Migrasi Database

```bash
npx prisma migrate deploy
```

### Jalankan Seed Data

```bash
npx prisma db seed
```

### Jalankan Aplikasi

```bash
npm run dev
```

Akses:

```text
http://localhost:3000
```

---

## 6.3 Akun Demo

| Role | Email | Password |
|------|-------|----------|
| **Admin** | `ADMIN@cmlabs.co` | `Demo123!` |
| **Executive** | `executive@cmlabs.co` | `Demo123!` |
| **Sales Manager** | `sales_mgr@cmlabs.co` | `Demo123!` |
| **Account Executive** | `ae@cmlabs.co` | `Demo123!` |

> **Catatan:** Email bersifat **case-sensitive**, gunakan sesuai penulisan pada tabel.

---

## 6.4 Menjalankan Unit Test

```bash
npm test
```

---

# 7. Struktur Project

```text
ta-sisteminformasi-221131004-crm-cmlabs/
│
├── app/
│   ├── (dashboard)/
│   │   ├── dashboard/          # Analytics Dashboard
│   │   ├── forecasting/        # Sales Forecasting Dashboard
│   │   ├── leads/              # Leads Management
│   │   ├── profile/            # Profile Management
│   │   ├── reports/            # Document Management
│   │   └── team/               # Team Management
│   │
│   ├── api/                    # Backend Route Handler
│   ├── login/
│   └── unauthorized/
│
├── components/                 # Reusable UI Components
├── hooks/                      # Custom React Hooks
├── lib/                        # Business Logic & Services
│
├── prisma/
│   ├── schema.prisma
│   ├── migrations/
│   └── seed.ts
│
├── public/
├── types/
│
├── proxy.ts                    # Route Guard (Next.js 16)
├── docker-compose.yml
├── Dockerfile
└── package.json
```

---

# 8. Catatan Khusus

## Batasan Penelitian

- Sistem dikembangkan sebagai implementasi penelitian Tugas Akhir.
- Pengujian dilakukan secara internal bersama Product Owner dan perwakilan pengguna CMLABS.
- Pengujian meliputi:
  - Black Box Testing
  - User Acceptance Testing (UAT)
- Sistem hanya mendukung empat role pengguna:
  - Admin
  - Executive
  - Sales Manager
  - Account Executive
- Modul **Document Management** menghasilkan dokumen bisnis dalam format `.docx`, meliputi Invoice, SPK, dan MoU.

---

## Demo Data

Seluruh akun demo beserta data awal akan dibuat secara otomatis ketika menjalankan:

```bash
docker compose up
```

atau

```bash
npx prisma db seed
```

---

## Repository

```text
https://github.com/repssrahmaa/ta-sisteminformasi-221131004-crm-cmlabs
```

---

## Lisensi

Repositori ini dibuat untuk keperluan akademik sebagai Tugas Akhir Program Studi Sistem Informasi Universitas Bhinneka Nusantara. Seluruh kode sumber dapat digunakan sebagai referensi pembelajaran, namun tidak diperkenankan untuk diklaim sebagai karya sendiri tanpa izin penulis.