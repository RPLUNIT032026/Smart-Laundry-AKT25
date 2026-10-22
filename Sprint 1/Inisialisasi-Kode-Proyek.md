# Inisialisasi Kode Proyek — Rencana Teknis

> **Status:** rancangan struktur dan contoh kontrak; ZIP dokumentasi ini **belum menyertakan** implementasi `backend/`, `frontend/`, `simulator/`, atau `database/`. Jangan menjalankan perintah seolah file sudah ada.

## Struktur yang direncanakan
```text
smart-laundry/
├── frontend/           # UI pelanggan, petugas, owner
├── backend/            # API autentikasi, orders, payments, machines
├── simulator/          # pembaruan status mesin (simulasi)
├── database/           # migrasi dan seed data
├── Sprint 1/           # dokumen perencanaan
├── Sprint 2/           # delapan dokumen UML
└── README.md
```

## Modul dan Endpoint Usulan
| Metode | Endpoint | Tujuan |
|---|---|---|
| POST | `/api/auth/login` | Autentikasi |
| GET/POST | `/api/orders` | Daftar / buat pesanan |
| GET | `/api/orders/:id` | Detail dan status pesanan |
| PATCH | `/api/orders/:id/status` | Pembaruan status oleh petugas |
| POST | `/api/orders/:id/payments` | Pencatatan pembayaran |
| GET | `/api/machines` | Status Digital Twin mesin |
| POST | `/api/machines/:id/telemetry` | Input status simulator/perangkat (terotorisasi) |
| GET | `/api/owner/summary` | Ringkasan owner |
| GET | `/api/history` | Riwayat sesuai izin akses |

Endpoint ini **belum dibuktikan terimplementasi**; sesuaikan dengan rancangan Sequence dan Component Sprint 2.

## Entitas Minimal
`users(id, name, role, password_hash)`; `orders(id, customer_id, machine_id, service_type, price, status, created_at)`; `payments(id, order_id, amount, method, status, paid_at)`; `machines(id, name, status, remaining_minutes, updated_at)`; `machine_status_history(id, machine_id, status, source, recorded_at)`; `order_status_history(id, order_id, status, recorded_at)`.

## Alur Data Digital Twin
1. Simulator atau perangkat mengirim identitas mesin, status, sisa waktu, cap waktu.
2. Backend memvalidasi mesin, sumber, dan rentang nilai.
3. Status terkini dan riwayat diperbarui.
4. Dashboard menampilkan status terbaru dan penanda data terlambat.

## Keamanan dan Praktik Pengembangan
Gunakan password hash, token/sesi aman, pembatasan akses per peran, variabel lingkungan untuk rahasia, validasi input, serta `.gitignore` untuk `.env` dan `node_modules`. **Jangan mencantumkan kredensial default nyata di dokumentasi.**

## Langkah implementasi selanjutnya
Buat direktori kode, migrasi database, backend API, simulator, UI, dan tes integrasi; dokumentasikan perintah instalasi **setelah** `package.json` dan skrip benar-benar tersedia.
