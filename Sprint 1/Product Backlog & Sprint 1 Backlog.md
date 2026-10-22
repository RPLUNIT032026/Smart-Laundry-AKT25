#  Product Backlog & Sprint 1 Backlog

**Nama Proyek:** Smart Laundry (Digital Twin System)  
**Fokus Tahap:** Perencanaan & Inisialisasi Sprint 1  
**Aktor:** Pelanggan, Petugas, Owner (mesin laundry adalah sumber data *digital twin*, bukan pengguna; lihat Project Charter)

---

## 1. Product Backlog (Daftar Seluruh Fitur Sistem)
Daftar kebutuhan fungsional keseluruhan aplikasi *Smart Laundry* yang diurutkan berdasarkan skala prioritas dan bobot estimasi:

| ID Item | Fitur Utama | Deskripsi User Story | Prioritas | Estimasi (Jam) |
| :---: | :--- | :--- | :---: | :---: |
| **PBI-01** | Konfigurasi Unit Mesin | Sebagai owner, saya ingin memasukkan data spesifikasi mesin cuci (kapasitas dan tipe) agar tercatat di sistem. | Tinggi | 8 jam |
| **PBI-02** | Monitoring Status Mesin | Sebagai pelanggan, petugas, atau owner, saya ingin melihat status unit mesin cuci secara *live* (apakah aktif, siaga, atau selesai). | Tinggi | 16 jam |
| **PBI-03** | Indikator Ruang Tunggu | Sebagai pelanggan, saya ingin mengetahui estimasi tingkat kepadatan di area tunggu *laundry*. | Sedang | 12 jam |
| **PBI-04** | Panel Kontrol Status | Sebagai petugas, saya dapat memperbarui status operasional mesin secara berkala. | Sedang | 10 jam |
| **PBI-05** | Riwayat & Rekap Data | Sebagai owner, saya ingin melihat rekam jejak penggunaan mesin untuk analisis layanan. | Rendah | 14 jam |
| **PBI-06** | Login & Logout Berbasis Peran | Sebagai pelanggan, petugas, atau owner, saya ingin masuk dan keluar dengan akun masing-masing agar hanya melihat menu sesuai peran. | Tinggi | 8 jam |
| **PBI-07** | Data Pelanggan & Pesanan | Sebagai petugas, saya ingin mencatat data pelanggan dan pesanan (layanan, berat, harga); sebagai pelanggan, saya ingin membuat pesanan dan memantau statusnya. | Tinggi | 16 jam |
| **PBI-08** | Pembayaran Digital | Sebagai pelanggan, saya ingin membayar pesanan secara digital agar tidak perlu transaksi tunai. | Sedang | 12 jam |
| **PBI-09** | Riwayat Transaksi | Sebagai owner dan petugas, saya ingin melihat daftar dan detail transaksi laundry. | Sedang | 8 jam |

> PBI-01 s.d. PBI-05 adalah item awal Sprint 1. PBI-06 s.d. PBI-09 ditambahkan setelah perancangan UML Sprint 2 menetapkan tiga aktor beserta alur pesanan dan pembayaran; keempatnya belum masuk Sprint 1 Backlog dan menunggu perencanaan sprint berikutnya.

### Keterkaitan Product Backlog dengan Diagram Sprint 2

| Item | Diagram Sprint 2 yang relevan |
| :---: | :--- |
| PBI-01, PBI-04 | Use Case Diagram, Class Diagram (kelas mesin), State Diagram Status Mesin |
| PBI-02 | Activity Diagram Monitoring Status Mesin Cuci, State Diagram Status Mesin, Context Model (aliran status dari mesin) |
| PBI-03 | Use Case Diagram, Sequence Diagram Pelanggan |
| PBI-05, PBI-09 | Sequence Diagram Owner, Class Diagram |
| PBI-06 | Use Case Diagram, Sequence Diagram Pelanggan / Petugas / Owner |
| PBI-07 | Sequence Diagram Pelanggan dan Petugas, State Diagram Status Pesanan Laundry, Class Diagram |
| PBI-08 | Sequence Diagram Pelanggan, Class Diagram |
| Seluruh PBI | Component Diagram dan Deployment Diagram (arsitektur dan penempatan sistem) |

> Pemetaan di atas disusun dari judul dan peruntukan tiap diagram. Detail isi gambar belum diverifikasi satu per satu.

---

## 2. Sprint 1 Backlog (Target Pekerjaan Saat Ini)

### A. Sprint Goal
Menghasilkan dokumen perencanaan proyek yang komprehensif, merancang arsitektur basis data awal, serta membangun halaman antarmuka web dasar yang terhubung dengan simulasi data unit mesin cuci.

### B. Ringkasan Sprint 1
* **Jumlah PBI yang Dikerjakan:** 3 Item Utama (PBI-01 s.d. PBI-03)
* **Total Estimasi Waktu:** 36 Jam Kerja Tim
* **Durasi Sprint:** 2 Minggu (Siklus Perencanaan Awal)

### C. Daftar Tugas (Task List)
Urutan pengerjaan tugas disesuaikan dengan ketergantungan sistem (basis data dan rancangan awal terlebih dahulu):

| ID Task | Fitur / Bagian | Deskripsi Pekerjaan | PIC / Peran | Estimasi |
| :---: | :--- | :--- | :---: | :---: |
| **T-01** | Dokumen Manajemen | Menyusun Project Charter dan analisis Function Point. | System Analyst | 6 jam |
| **T-02** | Desain UI/UX | Membuat sketsa *wireframe* dan tata letak dashboard utama. | UI/UX Designer | 8 jam |
| **T-03** | Database Setup | Membangun skema tabel relasional untuk data mesin dan ruang tunggu. | Backend Engineer | 8 jam |
| **T-04** | Frontend Dasar | Membangun kerangka HTML, CSS, dan JS untuk tampilan web. | Development Team | 10 jam |
| **T-05** | Integrasi & Setup Repo | Inisialisasi GitHub Organization dan penataan repositori kode. | Project Lead | 4 jam |

---

## 3. Definition of Done (DoD)
Kriteria penyelesaian agar sebuah tugas pada Sprint 1 dianggap tuntas:
* Dokumen perencanaan dan perancangan telah tersusun rapi dalam format Markdown di repositori.
* Desain antarmuka (*wireframe/mockup*) telah ditinjau dan disetujui oleh seluruh anggota tim.
* Struktur kode awal (*HTML/CSS/JS*) dapat dijalankan pada peladen lokal tanpa adanya galat (*error*) kritis.
* Seluruh berkas kode dan dokumen telah berhasil di-*push* ke dalam repositori GitHub kelompok.
