#  Perhitungan Function Point (FP) 

## 1. Daftar Fitur & Perhitungan Unadjusted Function Count (UFC)
Tabel estimasi ukuran aplikasi dan fungsionalitas berdasarkan rancangan fitur sistem *Smart Laundry Digital Twin*:

| No. | Nama Fungsi / Fitur Sistem | Jenis Komponen | Tingkat Kerumitan | Bobot | Total |
| :---: | :--- | :---: | :---: | :---: | :---: |
| 1 | Input data konfigurasi unit mesin cuci (kapasitas, tipe) | **EI** | Sederhana | 3 | 3 |
| 2 | Input data status sensor mesin (*live* waktu, getaran, status) | **EI** | Sedang | 4 | 8 |
| 3 | Tampilan antarmuka dashboard visualisasi status unit | **EO** | Sedang | 5 | 10 |
| 4 | Tampilan rekapitulasi status area ruang tunggu | **EO** | Sedang | 5 | 10 |
| 5 | Fitur pencarian ketersediaan mesin cuci (*filter*) | **EQ** | Sederhana | 3 | 3 |
| 6 | Basis data penyimpanan rekam jejak operasional mesin | **ILF** | Kompleks | 15 | 15 |
| 7 | Integrasi data simulasi IoT/sensor washer | **EIF** | Sedang | 7 | 7 |
| **TOTAL UFC** | | | | | **56 FP** |

---

## 2. Penilaian 14 Faktor Penyesuaian Sistem (General System Characteristics / GSC)
Skala penilaian menggunakan rentang nilai 0 (tidak ada pengaruh) hingga 5 (pengaruh sangat esensial):

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
| 12 | Kemudahan operasional bagi admin | 3 |
| 13 | Dukungan multi-perangkat (*responsive design*) | 1 |
| 14 | Kemudahan modifikasi fitur di masa depan | 2 |
| **JUMLAH TOTAL ($\sum F$)** | | **28** |

---

## 3. Perhitungan Value Adjustment Factor (VAF)
Rumus standar perhitungan faktor penyesuaian sistem:

$$VAF = 0,65 + (0,01 \times \sum F)$$
$$VAF = 0,65 + (0,01 \times 28)$$
$$VAF = 0,65 + 0,28 = 0,93$$

---

## 4. Hasil Akhir Function Point (FP)
Perhitungan total ukuran fungsional perangkat lunak:

$$FP = UFC \times VAF$$
$$FP = 56 \times 0,93 = 52,08 \text{ FP}$$

---

## 5. Kesimpulan
> Ukuran fungsional keseluruhan proyek **Smart Laundry (Digital Twin System)** pada tahap perencanaan Sprint 1 adalah **52,08 Function Point**, menunjukkan skala sistem yang terstruktur menengah dan siap dikembangkan secara bertahap.
> 
