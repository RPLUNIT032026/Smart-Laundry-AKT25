# Dokumen Manajemen & Perencanaan Proyek (Sprint 1)
**Nama Proyek:** Smart Laundry (Digital Twin System)

---

## 1. Project Charter
* **Latar Belakang:** Sering terjadinya penumpukan antrean dan ketidakpastian informasi ketersediaan mesin cuci bagi pengunjung laundry koin[span_1](start_span)[span_1](end_span).
* **Tujuan Aplikasi:** Membangun sistem *Digital Twin* berbasis web untuk memantau status operasional mesin dan kapasitas ruang tunggu secara *real-time*[span_2](start_span)[span_2](end_span).
* **Ruang Lingkup Proyek:** 
  * Modul Manajemen Status Mesin Cuci (Aktif/Standby/Selesai).
  * Modul Pemantauan Kepadatan Area Ruang Tunggu.
  * Antarmuka Dashboard Interaktif untuk Pengguna.
* **Struktur Anggota Tim:**
  * **Project Lead:** Ilma Zakiyah (NIM: 250504151)[span_3](start_span)[span_3](end_span)
  * **UI/UX Designer:** Rati Rifa (NIM: 250504152)[span_4](start_span)[span_4](end_span)
  * **Backend Engineer:** M. Syauqan Athaya (NIM: 250504164)[span_5](start_span)[span_5](end_span)

---

## 2. Dokumen Perhitungan Function Point (FP)
Tabel estimasi metrik ukuran aplikasi dan fungsionalitas berdasarkan fitur[span_6](start_span)[span_6](end_span):

| Kategori Fungsional | Deskripsi Fitur / Komponen | Jumlah | Bobot | Total |
| :--- | :--- | :---: | :---: | :---: |
| **External Inputs (EI)** | Form Status Mesin, Panel Kontrol Admin | 2 | 4 | 8 |
| **External Outputs (EO)** | Laporan Selesai Cuci, Notifikasi Web | 2 | 5 | 10 |
| **External Inquiries (EQ)** | Fitur Cek Sisa Waktu, Filter Status Mesin | 2 | 4 | 8 |
| **Internal Logical Files (ILF)**| Database Mesin Cuci, Database Pengunjung | 2 | 10 | 20 |
| **External Interface Files (EIF)**| Integrasi Sensor/Simulasi Data IoT | 1 | 7 | 7 |
| **Total Unadjusted Function Point (UFP)** | | | | **53 FP** |

---

## 3. Product Backlog & Sprint 1 Backlog

### A. Product Backlog (Daftar Seluruh Fitur)
1. Fitur monitoring status mesin cuci secara *real-time*[span_7](start_span)[span_7](end_span).
2. Fitur estimasi durasi dan sisa waktu pencucian[span_8](start_span)[span_8](end_span).
3. Indikator tingkat kepadatan/antrean ruang tunggu[span_9](start_span)[span_9](end_span).
4. Panel kontrol manajemen data operasional bagi pengelola[span_10](start_span)[span_10](end_span).

### B. Sprint 1 Backlog (Target Pekerjaan Saat Ini)
1. **Penyusunan Project Charter:** Menentukan latar belakang, tujuan, ruang lingkup, dan struktur anggota tim[span_11](start_span)[span_11](end_span)[span_12](start_span)[span_12](end_span).
2. **Analisis Function Point:** Menyusun tabel estimasi metrik fungsionalitas aplikasi[span_13](start_span)[span_13](end_span).
3. **Product & Sprint Backlog:** Merinci daftar kebutuhan fitur utama dan target khusus Sprint 1[span_14](start_span)[span_14](end_span).
4. **Project Setup & Dokumentasi Repository:** Inisialisasi struktur folder di GitHub Organization[span_15](start_span)[span_15](end_span)[span_16](start_span)[span_16](end_span).