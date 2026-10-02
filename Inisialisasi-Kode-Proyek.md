Inisialisasi Proyek — Smart Laundry Digital Twin

```text
smart-laundry-akt25/
|-- backend/ (server.js, package.json)
|-- frontend/ (index.html, style.css, app.js)
|-- simulator/ (machine_simulator.js)
|-- database/ (schema.sql)
|-- README.md
```

markdown Smart Laundry Digital Twin System

Pengembangan sistem Digital Twin untuk monitoring status mesin cuci dan manajemen antrean pelanggan secara real-time. Setup kode dasar untuk Sprint 1 — Product Release 1 (Pendekatan Scrum).

## Struktur Direktori

```text
smart-laundry-akt25/
|-- backend/          # Node.js & Express REST API (Logika server)
|-- frontend/         # Antarmuka web dashboard antrean (HTML/CSS/JS)
|-- simulator/        # Script simulator untuk data sensor IoT mesin cuci
|-- database/         # File skema database MySQL (smart_laundry_db)
|-- README.md         # File dokumentasi utama
```

## Panduan Menjalankan Sistem

```bash
# 1) Inisialisasi Server Backend
cd backend
npm install
node init_db.js
npm start

# 2) Menjalankan Simulator IoT
cd simulator
npm install
node machine_simulator.js

# 3) Menjalankan Frontend Web
cd frontend
npm install
npm start
```

Akses default (hanya untuk environment development): `admin` / `admin123`, `operator` / `operator123`.

## Daftar Endpoint API

| Method | Endpoint | Kegunaan |
| :--- | :--- | :--- |
| GET | `/api/health` | Memeriksa koneksi dan status server |
| POST | `/api/login` | Proses autentikasi user (username & password) |
| GET | `/api/machines` | Mengambil seluruh data status mesin cuci |
| POST | `/api/machines/status` | Menerima update data dari sensor mesin |
| GET | `/api/queue` | Melihat daftar antrean saat ini |
| POST | `/api/queue/add` | Mendaftarkan pelanggan baru ke antrean |

## Konfigurasi Database

Tabel utama yang digunakan: `users`, `machines`, `waiting_queue`, `transactions` — selengkapnya di `database/schema.sql`.

## Aturan Version Control (Git)

- Pembagian Branch: `main` (rilis stabil), `develop` (penggabungan fitur), dan `feature/<nama-fitur>` (pengerjaan fitur baru).
- Manajemen tugas dilakukan melalui GitHub Projects (Sprint & Product Backlog).
- Setiap kode yang masuk ke `develop` wajib melalui tahapan Pull Request dan direview oleh rekan tim.

## `.gitignore`

```text
node_modules/
*.log
.env
.DS_Store
```

## `database/schema.sql`

```sql
-- Skema Database Sistem Smart Laundry (MySQL)

CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    role ENUM('admin', 'operator') NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS machines (
    machine_id INT AUTO_INCREMENT PRIMARY KEY,
    machine_name VARCHAR(50) NOT NULL,
    status ENUM('Available', 'Running', 'Maintenance') DEFAULT 'Available',
    remaining_time_minutes INT DEFAULT 0,
    temperature_celsius DECIMAL(5,2) DEFAULT 0.00,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS waiting_queue (
    queue_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    phone_number VARCHAR(15) NOT NULL,
    assigned_machine_id INT,
    queue_status ENUM('Waiting', 'Processing', 'Finished') DEFAULT 'Waiting',
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
