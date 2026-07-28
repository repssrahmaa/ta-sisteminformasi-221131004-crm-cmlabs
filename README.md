# Sistem CRM CMLABS — Monitoring Leads & Sales

Sistem Customer Relationship Management (CRM) berbasis web untuk membantu proses monitoring leads dan sales pada PT CMLABS Indonesia Digital, dikembangkan menggunakan metode Scrum sebagai bagian dari Tugas Akhir.

## 1. Judul Tugas Akhir

**Pengembangan Sistem Customer Relationship Management (CRM) Berbasis Web untuk Monitoring Leads dan Sales pada CMLABS Menggunakan Metode Scrum**

## 2. Identitas Mahasiswa

| | |
|---|---|
| Nama | Reva Rahma Nadira |
| NIM | 221131004 |
| Program Studi | Sistem Informasi (S1) |
| Fakultas | Sains dan Teknologi |
| Universitas | Universitas Bhinneka Nusantara (UBHINUS) |

## 3. Dosen Pembimbing

| | |
|---|---|
| Dosen Pembimbing | Koko Wahyu Prasetyo |

## 4. Deskripsi Singkat Sistem

CMLABS adalah perusahaan digital marketing (SEO, content marketing, dan produk digital lain) yang sebelumnya mengelola leads dan sales secara manual melalui spreadsheet serta komunikasi yang tersebar di berbagai media (email, WhatsApp, Google Chat). Sistem ini dikembangkan menggunakan metode Scrum dalam delapan sprint selama 88 hari kerja untuk mengintegrasikan seluruh proses tersebut ke dalam satu platform, mencakup delapan modul utama:

1. **Authentication & Role-Based Access Control (RBAC)** — login dan pembatasan hak akses untuk 4 role: Admin, Executive, Sales Manager, Account Executive
2. **Leads Management** — Kanban Board dengan 6 tahapan pipeline (Approach, Cold Lead, Deck Request, Meeting, Deal, Recycle), mendukung drag-and-drop
3. **Analytics Dashboard** — ringkasan KPI dan visualisasi performa penjualan
4. **Team Management** — pengelolaan data anggota Tim Sales
5. **Profile Management** — pengelolaan profil akun secara mandiri
6. **Lead Activity Timeline** — pencatatan riwayat aktivitas per leads (Catatan, Pengiriman Email, Agenda Telepon, Agenda Meeting, Tugas)
7. **Sales Forecasting Dashboard** — proyeksi pendapatan berbasis weighted probability per tahapan pipeline
8. **Document Management** — pembuatan dokumen bisnis (Invoice, SPK, MoU) dalam format `.docx`, digenerate on-demand

Sistem telah diuji melalui Black Box Testing (bersama Product Owner, seluruh skenario Valid) dan User Acceptance Testing melibatkan 10 responden dari empat role pengguna di CMLABS.

## 5. Teknologi yang Digunakan

| Kategori | Teknologi |
|---|---|
| Framework | Next.js 16 (App Router), React 19 |
| Bahasa | TypeScript |
| Styling | Tailwind CSS |
| Autentikasi | NextAuth.js v5 (beta) |
| ORM & Database | Prisma ORM v5.22.0, PostgreSQL (Neon serverless / Docker lokal) |
| Drag & Drop | @hello-pangea/dnd |
| Visualisasi Data | Recharts |
| Generate Dokumen | docx (`.docx`), jspdf + jspdf-autotable |
| Validasi & Form | Zod, React Hook Form |
| Data Fetching | TanStack React Query |
| Keamanan Password | bcryptjs |
| Pengiriman Email | Resend |
| Testing | Jest |
| Deployment | Vercel, Docker |

## 6. Cara Menjalankan Sistem

### 6.1 Menjalankan via Docker (disarankan)

**Prasyarat:** Docker Desktop (Windows/macOS) atau Docker Engine + Docker Compose plugin (Linux/Ubuntu).

**Langkah:**
```bash
git clone https://github.com/repssrahmaa/ta-sisteminformasi-221131004-crm-cmlabs.git
cd ta-sisteminformasi-221131004-crm-cmlabs
docker compose up --build
```

Perintah ini menjalankan tiga tahap secara berurutan dan otomatis: (1) container `postgres` menyala dan ditunggu hingga siap, (2) container `migrate` menjalankan migrasi skema database dan mengisi data awal, (3) container `app` baru menyala setelah migrasi selesai. Tunggu hingga log menampilkan `✓ Ready`, lalu buka `http://localhost:3000`.

Untuk menghentikan:
```bash
docker compose down          # hentikan, data database tetap ada
docker compose down -v       # hentikan sekaligus hapus data database
```

### 6.2 Menjalankan Tanpa Docker (Node.js lokal)

**Prasyarat:** Node.js 20 LTS+, npm, akun database PostgreSQL (mis. [Neon](https://neon.tech)).

```bash
git clone https://github.com/repssrahmaa/ta-sisteminformasi-221131004-crm-cmlabs.git
cd ta-sisteminformasi-221131004-crm-cmlabs
npm install
```

Buat file `.env` di root project:
```env
DATABASE_URL="postgresql://user:password@host:port/database"
NEXTAUTH_SECRET="isi-dengan-string-acak-yang-aman"
NEXTAUTH_URL="http://localhost:3000"
RESEND_API_KEY="re_xxxxxxxxxxxxxxxxxxxx"
```
(`NEXTAUTH_SECRET` bisa dibuat dengan `openssl rand -base64 32`)

```bash
npx prisma migrate deploy
npx prisma db seed
npm run dev
```

Buka `http://localhost:3000`.

### 6.3 Akun Demo

| Role | Email | Password |
|---|---|---|
| Admin | `ADMIN@cmlabs.co` | `Demo123!` |
| Executive | `executive@cmlabs.co` | `Demo123!` |
| Sales Manager | `sales_mgr@cmlabs.co` | `Demo123!` |
| Account Executive | `ae@cmlabs.co` | `Demo123!` |

> Salin persis seperti tertulis — email bersifat *case-sensitive*.

### 6.4 Menjalankan Test
```bash
npm test
```

## 7. Struktur Project

```text
ta-sisteminformasi-221131004-crm-cmlabs/
├── app/
│   ├── (dashboard)/          # Route group halaman utama (butuh login)
│   │   ├── dashboard/        # Analytics Dashboard
│   │   ├── forecasting/      # Sales Forecasting Dashboard
│   │   ├── leads/            # Leads Management (Kanban Board)
│   │   ├── profile/          # Profile Management
│   │   ├── reports/          # Document Management
│   │   └── team/             # Team Management
│   ├── api/                  # Route handler backend
│   ├── login/                # Halaman Login
│   └── unauthorized/         # Halaman akses ditolak
├── components/               # Komponen UI (Kanban board, Sidebar, form, dll.)
├── hooks/                    # Custom React hooks (useRoleGuard, useTheme, dll.)
├── lib/                      # Konfigurasi auth, permission matrix, service (docx generator, dll.)
├── prisma/
│   ├── schema.prisma         # Skema database
│   ├── migrations/           # Riwayat migrasi database
│   └── seed.ts               # Skrip pengisian data awal
├── types/                    # TypeScript type definitions
├── public/                   # Aset statis
├── proxy.ts                  # Route guard berbasis role (konvensi Next.js 16, pengganti middleware.ts)
├── docker-compose.yml        # Orkestrasi Docker (postgres → migrate → app)
├── Dockerfile
└── package.json
```

## 8. Catatan Khusus

**Batasan:**
- Sistem ini merupakan hasil penelitian Tugas Akhir, dikembangkan dan diuji secara internal bersama Product Owner dan perwakilan pengguna CMLABS melalui Black Box Testing dan User Acceptance Testing.
- Cakupan role dibatasi pada empat role: Admin, Executive, Sales Manager, dan Account Executive.
- Fitur Document Management berfokus pada pembuatan dokumen bisnis format `.docx` (Invoice, SPK, MoU).

**Demo:** lihat tabel Akun Demo pada bagian 6.3. Seluruh akun dan data contoh dibuat otomatis saat `docker compose up` (atau `npx prisma db seed` pada instalasi manual).