#  Product Backlog & Sprint 1 Backlog

**Nama Proyek:** Smart Laundry (Digital Twin System)  
**Fokus Tahap:** Perencanaan & Inisialisasi Sprint 1

---

## 1. Product Backlog (Daftar Seluruh Fitur Sistem)
Daftar kebutuhan fungsional keseluruhan aplikasi *Smart Laundry* yang diurutkan berdasarkan skala prioritas dan bobot estimasi:

| ID Item | Fitur Utama | Deskripsi User Story | Prioritas | Estimasi (Jam) |
| :---: | :--- | :--- | :---: | :---: |
| **PBI-01** | Konfigurasi Unit Mesin | Sebagai pengelola, saya ingin memasukkan data spesifikasi mesin cuci (kapasitas dan tipe) agar tercatat di sistem. | Tinggi | 8 jam |
| **PBI-02** | Monitoring Status Mesin | Sebagai pengguna, saya ingin melihat status unit mesin cuci secara *live* (apakah aktif, siaga, atau selesai). | Tinggi | 16 jam |
| **PBI-03** | Indikator Ruang Tunggu | Sebagai pengunjung, saya ingin mengetahui estimasi tingkat kepadatan di area tunggu *laundry*. | Sedang | 12 jam |
| **PBI-04** | Panel Kontrol Status | Sebagai admin, saya dapat memperbarui status operasional mesin secara berkala. | Sedang | 10 jam |
| **PBI-05** | Riwayat & Rekap Data | Sebagai pengelola, saya ingin melihat rekam jejak penggunaan mesin untuk analisis layanan. | Rendah | 14 jam |

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
