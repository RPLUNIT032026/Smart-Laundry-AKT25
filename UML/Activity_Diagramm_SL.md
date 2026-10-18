# Activity Diagram — Monitoring Status Mesin Cuci Smart Laundry

Diagram ini menggambarkan proses pemantauan status mesin cuci pada sistem Smart Laundry Digital Twin. Mesin atau perangkat IoT mengirim data status ke sistem, sistem memvalidasi dan menyimpan data, lalu dashboard menampilkan kondisi mesin kepada petugas.

**Swimlane:**
1. Mesin Cuci / IoT
2. Sistem Digital Twin
3. Dashboard & Petugas Laundry

**Alur utama:**
- Mesin membaca dan mengirim status.
- Sistem menerima serta memvalidasi data.
- Jika data tidak valid, sistem menolak data dan menampilkan pesan kesalahan.
- Jika data valid, sistem menyimpan data dan menganalisis status mesin.
- Dashboard menampilkan status Siaga, Sedang Mencuci, Selesai, atau Gangguan.
- Jika terjadi gangguan, dashboard mengirim notifikasi agar petugas memeriksa mesin.

**Catatan:** Diagram ini merupakan rancangan konseptual. Implementasi pemantauan real-time memerlukan mesin/perangkat sensor, koneksi komunikasi, dan perangkat lunak yang mendukung pengiriman data.

<img width="1280" height="1040" alt="WhatsApp Image 2026-10-18 at 5 42 13 PM" src="https://github.com/user-attachments/assets/27bbf0bb-f704-4c2b-809d-f65e63e63a03" />

