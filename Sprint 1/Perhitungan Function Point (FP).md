#  Perhitungan Function Point (FP) 

## 1. Daftar Fitur & Perhitungan Unadjusted Function Count (UFC)
Tabel estimasi ukuran aplikasi dan fungsionalitas berdasarkan rancangan fitur sistem *Smart Laundry Digital Twin*. Kolom **Total = Bobot × Jumlah** (jumlah menunjukkan banyaknya fungsi sejenis pada baris tersebut).

### A. Modul Pemantauan Mesin dan Kapasitas (rancangan awal Sprint 1)

| No. | Nama Fungsi / Fitur Sistem | Jenis Komponen | Tingkat Kerumitan | Bobot | Jumlah | Total |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| 1 | Input data konfigurasi unit mesin cuci (kapasitas, tipe) | **EI** | Sederhana | 3 | 1 | 3 |
| 2 | Input data status sensor mesin (*live* waktu, getaran, status) | **EI** | Sedang | 4 | 2 | 8 |
| 3 | Tampilan antarmuka dashboard visualisasi status unit | **EO** | Sedang | 5 | 2 | 10 |
| 4 | Tampilan rekapitulasi status area ruang tunggu | **EO** | Sedang | 5 | 2 | 10 |
| 5 | Fitur pencarian ketersediaan mesin cuci (*filter*) | **EQ** | Sederhana | 3 | 1 | 3 |
| 6 | Basis data penyimpanan rekam jejak operasional mesin | **ILF** | Kompleks | 15 | 1 | 15 |
| 7 | Integrasi data simulasi IoT/sensor washer | **EIF** | Sedang | 7 | 1 | 7 |
| **Subtotal A** | | | | | | **56** |

### B. Modul Pelanggan, Pesanan, dan Pembayaran (ditambahkan mengikuti perancangan UML Sprint 2)

Sprint 2 menetapkan tiga aktor (Pelanggan, Petugas, Owner) beserta alur pesanan, status pesanan, dan pembayaran digital, sehingga fungsi berikut ditambahkan ke estimasi.

| No. | Nama Fungsi / Fitur Sistem | Jenis Komponen | Tingkat Kerumitan | Bobot | Jumlah | Total |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| 8 | Login dan logout berbasis peran (Pelanggan, Petugas, Owner) | **EI** | Sederhana | 3 | 1 | 3 |
| 9 | Input dan kelola data pelanggan | **EI** | Sederhana | 3 | 1 | 3 |
| 10 | Input pesanan laundry (layanan, berat, hitung harga) | **EI** | Sedang | 4 | 1 | 4 |
| 11 | Perbarui status pesanan laundry | **EI** | Sederhana | 3 | 1 | 3 |
| 12 | Input pembayaran digital | **EI** | Sedang | 4 | 1 | 4 |
| 13 | Tampilan status pesanan dan pembayaran bagi pelanggan | **EO** | Sedang | 5 | 1 | 5 |
| 14 | Tampilan riwayat transaksi dan rekap data bagi owner | **EO** | Sedang | 5 | 1 | 5 |
| 15 | Pencarian dan detail pesanan/transaksi | **EQ** | Sederhana | 3 | 1 | 3 |
| 16 | Basis data pengguna, pelanggan, pesanan, dan pembayaran | **ILF** | Sedang | 10 | 1 | 10 |
| **Subtotal B** | | | | | | **40** |

| Ringkasan | Nilai |
| :--- | :---: |
| Subtotal A (modul pemantauan) | 56 |
| Subtotal B (modul pesanan dan pembayaran) | 40 |
| **TOTAL UFC** | **96 FP** |

---

## 2. Penilaian 14 Faktor Penyesuaian Sistem (General System Characteristics / GSC)
Skala penilaian menggunakan rentang nilai 0 (tidak ada pengaruh) hingga 5 (pengaruh sangat esensial). Nilai GSC tidak diubah dari penilaian awal.

| No. | Faktor Pengaruh Sistem | Nilai (0–5) |
| :---: | :--- | :---: |
| 1 | Komunikasi data (koneksi web & peladen) | 2 |
| 2 | Fungsi terdistribusi (arsitektur modular) | 1 |
| 3 | Kinerja sistem (*responsiveness*) | 2 |
| 4 | Konfigurasi perangkat keras (kompatibilitas server) | 1 |
| 5 | Tingkat transaksi data harian | 2 |
| 6 | Masukan data pengguna secara interaktif | 2 |
| 7 | Kemudahan efisiensi pengguna (*user experience*) | 3 |
| 8 | Pembaruan data langsung (*live update*) | 3 |
| 9 | Kompleksitas pemrosesan logika sistem | 2 |
| 10 | Penggunaan kembali kode (*reusability*) | 2 |
| 11 | Kemudahan instalasi perangkat lunak | 2 |
| 12 | Kemudahan operasional bagi petugas dan owner | 3 |
| 13 | Dukungan multi-perangkat (*responsive design*) | 1 |
| 14 | Kemudahan modifikasi fitur di masa depan | 2 |
| **JUMLAH TOTAL ($\sum F$)** | | **28** |

---

### 3. Perhitungan Value Adjustment Factor (VAF)

Rumus standar perhitungan faktor penyesuaian sistem:

**VAF = 0,65 + (0,01 × ΣF)**

Diketahui:
- Total nilai General System Characteristics (ΣF) = 28
- Konstanta dasar = 0,65
- Faktor penyesuaian = 0,01

Perhitungan:

VAF = 0,65 + (0,01 × 28)

VAF = 0,65 + 0,28

**VAF = 0,93**

### 4. Hasil Akhir Function Point (FP)

Rumus perhitungan:

**FP = UFC × VAF**

Diketahui:
- Unadjusted Function Count (UFC) = 96
- Value Adjustment Factor (VAF) = 0,93

Perhitungan:

FP = 96 × 0,93

**FP = 89,28 FP**

### 5. Perbandingan Estimasi Function Point

Sebagai pembanding, estimasi awal Sprint 1 hanya mencakup modul pemantauan mesin (Subtotal A).

FP Awal = 56 × 0,93

**FP Awal = 52,08 FP**

Dengan demikian, estimasi ukuran fungsional keseluruhan sistem Smart Laundry Digital Twin adalah **89,28 FP**, sedangkan estimasi awal modul pemantauan sebesar **52,08 FP**.

Catatan: Hasil ini berlaku apabila nilai UFC dan VAF yang digunakan telah diverifikasi berdasarkan tabel perhitungan.
