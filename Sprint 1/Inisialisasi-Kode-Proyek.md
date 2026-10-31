
# Inisialisasi Kode Proyek — Smart Laundry Digital Twin

## 1. Deskripsi
Smart Laundry adalah aplikasi berbasis web yang dirancang untuk mengelola layanan laundry dan memantau kondisi mesin melalui teknologi Digital Twin.

Sistem memiliki tiga aktor:
1. Pelanggan
2. Petugas
3. Owner

Digital Twin menggunakan simulator perangkat lunak sebagai sumber data kondisi mesin pada tahap awal.

## 2. Rencana Struktur Proyek

```text
smart-laundry-akt25/
├── backend/
│   ├── server.js
│   ├── init_db.js
│   └── package.json
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── app.js
├── simulator/
│   └── machine_simulator.js
├── database/
│   └── schema.sql
└── README.md
```

Struktur tersebut merupakan rencana implementasi dan belum menunjukkan bahwa seluruh kode telah selesai dibuat.

## 3. Rencana Teknologi
- Frontend: HTML, CSS, JavaScript.
- Backend: Node.js dan Express.
- Database: MySQL.
- Simulator: JavaScript.
- Metode pengembangan: Agile Scrum.

## 4. Modul Sistem
1. Autentikasi dan manajemen pengguna.
2. Monitoring status mesin.
3. Pengelolaan pelanggan.
4. Pengelolaan pesanan.
5. Pengelolaan pembayaran.
6. Monitoring antrean.
7. Dashboard dan laporan.

## 5. Rancangan Database
Database direncanakan memiliki tabel:

- users
- customers
- machines
- orders
- payments
- waiting_queue

### Status Mesin
- Available: Mesin tersedia.
- Running: Mesin beroperasi.
- Completed: Siklus pencucian selesai.
- Maintenance: Mesin dalam perawatan.
- Error: Mesin mengalami gangguan.

### Status Pesanan
- Waiting
- Processing
- Finished

### Status Pembayaran
- Pending
- Paid
- Failed

Status mesin, pesanan, dan pembayaran merupakan informasi yang berbeda.

## 6. Rencana Autentikasi
Setiap pengguna masuk melalui akun sesuai perannya.

- Pelanggan mengakses layanan dan pesanan pribadi.
- Petugas mengelola operasional.
- Owner mengakses dashboard dan laporan.

Akun dummy dapat digunakan saat tahap pengembangan.

## 7. Tahapan Implementasi
1. Menyiapkan struktur direktori.
2. Membuat database.
3. Mengembangkan frontend.
4. Mengembangkan backend.
5. Mengintegrasikan simulator mesin.
6. Melakukan pengujian sistem.

## 8. Status Pengembangan
Dokumen ini merupakan rancangan inisialisasi kode.

Implementasi serta pengujian aplikasi dilakukan secara bertahap pada sprint pengembangan berikutnya.
