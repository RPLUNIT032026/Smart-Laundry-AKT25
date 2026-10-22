# 2.1 Rancangan UX/UI - Smart Laundry

Aplikasi dipakai oleh tiga aktor, yaitu **Pelanggan**, **Petugas**, dan **Owner** (sesuai Use Case dan Sequence Diagram Sprint 2). Setiap aktor masuk dengan akunnya (pada tahap pengembangan memakai akun dummy) dan melihat menu sesuai perannya.

# 1. Alur Navigasi Aplikasi

```mermaid
flowchart TD

    A["Splash Screen"] --> B["Login"]
    B --> V{"Akun valid?"}
    V -- "Tidak" --> B
    V -- "Ya" --> R{"Peran pengguna"}

    R -- "Pelanggan" --> MP["Menu Pelanggan"]
    R -- "Petugas" --> MT["Menu Petugas"]
    R -- "Owner" --> MO["Menu Owner"]

    MP --> P1["Buat Pesanan"]
    MP --> P2["Status Pesanan"]
    MP --> P3["Pembayaran Digital"]
    MP --> G["Status Laundry"]
    MP --> H["Profil"]
    MP --> I["Keluar"]

    MT --> D["Tambah Pelanggan"]
    MT --> E["Proses Transaksi"]
    MT --> T1["Perbarui Status Pesanan dan Mesin"]
    MT --> F["Data Transaksi"]
    MT --> G
    MT --> H
    MT --> I

    MO --> G
    MO --> F
    MO --> O1["Konfigurasi Mesin"]
    MO --> H
    MO --> I

    D --> D1["Input Nama"]
    D1 --> D2["Input No HP"]
    D2 --> D3["Simpan Data"]
    D3 --> MT

    E --> E1["Pilih Pelanggan"]
    E1 --> E2["Pilih Layanan"]
    E2 --> E3["Input Berat"]
    E3 --> E4["Hitung Harga"]
    E4 --> E5["Simpan Transaksi"]
    E5 --> MT

    P1 --> P1a["Pilih Layanan dan Input Berat"]
    P1a --> P1b["Konfirmasi Pesanan"]
    P1b --> MP
    P2 --> P2a["Lihat Status Pesanan"]
    P2a --> MP
    P3 --> P3a["Pilih Pesanan dan Bayar"]
    P3a --> MP

    F --> F1["Pilih Transaksi"]
    F1 --> F2["Detail Transaksi"]
    F2 --> BACK["Kembali ke Menu sesuai Peran"]

    G --> G1["Lihat Status Mesin"]
    G1 --> G2["Lihat Kapasitas"]
    G2 --> BACK

    H --> H1["Data Pengguna"]
    H1 --> H2["Pengaturan"]
    H2 --> BACK

    I --> J["Konfirmasi Keluar"]
    J --> K["Logout dan kembali ke Login"]
```

Halaman bersama (Status Laundry, Data Transaksi, Profil) selalu kembali ke menu aktor yang sedang login.

# 2.2 Rancangan Sistem

## 1. Arsitektur Sistem

```mermaid
flowchart TD

    USER["Pengguna (Pelanggan / Petugas / Owner)"]
    UI["Frontend Web Smart Laundry"]
    API["Backend REST API (Login, Pesanan, Pembayaran, Status Mesin)"]
    DB[("Database MySQL")]
    SIM["Simulator Mesin Laundry (data sensor IoT)"]

    USER --> UI
    UI <--> API
    API <--> DB
    SIM --> API
```

Arsitektur ini sejalan dengan struktur kode pada *Inisialisasi-Kode-Proyek* (`frontend/`, `backend/`, `database/`, `simulator/`). Pembagian komponen dan penempatan perangkat yang lebih rinci dijabarkan pada Component Diagram dan Deployment Diagram di Sprint 2.

---

## 2. Flowchart Sistem

```mermaid
flowchart TD

    START(["Mulai"])
    LOGIN["Login dengan akun"]
    VALID{"Akun valid?"}
    MENU["Tampilkan Menu sesuai Peran"]
    PILIH{"Pilih Menu"}

    TAMBAH["Tambah Pelanggan"]
    TRANSAKSI["Proses Transaksi"]
    DATA["Lihat Data Transaksi"]
    STATUS["Lihat Status Mesin dan Kapasitas"]
    KELUAR["Keluar"]

    INPUT1["Input Nama dan No HP"]
    SIMPAN1["Simpan Data Pelanggan"]

    PILIHPEL["Pilih Pelanggan"]
    LAYANAN["Pilih Layanan Laundry"]
    BERAT["Input Berat Pakaian"]
    HARGA["Hitung Harga"]
    SIMPAN2["Simpan Pesanan dan Transaksi"]

    DATABASE[("Database")]

    START --> LOGIN
    LOGIN --> VALID
    VALID -- "Tidak" --> LOGIN
    VALID -- "Ya" --> MENU
    MENU --> PILIH

    PILIH --> TAMBAH
    PILIH --> TRANSAKSI
    PILIH --> DATA
    PILIH --> STATUS
    PILIH --> KELUAR

    TAMBAH --> INPUT1
    INPUT1 --> SIMPAN1
    SIMPAN1 --> DATABASE
    DATABASE --> MENU

    TRANSAKSI --> PILIHPEL
    PILIHPEL --> LAYANAN
    LAYANAN --> BERAT
    BERAT --> HARGA
    HARGA --> SIMPAN2
    SIMPAN2 --> DATABASE

    DATA --> DATABASE
    STATUS --> DATABASE

    KELUAR --> LOGOUT["Logout"]
    LOGOUT --> SELESAI(["Selesai"])
```

Menu "Tambah Pelanggan" dan "Proses Transaksi" hanya tersedia bagi Petugas; Pelanggan membuat pesanannya sendiri dan Owner melihat data transaksi serta status mesin.

---

## 3. ERD / Struktur Database

```mermaid
erDiagram

    USERS ||--o| CUSTOMERS : "memiliki akun"
    CUSTOMERS ||--o{ ORDERS : "membuat"
    MACHINES ||--o{ ORDERS : "memproses"
    ORDERS ||--o{ PAYMENTS : "dibayar lewat"
    ORDERS ||--o| WAITING_QUEUE : "masuk antrean"
    MACHINES ||--o{ WAITING_QUEUE : "melayani"

    USERS {
        int id PK
        string username
        string password_hash
        string role
    }

    CUSTOMERS {
        int customer_id PK
        int user_id FK
        string customer_name
        string phone_number
    }

    MACHINES {
        int machine_id PK
        string machine_name
        string machine_type
        float capacity_kg
        string status
        int remaining_time_minutes
        float temperature_celsius
    }

    ORDERS {
        int order_id PK
        int customer_id FK
        int machine_id FK
        string service_type
        float weight_kg
        float total_price
        string order_status
        string created_at
        string finished_at
    }

    PAYMENTS {
        int payment_id PK
        int order_id FK
        float amount
        string payment_method
        string payment_status
        string paid_at
    }

    WAITING_QUEUE {
        int queue_id PK
        int order_id FK
        int assigned_machine_id FK
        string queue_status
        string joined_at
    }
```

Struktur ERD ini identik dengan `database/schema.sql` pada dokumen *Inisialisasi-Kode-Proyek*.

---
