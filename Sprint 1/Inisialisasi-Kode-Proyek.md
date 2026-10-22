# Inisialisasi Proyek — Smart Laundry Digital Twin

```text
smart-laundry-akt25/
|-- backend/ (server.js, init_db.js, package.json)
|-- frontend/ (index.html, style.css, app.js)
|-- simulator/ (machine_simulator.js)
|-- database/ (schema.sql)
|-- README.md
```

# Smart Laundry Digital Twin System

Pengembangan sistem Digital Twin untuk monitoring status mesin cuci dan pengelolaan pesanan laundry secara real-time oleh tiga aktor: **Pelanggan**, **Petugas**, dan **Owner**. Mesin laundry bukan pengguna sistem; statusnya dikirim ke sistem oleh `simulator/` (pada produksi: sensor mesin). Setup kode dasar untuk Sprint 1 — Product Release 1 (Pendekatan Scrum).

## Struktur Direktori

```text
smart-laundry-akt25/
|-- backend/          # Node.js & Express REST API (Logika server, login per peran)
|-- frontend/         # Antarmuka web dashboard (HTML/CSS/JS)
|-- simulator/        # Script simulator yang berperan sebagai mesin laundry (data sensor IoT)
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

## Akun Dummy (khusus environment development)

`node init_db.js` membuat satu akun dummy untuk setiap peran. Akun ini hanya untuk pengembangan dan pengujian, tidak boleh dipakai di lingkungan sebenarnya.

| Peran | Username | Password |
| :--- | :--- | :--- |
| Pelanggan | `pelanggan` | `pelanggan123` |
| Petugas | `petugas` | `petugas123` |
| Owner | `owner` | `owner123` |

## Daftar Endpoint API

| Method | Endpoint | Peran | Kegunaan |
| :--- | :--- | :--- | :--- |
| GET | `/api/health` | Semua | Memeriksa koneksi dan status server |
| POST | `/api/login` | Semua | Autentikasi user (username & password), mengembalikan peran |
| POST | `/api/logout` | Semua | Mengakhiri sesi login |
| GET | `/api/machines` | Semua | Mengambil seluruh data status mesin cuci |
| POST | `/api/machines` | Owner | Menambah data mesin (kapasitas, tipe) |
| POST | `/api/machines/status` | Simulator / Petugas | Menerima update status dari sensor mesin atau input petugas |
| GET | `/api/queue` | Semua | Melihat daftar antrean ruang tunggu saat ini |
| POST | `/api/queue/add` | Petugas | Memasukkan pesanan ke antrean |
| GET | `/api/customers` | Petugas | Melihat data pelanggan |
| POST | `/api/customers` | Petugas | Menambah data pelanggan |
| GET | `/api/orders` | Semua | Melihat pesanan (pelanggan hanya miliknya sendiri) |
| POST | `/api/orders` | Pelanggan, Petugas | Membuat pesanan baru |
| PATCH | `/api/orders/:id/status` | Petugas | Memperbarui status pesanan |
| POST | `/api/payments` | Pelanggan | Mencatat pembayaran digital untuk pesanan |
| GET | `/api/transactions` | Petugas, Owner | Melihat riwayat dan detail transaksi |

## Konfigurasi Database

Tabel utama yang digunakan: `users`, `customers`, `machines`, `orders`, `payments`, dan `waiting_queue` — selengkapnya di `database/schema.sql`. Tabel `transactions` pada rancangan awal digantikan oleh `orders` (data pesanan) dan `payments` (data pembayaran).

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
    role ENUM('pelanggan', 'petugas', 'owner') NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NULL,
    customer_name VARCHAR(100) NOT NULL,
    phone_number VARCHAR(15) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE IF NOT EXISTS machines (
    machine_id INT AUTO_INCREMENT PRIMARY KEY,
    machine_name VARCHAR(50) NOT NULL,
    machine_type ENUM('washer', 'dryer') NOT NULL DEFAULT 'washer',
    capacity_kg DECIMAL(5,2) NOT NULL DEFAULT 0.00,
    status ENUM('Available', 'Running', 'Maintenance') DEFAULT 'Available',
    remaining_time_minutes INT DEFAULT 0,
    temperature_celsius DECIMAL(5,2) DEFAULT 0.00,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    machine_id INT NULL,
    service_type VARCHAR(50) NOT NULL,
    weight_kg DECIMAL(5,2) NOT NULL,
    total_price DECIMAL(10,2) NOT NULL,
    order_status ENUM('Waiting', 'Processing', 'Finished') DEFAULT 'Waiting',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    finished_at TIMESTAMP NULL,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (machine_id) REFERENCES machines(machine_id)
);

CREATE TABLE IF NOT EXISTS payments (
    payment_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    payment_method VARCHAR(30) NOT NULL,
    payment_status ENUM('Pending', 'Paid', 'Failed') DEFAULT 'Pending',
    paid_at TIMESTAMP NULL,
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
);

CREATE TABLE IF NOT EXISTS waiting_queue (
    queue_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT NOT NULL,
    assigned_machine_id INT NULL,
    queue_status ENUM('Waiting', 'Processing', 'Finished') DEFAULT 'Waiting',
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (assigned_machine_id) REFERENCES machines(machine_id)
);
```

Ringkasan struktur tabelnya:

| Tabel | Kolom utama | Fungsi |
|---|---|---|
| `users` | id, username, password_hash, role | Akun pelanggan, petugas, dan owner |
| `customers` | customer_id, user_id, customer_name, phone_number | Data pelanggan (dapat terhubung ke akun login) |
| `machines` | machine_id, machine_name, machine_type, capacity_kg, status, remaining_time_minutes, temperature_celsius | Spesifikasi dan status mesin secara real-time |
| `orders` | order_id, customer_id, machine_id, service_type, weight_kg, total_price, order_status | Pesanan laundry dan statusnya |
| `payments` | payment_id, order_id, amount, payment_method, payment_status | Pembayaran digital per pesanan |
| `waiting_queue` | queue_id, order_id, assigned_machine_id, queue_status | Antrean ruang tunggu |
