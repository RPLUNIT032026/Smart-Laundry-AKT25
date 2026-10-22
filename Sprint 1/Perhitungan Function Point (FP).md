# Estimasi Function Point — Smart Laundry (Revisi)

> Estimasi **awal**, bukan pengukuran IFPUG tersertifikasi. Kompleksitas final harus ditentukan dari DET, FTR, dan RET setelah kebutuhan disepakati.

## 1. Unadjusted Function Point (UFP)
Menggunakan bobot standar kompleksitas rendah sebagai asumsi awal untuk menghindari angka total yang tidak memiliki jumlah fungsi.

| Fungsi | Tipe | Jumlah | Bobot/unit | Subtotal |
|---|---|---:|---:|---:|
| Membuat pesanan | EI | 1 | 3 | 3 |
| Mengubah status pesanan | EI | 1 | 3 | 3 |
| Mencatat pembayaran | EI | 1 | 3 | 3 |
| Menerima status mesin | EI | 1 | 3 | 3 |
| Melihat detail/status pesanan | EQ | 1 | 3 | 3 |
| Melihat status mesin | EQ | 1 | 3 | 3 |
| Ringkasan operasional owner | EO | 1 | 4 | 4 |
| Riwayat aktivitas/status | EO | 1 | 4 | 4 |
| Data pengguna | ILF | 1 | 7 | 7 |
| Data pesanan dan pembayaran* | ILF | 2 | 7 | 14 |
| Data mesin dan riwayat status* | ILF | 2 | 7 | 14 |
| **TOTAL UFP** | | | | **61** |

*Asumsi dua kelompok logis terpisah masing-masing; perlu validasi batas file logis saat desain rinci. Simulator internal **tidak otomatis** dihitung sebagai EIF. Autentikasi dan fungsi lain belum dihitung tersendiri untuk menghindari klaim tanpa spesifikasi transaksi elementer.

## 2. Penyesuaian
Gunakan 14 General System Characteristics hanya bila metode perkuliahan mensyaratkan adjusted FP. Nilai sebelumnya 28 belum dievaluasi ulang terhadap perubahan cakupan. Sebagai **simulasi saja**, jika TDI = 28 maka VAF = 0,65 + 0,01 × 28 = **0,93**, sehingga adjusted FP = 61 × 0,93 = **56,73 FP**.

## 3. Kesimpulan
**61 UFP** adalah estimasi perencanaan sementara. **56,73 adjusted FP** hanya berlaku pada asumsi TDI 28. Tidak boleh menyatakan angka ini ukuran final sebelum klasifikasi dan tingkat kompleksitas diverifikasi.
