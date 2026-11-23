# UI/UX Design — Smart Laundry Digital Twin

> **Sprint 1 — Spesifikasi antarmuka dan pengalaman pengguna**  
> Tema: **Clean Blue Laundry** (biru bersih dengan aksen kuning, hijau, dan merah lembut).  
> Dokumen ini diselaraskan dengan prototipe **Wash Smart Laundry** (`Wash_SmartLaundry.zip`: HTML + CSS + JavaScript statis, data tersimpan di `localStorage` browser). Warna, ukuran, komponen, nama menu, dan label status di bawah diambil langsung dari prototipe tersebut. Bagian yang belum terpenuhi prototipe dicatat jujur pada **Bagian 9**.

## 1. Tujuan dan ruang lingkup

Merancang antarmuka responsif untuk tiga aktor yang dijelaskan dalam dokumentasi Sprint 2: **Pelanggan (Customer), Petugas, dan Owner**. Sistem mendukung pengelolaan pesanan dan pembayaran serta **Digital Twin** untuk memantau status mesin. Data mesin pada tahap ini berasal dari simulasi di aplikasi (timer per mesin); jangan menyebutnya pembacaan sensor nyata jika belum ada perangkat fisik.

**Prinsip penting:** status **pesanan**, **pembayaran**, dan **mesin** adalah tiga informasi berbeda dan tidak boleh disatukan dalam satu label status.

## 2. Prinsip UX

- Antarmuka sederhana, ramah, responsif, dan mudah digunakan pada HP maupun desktop.
- Pada halaman masuk, pengguna memilih jenis akun (**Owner / Petugas / Customer**) hanya untuk memandu isi form. **Izin tindakan mengikuti role akun yang tersimpan**: jenis akun yang tidak cocok dengan akun ditolak, dan setiap aksi dicek ulang berdasarkan role.
- Warna status selalu didampingi teks (label pada badge), sehingga tidak mengandalkan warna saja.
- Aksi penting (membuat pesanan, mengubah status, konfirmasi pembayaran, menonaktifkan akun) memerlukan validasi dan umpan balik.
- Tampilkan kondisi data kosong, error, akses ditolak, dan kegagalan penyimpanan (lihat Bagian 8).
- Data Digital Twin menampilkan **sumber data**, **waktu pembaruan terakhir**, dan label **SIMULASI** selama datanya berasal dari simulasi (status pemenuhan: Bagian 9).
- Jika pembaruan data terlambat, tampilkan **Data belum terkonfirmasi**, bukan menyatakan mesin pasti aktif atau tersedia.

## 3. Design System — Clean Blue Laundry

### 3.1 Palet warna

Warna diterapkan sebagai variabel CSS (`:root`) pada `assets/css/style.css`.

#### Mode terang (default)

| Elemen | Token CSS | Hex | Penggunaan |
|---|---|---|---|
| Primary | `--pri` | `#4A86F0` | Tombol utama, tautan, fokus input, langkah aktif pada stepper |
| Primary Dark | `--pri-d` | `#1F5FC4` | Hover tombol utama, judul besar, label form, teks menu aktif |
| Primary Light | `--pri-l` | `#E4EEFE` | Latar menu aktif, badge *Diproses Mesin*, chip, kotak informasi |
| Warning (latar) | `--yel` | `#FDF1C4` | Badge *Menunggu Antrean* / *Belum bayar*, kotak total biaya, peringatan |
| Warning (teks) | `--yel-d` | `#9A6B00` | Teks di atas latar kuning |
| Success (latar) | `--grn` | `#E2F6EC` | Badge *Siap Diambil*, *Lunas*, *Selesai* |
| Success (teks) | `--grn-d` | `#1D7A4D` | Teks di atas latar hijau, indikator "Sistem terhubung" |
| Danger (latar) | `--red` | `#FDE6E6` | Badge *Dibatalkan* / *Perbaikan*, kotak error |
| Danger (teks) | `--red-d` | `#B83A3A` | Teks di atas latar merah, tombol Logout |
| Background | `--bg` | `#F6F9FE` | Latar aplikasi |
| Card | `--card` | `#FFFFFF` | Kartu, sidebar, topbar, modal, formulir |
| Text | `--ink` | `#1C2B4A` | Teks utama dan latar toast |
| Muted Text | `--mut` | `#6B7A96` | Teks penjelas, header tabel |
| Border | `--line` | `#E3EAF5` | Garis pembatas kartu, tabel, dan input |

**Warna pendukung**

| Penggunaan | Warna |
|---|---|
| Badge default (*Dibuat*, *Telah Diambil*, *Tersedia*, *Nonaktif*) | `#EEF1F6` dengan teks `--mut` |
| Header tabel | `#F6F9FD` |
| Kartu mesin | `#FAFCFF` dengan border `--line` |
| Tombol *ghost* | `#EEF2F8` (hover `#E2E8F2`) |
| Panel "Butuh bantuan?" | `#F3F6FB` |
| Gradien banner (*hero*) | `linear-gradient(90deg, #E1ECFD, #FDF3CF)` |
| Gradien panel kiri halaman masuk | `linear-gradient(160deg, #E6F1FF, #CFE3FC)` |
| Grafik pendapatan harian | Batang `#C9DCFB`, hari ini `#F3C94D` |
| Avatar tanpa foto | Latar `--yel` |

#### Mode gelap (`[data-theme=dark]`)

Dapat diaktifkan pengguna lewat **Pengaturan > Preferensi > Mode gelap**.

| Token | Hex | | Token | Hex |
|---|---|---|---|---|
| `--bg` | `#0F172A` | | `--grn` / `--grn-d` | `#12382A` / `#6FE0A8` |
| `--card` | `#16213A` | | `--yel` / `--yel-d` | `#4A3D12` / `#F3D572` |
| `--line` | `#2A3856` | | `--red` / `--red-d` | `#3D1C1C` / `#FF9A9A` |
| `--ink` | `#E6ECF8` | | `--pri-l` | `#1E3358` |
| `--mut` | `#98A7C4` | | `--pri-d` | `#8FB4FF` |

> **Aksesibilitas (rasio kontras terhitung dari warna di atas):**
>
> | Pasangan warna | Rasio |
> |---|---|
> | Teks utama `#1C2B4A` di latar `#F6F9FE` | 13,32 : 1 |
> | Teks utama di kartu putih | 14,06 : 1 |
> | Label form / hover primer (`#1F5FC4`, putih) | 6,01 : 1 |
> | Badge biru (`#1F5FC4` di `#E4EEFE`) | 5,14 : 1 |
> | Badge hijau (`#1D7A4D` di `#E2F6EC`) | 4,72 : 1 |
> | Badge merah (`#B83A3A` di `#FDE6E6`) | 4,76 : 1 |
> | Teks redup `#6B7A96` di kartu putih | 4,33 : 1 |
> | Badge kuning (`#9A6B00` di `#FDF1C4`) | 4,14 : 1 |
> | Teks putih di tombol primer `#4A86F0` | 3,52 : 1 |
>
> Warna status dipakai sebagai latar badge dengan teks berwarna tua dari keluarga yang sama. Pasangan di bawah 4,5 : 1 dicatat pada Bagian 9.

### 3.2 Tipografi dan komponen

- Font: **Inter** (Google Fonts), cadangan `system-ui`, `sans-serif`. Tampilan tetap terbaca tanpa internet.
- Ukuran teks:

| Elemen | Ukuran / bobot |
|---|---|
| Teks dasar (body) | 14 px |
| Judul halaman (topbar) | 20 px semibold (17 px di HP) |
| Judul kartu (H3) | 16 px semibold |
| Judul banner (*hero*) | 26 px semibold (21 px di HP) |
| Angka statistik | 26 px |
| Timer mesin | 28 px semibold, angka rata (*tabular*) |
| Harga layanan | 30 px bold |
| Judul halaman masuk | 42 px (panel kiri), 30 px (form; 26 px di HP) |
| Label form | 12 px medium, warna `--pri-d` |
| Badge / header tabel / caption | 11–12 px |

- **Tombol:** radius 10 px, padding 10 × 16 px (tinggi ± 40 px), teks semibold. Primer: latar `--pri`, teks putih, hover `--pri-d`. Varian: *ghost* (abu), *outline* (putih + border), *sm* (padding 6 × 12 px, teks 12 px). Disabled: opasitas 50%.
- **Kartu:** latar putih, radius 12 px, border 1 px `--line`, padding 20 px (16 px di HP), **tanpa bayangan**. Banner (*hero*) radius 16 px, padding 28 px.
- **Input:** label selalu terlihat di atas field, radius 10 px, border `--line`, padding 11 × 14 px. Fokus: border `--pri` dan cincin 3 px biru transparan. Pesan error/sukses tampil sebagai kotak berwarna di atas form (merah / hijau, radius 8 px).
- **Badge:** radius 6 px, teks 11 px, `padding 3 × 10 px`. **Chip:** radius penuh (20 px), dipakai untuk "Digital Twin • Terhubung".
- **Modal:** radius 16 px, padding 24 px, lebar maksimum 480 px (struk 430 px), animasi muncul singkat, tutup dengan tombol ✕, klik latar, atau tombol Esc.
- **Toast:** kapsul gelap (`--ink`) di tengah bawah layar, hilang otomatis.
- **Stepper pesanan (5 langkah):** langkah selesai = lingkaran `--pri-l`, langkah aktif = lingkaran `--pri` teks putih tebal, langkah berikutnya = abu.
- **Kartu mesin:** nama + badge status, sisa waktu besar, info pesanan, batang progres 5 px.
- **Navigasi:** sidebar putih lebar 240 px (item radius 10 px, aktif `--pri-l`), topbar putih *sticky* dengan lonceng notifikasi dan menu akun (avatar foto atau inisial).
- **Tab jenis akun** (halaman masuk/daftar): kontrol tiga segmen *Owner | Petugas | Customer*, segmen aktif putih dengan bayangan tipis.
- **Saklar (toggle)** 42 × 24 px untuk preferensi pengaturan.
- **Responsif:**
  - Desktop: sidebar + area konten (kartu statistik 4 kolom, grid 2 kolom untuk grafik dan log).
  - HP (≤ 900 px): sidebar menjadi **menu geser** (tombol ☰, lebar 260 px, latar gelap transparan), kartu satu kolom, tabel bisa digeser ke samping (min. 520 px), chip "Digital Twin" disembunyikan, halaman masuk menampilkan logo di atas form (panel kiri disembunyikan). Mendukung *safe area* HP.
  - Cetak struk: hanya isi struk yang dicetak. Animasi dimatikan bila pengguna memilih *reduced motion*.
- **Logo:** `logo-washwash.png` (halaman masuk, logo penuh) dan `logo-icon.png` (sidebar, di samping teks "WASH WASH / LAUNDRY"). Logo tidak boleh diubah atau diganti ikon lain.

### 3.3 Aturan Status Sistem

Status pada antarmuka mengikuti prototipe. Setiap status tampil sebagai badge berwarna **dengan teks**.

| Kategori | Status (tampilan) | Warna badge | Catatan |
|---|---|---|---|
| Pesanan | **Dibuat** | Abu | Langkah 1 pada stepper (selalu tercapai) |
| Pesanan | **Menunggu Antrean** | Kuning | Status awal pesanan baru |
| Pesanan | **Diproses Mesin** | Biru | Setelah petugas memilih mesin |
| Pesanan | **Siap Diambil** | Hijau | Mesin dibebaskan |
| Pesanan | **Telah Diambil** | Abu | Pesanan selesai; pembayaran harus sudah lunas |
| Pesanan | **Dibatalkan** | Merah | Hanya bisa dari *Menunggu Antrean*, oleh pelanggan |
| Mesin | **Tersedia** | Abu | Siap digunakan |
| Mesin | **Mencuci** | Biru | Menampilkan sisa waktu dan pesanan terkait |
| Mesin | **Selesai** | Hijau | Timer habis; pesanan menunggu petugas menekan *Siap diambil* |
| Mesin | **Perbaikan** | Merah | Tidak bisa dipilih untuk pesanan |
| Mesin | **Nonaktif** | Abu, kartu diredupkan | Dinonaktifkan owner |
| Pembayaran | **Belum bayar** | Kuning | Termasuk QRIS yang menunggu pembayaran |
| Pembayaran | **Lunas** | Hijau | Dengan metode **QRIS** atau **Bayar di tempat (tunai)** |

Aturan lintas status:

- Status mesin, pesanan, dan pembayaran ditampilkan secara terpisah (badge terpisah pada kolom *Status* dan *Bayar*).
- Status mesin **Selesai** tidak otomatis mengubah status pesanan menjadi *Siap Diambil*; petugas yang mengubahnya.
- Pesanan **QRIS yang belum dibayar tidak dapat diproses** ke mesin. QRIS berlaku 15 menit; jika kedaluwarsa, tampil "QRIS kedaluwarsa" dan tombol **Terbitkan ulang QRIS**.
- Pesanan tidak dapat ditandai *Telah Diambil* sebelum pembayaran **Lunas**.
- Pembayaran tunai dicatat petugas dengan uang diterima dan kembalian otomatis.
- Data mesin pada tahap awal berasal dari simulasi aplikasi. Status "Gagal" untuk pembayaran belum ada di prototipe (kasus gagal diwakili QRIS kedaluwarsa).

## 4. Sitemap

<img width="1417" height="616" alt="sitemap2 drawio" src="https://github.com/user-attachments/assets/d2421057-15d7-4e87-8e4a-726c81dbe973" />

**Sitemap sesuai prototipe (nama menu persis seperti di aplikasi):**

| Area | Menu / halaman |
|---|---|
| Publik | Masuk (tab Owner / Petugas / Customer) · Daftar · Lupa kata sandi (khusus Customer) · Kebijakan Privasi · Syarat & Ketentuan · Bantuan |
| Pelanggan | **Dashboard** · **Buat Pesanan** (modal) · **Pantau / Lacak Status** · Detail pesanan & struk (modal) · Pembayaran QRIS (modal) |
| Petugas | **Dashboard** · **Lihat Antrean** · **Monitoring Mesin IoT** · **Update Status** · Proses di mesin / Terima pembayaran / Catat Pesanan Pelanggan (modal) |
| Owner | **Dashboard** · **Lihat Laporan** · **Kelola Layanan** · **Monitoring & Riwayat Mesin** · **Pantau Kinerja** · **Manajemen Karyawan** |
| Semua peran | Menu akun (klik nama/avatar di kanan atas): **Edit Profil** · **Pengaturan** · Bantuan · Kebijakan Privasi · Syarat & Ketentuan · Logout; ikon lonceng = Notifikasi |

**Tab Pengaturan dibedakan per peran:**

| Peran | Tab |
|---|---|
| Pelanggan | Profil · Notifikasi · Preferensi · Keamanan |
| Petugas | Profil · Tugas & Shift · Preferensi · Keamanan |
| Owner | Profil · Info Usaha · Notifikasi · Preferensi · Keamanan |

Profil semua peran dapat diberi **foto** (dipotong persegi otomatis).

## 5. User Flow

### 5.1 Login

<img width="862" height="652" alt="use flow drawio" src="https://github.com/user-attachments/assets/8240fe60-e893-4a59-8f3a-ddd1679348a2" />

Alur teks sesuai prototipe:

1. Pilih jenis akun: **Owner**, **Petugas**, atau **Customer**.
2. Isi **email** dan **kata sandi**; format email dan kata sandi divalidasi.
3. Sistem mencocokkan kata sandi (disimpan sebagai hash) dan memeriksa bahwa role akun sama dengan jenis akun yang dipilih. Gagal: "Email atau kata sandi salah." atau pesan jenis akun tidak sesuai.
4. Berhasil: diarahkan ke dashboard sesuai role. **5 kali gagal = login dikunci 5 menit.**
5. **Daftar:** Customer cukup nama, email, kata sandi. **Petugas dan Owner memerlukan kode keamanan** pada form daftar.
6. **Lupa kata sandi:** hanya untuk akun Customer. Akun Petugas/Owner direset oleh Owner (Manajemen Karyawan).

### 5.2 Pelanggan

<img width="415" height="872" alt="pelanggan drawio" src="https://github.com/user-attachments/assets/7d750514-e89b-400d-ad45-473119fbff34" />

Alur teks: masuk → Dashboard → **Buat Pesanan Baru** → pilih layanan, berat, mesin (opsional), catatan, metode bayar → **Kirim Pesanan** → bila QRIS: layar pembayaran QRIS → pantau di **Pantau / Lacak Status** → ambil cucian → lihat/cetak struk dari **Detail**.

### 5.3 Petugas dan Owner

- **Petugas:** masuk → Dashboard (antrean, mesin) → pilih pesanan di **Lihat Antrean** → *Konfirmasi lunas* (QRIS) atau *Proses di mesin* (pilih mesin dan durasi) → *Siap diambil* → *Terima pembayaran* bila tunai belum dibayar → *Telah diambil*. Dapat **Catat Pesanan Pelanggan** untuk pelanggan yang datang langsung dan mengatur status mesin (siaga/perbaikan) di **Update Status**.
- **Owner:** masuk → Dashboard (pendapatan, utilisasi mesin, kinerja) → **Lihat Laporan** (periode 7 hari / 30 hari / Semua, ekspor CSV) → **Kelola Layanan**, **Monitoring & Riwayat Mesin** (konfigurasi unit + rekap penggunaan), **Pantau Kinerja**, **Manajemen Karyawan** (tambah, ubah, nonaktifkan petugas).

## 6. Wireframe halaman

> Wireframe berikut berupa teks agar mudah dibuat ulang di Figma atau Draw.io. Warna dan tipografi mengikuti Design System pada Bagian 3. Nama menu dan label mengikuti prototipe.

### 6.1 Login dan Daftar

```text
+-----------------------------------+--------------------------------------+
| smart laundry digital twin        |                 Butuh bantuan? Hubungi kami |
| WASH WASH LAUNDRY                 |                                      |
| Cucian beres.                     |  Selamat datang kembali              |
| tinggal santai.                   |  Masuk untuk pesan layanan ...       |
| (teks sambutan 3 baris)           |  [ Owner | Petugas | Customer ]      |
| Pesan lebih praktis | Riwayat rapi|  Email        [____________________] |
| [ logo Wash Wash Laundry ]        |  Kata sandi   [__________] [Lihat]   |
| Masuk dulu, sisanya lebih mudah.  |  [ ] Ingat saya    Lupa kata sandi?  |
| (latar gradasi biru muda)         |  [   Masuk sebagai Customer   ]      |
|                                   |  Belum punya akun? Daftar sekarang   |
|                                   |  Kebijakan Privasi · Syarat & Ketentuan |
+-----------------------------------+--------------------------------------+
Mobile: panel kiri disembunyikan; logo tampil di atas form.
Daftar: tab jenis akun, Nama, Email, Kata sandi, Ulangi kata sandi,
        Kode keamanan (hanya Petugas/Owner), [x] setuju Syarat & Kebijakan.
```

### 6.2 Pelanggan — Dashboard dan Pantau / Lacak Status

```text
+-----------+---------------------------------------------------------------+
| [logo]    | Dashboard Pelanggan                    [lonceng] (B) Halo, Budi v |
| WASH WASH | Minggu, 22 November 2026                                      |
| LAUNDRY   | +-----------------------------------------------------------+ |
|           | | Buat Harimu Lebih Santai          [ + Buat Pesanan Baru ] | |
| Dashboard | +-----------------------------------------------------------+ |
| Buat Pesanan | [Cucian Aktif] [Menunggu Antrean] [Selesai] [Ruang tunggu] |
| Pantau /  | Pelacakan Pesanan Aktif                       1 dari N  < > |
|  Lacak    | #WW-0001  Ekspres 4kg  Rp48.000   [Diproses Mesin]            |
| Status    | (1)Dibuat (2)Menunggu (3)Diproses (4)Siap Diambil (5)Telah Diambil |
|           | Mesin 02 · Perkiraan selesai 14:48        [Batalkan Pesanan]  |
| Butuh     | Riwayat Pesanan                                               |
| bantuan?  | No. Order | Tanggal | Layanan & Berat | Total | Status | Aksi |
| Logout    | #WW-0001  | 22 Nov  | Ekspres • 4 kg  | 48.000| ...    |[Detail]|
+-----------+---------------------------------------------------------------+
Kartu "Ruang tunggu" menampilkan Sepi / Sedang / Ramai dari jumlah pesanan aktif.
```

### 6.3 Pelanggan — Buat Pesanan (modal)

```text
+---------------------------------------------------+
| Buat Pesanan Baru                              [x] |
| Smart Laundry Digital Twin System                  |
| Pilih Jenis Layanan Mesin                          |
| (o) Reguler        Rp7.000/kg                      |
| ( ) Ekspres        Rp12.000/kg                     |
| ( ) Cuci Basah     Rp5.000/kg                      |
| Perkiraan Berat Cucian (Kg)   [ - ]  4  [ + ]      |
| Pilih Unit Mesin Tersedia  [Biarkan petugas memilih v] |
| Catatan Tambahan (opsional) [____________________] |
| Metode Pembayaran  (o) QRIS   ( ) Bayar di Tempat  |
| +-----------------------------------------------+ |
| | Total Estimasi Biaya                 Rp28.000  | |
| | Estimasi selesai: 2 hari                       | |
| +-----------------------------------------------+ |
| [ Batal ]                     [ Kirim Pesanan ]    |
+---------------------------------------------------+
```

### Ketentuan Pembuatan Pesanan

Pelanggan dapat memilih layanan laundry dan membuat pesanan.

Berat laundry dan total harga tercatat sebelum pesanan disimpan: pelanggan mengisi **perkiraan berat 1–15 kg**, total = harga per kg × berat. Berat final ditimbang petugas saat cucian diterima. Pesanan **walk-in** yang dicatat petugas dapat sampai 30 kg.

Informasi yang ditampilkan meliputi:
- Jenis layanan
- Berat laundry
- Estimasi atau total harga
- Status pesanan
- Informasi pembayaran

### 6.4 Pelanggan — Detail Pesanan, Pembayaran QRIS, dan Struk

```text
Pembayaran QRIS (modal)                 Detail pesanan / Struk (modal)
+--------------------------------+      +-------------------------------------+
| Pembayaran QRIS            [x] |      | WASH WASH LAUNDRY (nama usaha)   [x] |
| #WW-0001 · Ekspres 4 kg        |      | #WW-0001   [Diproses Mesin] [Lunas]  |
|        [  kode QR  ]           |      | Pelanggan · Layanan · Berat          |
| Total pembayaran     Rp48.000  |      | Harga/kg · Total · Metode            |
| Ref: QR261122ABC123            |      | Pembayaran: Lunas · 22 Nov 14:20     |
| Selesaikan dalam 14:32         |      | Dibuat · Petugas · Catatan           |
| [ Saya sudah membayar ]        |      | (stepper 5 langkah)                  |
| [ Bayar nanti ]                |      | [ Cetak Struk ]  [ Tutup ]           |
| Kedaluwarsa: [Terbitkan ulang] |      +-------------------------------------+
+--------------------------------+
Tombol "Saya sudah membayar" adalah simulasi pembayaran.
```

### 6.5 Petugas — Dashboard Operasional

```text
+-----------+---------------------------------------------------------------+
| [logo]    | Workspace / Petugas                [Digital Twin • Terhubung]  |
| SMART     | Ringkasan operasional                      [lonceng] (P) Petugas 01 v |
| LAUNDRY   | Selamat pagi, Petugas!                  [Shift pagi · 08.00–16.00] |
| SYSTEM    | [ + Catat Pesanan Pelanggan ]                                 |
| AREA      | [Antrean Masuk] [Diproses Mesin] [Siap Diambil] [Mesin Aktif 3/4] |
| PETUGAS   | Monitoring mesin IoT                        [● MQTT terhubung] |
| Dashboard | [Mesin 01 Mencuci 18:42] [Mesin 02 Tersedia] [Mesin 03 Perbaikan] ... |
| Lihat     | Antrean pesanan                     [Cari nama atau ID pesanan] |
|  Antrean  | ID | Pelanggan | Layanan | Berat | Masuk | Status | Bayar | Aksi |
| Monitoring| WW-0001 | Budi | Reguler | 4 kg | 09:15 | Menunggu | Lunas | [Proses di mesin] |
| Mesin IoT | Menampilkan 4 dari 23 pesanan aktif                           |
| Update    +---------------------------------------------------------------+
|  Status   | [● Sistem terhubung · MQTT broker online] (kartu sidebar)     |
+-----------+---------------------------------------------------------------+
```

### 6.6 Petugas — Proses Pesanan dan Update Status

```text
Aksi pada baris antrean (berubah menurut status):
  Menunggu Antrean + QRIS belum bayar -> [Konfirmasi lunas]
  Menunggu Antrean                    -> [Proses di mesin]
  Diproses Mesin                      -> [Siap diambil]
  Siap Diambil + belum lunas          -> [Terima pembayaran]
  Siap Diambil + lunas                -> [Telah diambil]

Proses di mesin (modal)             Terima pembayaran (modal)
+------------------------------+    +----------------------------------+
| Proses #WW-0001           [x] |    | Terima pembayaran             [x] |
| Budi · Reguler 4 kg           |    | Total tagihan          Rp28.000   |
| Pilih mesin  [Mesin 01 · 15kg v]    | Uang diterima [ 50000 ]           |
| Durasi (menit) [ 60 ]         |    | [Uang pas] [50.000] [100.000]     |
| [ Batal ]        [ Mulai ]    |    | Kembalian              Rp22.000   |
+------------------------------+    | [ Batal ]  [ Konfirmasi lunas ]    |
Halaman Update Status:              +----------------------------------+
  Panel kontrol mesin (Set siaga / Set perbaikan, tidak bisa saat mencuci)
  Update status pesanan (tabel antrean + tombol aksi di atas)
```

### 6.7 Owner — Dashboard

```text
+-----------+---------------------------------------------------------------+
| [logo]    | Workspace / Owner                  [Digital Twin • Terhubung]  |
| SMART     | Ringkasan operasional                      [lonceng] (O) Owner v  |
| LAUNDRY   | Bisnis bersih, hasil lebih.            [Minggu, 22 November 2026] |
| SYSTEM    | [Total Pendapatan] [Pesanan Selesai] [Utilisasi Mesin IoT] [Kinerja Petugas] |
| AREA OWNER| Pendapatan harian (7 hari)        | Log MachineHistory            |
| Dashboard | [grafik batang, hari ini kuning]  | Mesin 01 mulai mencuci #WW-0001 |
| Lihat     | Laporan transaksi (4 terbaru)                [ Export Laporan ] |
|  Laporan  | ID Transaksi | Pelanggan | Tanggal | Layanan | Berat | Total | Pembayaran |
| Kelola    | TRX-0001 | Budi | 22 Nov | Reguler | 4 kg | Rp28.000 | Lunas · QRIS |
|  Layanan  +---------------------------------------------------------------+
| Monitoring & Riwayat Mesin | Pantau Kinerja | Manajemen Karyawan            |
+-----------+---------------------------------------------------------------+
```

### 6.8 Monitoring Mesin — Digital Twin

```text
+---------------------------------------------------+
| Monitoring mesin IoT        [● MQTT terhubung]     |
| Digital twin tersinkronisasi dengan kondisi mesin  |
| [Mesin 01 Mencuci]  [Mesin 02 Tersedia]            |
|  Sisa waktu 18:42    Siap beroperasi · 15 kg       |
|  #WW-0001 · Budi     Siap digunakan                |
|  [=======-----]                                    |
| [Mesin 03 Perbaikan] [Mesin 04 Selesai]            |
| Log MachineHistory: "Mesin 04 selesai • #WW-0002"  |
|                                                   |
| Hanya Owner (Monitoring & Riwayat Mesin):          |
|  Konfigurasi unit mesin  [ + Tambah Mesin ]        |
|   Nama | Tipe | Kapasitas | Status | [Edit][Nonaktifkan] |
|  Riwayat & rekap penggunaan                        |
|   Mesin | Siklus selesai | Total waktu pakai | Rata-rata/siklus |
+---------------------------------------------------+
```

### 6.9 Owner — Laporan, Layanan, Kinerja, dan Karyawan

```text
Lihat Laporan:      Laporan transaksi   [7 hari | 30 hari | Semua]  [Export Laporan (CSV)]
                    ID | Pelanggan | Tanggal | Layanan | Berat | Total | Pembayaran
Kelola Layanan:     [ + Tambah Layanan Baru ]   kartu: Reguler / Ekspres / Cuci Basah
                    harga per kg, estimasi, keunggulan, [Edit Harga] [Nonaktifkan]
Pantau Kinerja:     # | Petugas | Shift | Akun | Pesanan diproses | Selesai | Nilai ditangani
Manajemen Karyawan: [ + Tambah Petugas ]   Nama | Email | No. HP | Shift | Status | [Ubah][Nonaktifkan]
                    (petugas nonaktif tidak bisa login; kata sandi baru diisi lewat Ubah)
```

### 6.10 Pengaturan (dibedakan per peran)

```text
+----------------+--------------------------------------------------+
| Profil         |  Profil                                          |
| (tab sesuai    |  (foto)  [Unggah foto] [Hapus foto]              |
|  peran, lihat  |  Nama | Email | No. HP/WhatsApp | Peran (terkunci)|
|  Bagian 4)     |  Alamat (Pelanggan) / Catatan tugas (Petugas) /  |
|                |  Tentang saya (Owner)       [ Simpan profil ]    |
+----------------+--------------------------------------------------+
Pelanggan: Notifikasi (WhatsApp, email), Preferensi (mode gelap, segarkan otomatis,
           metode bayar default), Keamanan (ubah sandi, hak akses).
Petugas:   Tugas & Shift (shift dari Owner, notifikasi pesanan baru, hak akses),
           Preferensi, Keamanan.
Owner:     Info Usaha (nama, WhatsApp, jam operasional, alamat, pintasan kelola,
           unduh/pulihkan cadangan data, reset data), Notifikasi, Preferensi, Keamanan.
```

## 7. Contoh tampilan visual menggunakan Mermaid

> Gambar berikut merupakan **sketsa alur halaman**, bukan screenshot aplikasi.

<img width="923" height="541" alt="alur halaman drawio" src="https://github.com/user-attachments/assets/eda54089-4d2f-487a-a21a-e0b405beb8cf" />

## 8. Kondisi antarmuka (UI States)

| Kondisi | Perilaku UI pada prototipe |
|---|---|
| Loading | Data berasal dari penyimpanan lokal sehingga tampil seketika. Jika nanti memakai backend, gunakan skeleton/spinner dan label "Memuat data…" |
| Data kosong | Judul tebal + penjelasan satu baris, mis. "Belum ada pesanan — Pesanan yang kamu buat akan muncul di sini", "Antrean masih kosong", "Belum ada transaksi", "Belum ada mesin" |
| Login gagal | Kotak merah di atas form: "Email atau kata sandi salah." (tidak membedakan email tak terdaftar dan sandi salah); jenis akun tidak cocok mendapat pesan terpisah setelah sandi benar |
| Terlalu banyak percobaan | Setelah 5 kali gagal: "Terlalu banyak percobaan gagal. Coba lagi dalam beberapa menit." (kunci 5 menit) |
| Validasi form | Kotak merah di dalam form, mis. "Format email belum benar.", "Kata sandi minimal 6 karakter." |
| Gagal menyimpan | Toast/pesan merah dengan penyebab, mis. penyimpanan browser penuh atau diblokir; data lama tidak berubah |
| Berhasil menyimpan | Toast gelap di tengah bawah, mis. "Profil disimpan", "Pesanan terkirim"; tampilan langsung diperbarui |
| Server/penyimpanan bermasalah | Layar "Terjadi kesalahan" + tombol **Muat ulang** dan petunjuk memeriksa penyimpanan browser |
| Data mesin terlambat | Belum ada indikator "Data belum terkonfirmasi" pada prototipe (target: Bagian 9) |
| Pembayaran belum terverifikasi | Badge kuning **Belum bayar**, banner "Menunggu pembayaran QRIS…" dengan tombol *Bayar sekarang*; status Lunas tidak pernah ditampilkan sebelum dikonfirmasi |
| QRIS kedaluwarsa | "QRIS kedaluwarsa" + tombol *Terbitkan ulang QRIS* |
| Akun dinonaktifkan | "Akun dinonaktifkan. Hubungi owner." dan sesi berakhir |
| Akses ditolak | "Aksi tidak diizinkan untuk peran ini."; membuka halaman yang bukan milik perannya dialihkan ke Dashboard |

## 9. Catatan kesesuaian dengan prototipe

Bagian ini mencatat selisih antara prinsip dokumen dan prototipe yang berjalan agar tidak ada klaim yang tidak sesuai.

| Hal | Kondisi prototipe | Tindak lanjut yang disarankan |
|---|---|---|
| Label **SIMULASI** | Belum ada. Aplikasi menampilkan chip "Digital Twin • Terhubung" dan badge "● MQTT terhubung" sebagai elemen tampilan; **tidak ada broker MQTT atau sensor nyata**, timer mesin dihitung di aplikasi | Tambah label SIMULASI, sumber data, dan waktu pembaruan terakhir; ganti teks "MQTT terhubung" bila tidak ada MQTT |
| **Kontras warna** | Teks putih di tombol primer `#4A86F0` = 3,52 : 1; tautan biru `#4A86F0` di putih = 3,52 : 1; teks redup 4,33 : 1; badge kuning 4,14 : 1 (di bawah 4,5 : 1 untuk teks kecil) | Gunakan `--pri-d` `#1F5FC4` (6,01 : 1) untuk tombol/tautan teks kecil atau perbesar/tebalkan teks |
| **Target sentuh** | Tombol standar ± 40 px, tombol kecil ± 30 px | Naikkan menjadi minimal 44 px pada HP |
| **Kode keamanan daftar** Petugas/Owner | Kode dicek di sisi klien dan tertulis di kode sumber | Jangan dipublikasikan di repositori publik; pindahkan ke backend dan gunakan alur undangan dari Owner |
| **Penyimpanan data** | `localStorage` per browser/perangkat, tidak tersinkron antar perangkat; pelanggan di HP berbeda tidak terhubung ke dashboard petugas | Backend + database pada sprint berikutnya |
| **Status pembayaran Gagal** | Belum ada; diwakili QRIS kedaluwarsa | Tambah status Gagal bila ada payment gateway |
| **Diagram gambar** (Bagian 4, 5.1, 5.2, 7) | Gambar draw.io tidak diubah dalam dokumen ini | Periksa warna di diagram; jika masih pastel pink/lavender, ekspor ulang dengan palet Bagian 3.1 |

## 10. Perubahan dari versi sebelumnya

- Tema **Pastel Laundry** (pink, kuning, lavender, mint; latar krem `#FFFBF7`, teks plum `#3F3447`) diganti **Clean Blue Laundry** sesuai prototipe: primer biru `#4A86F0`, latar `#F6F9FE`, teks `#1C2B4A`, plus mode gelap.
- Tipografi, radius, tinggi tombol, gaya kartu (tanpa bayangan), dan breakpoint disesuaikan dengan CSS prototipe.
- Login memakai **email** (bukan username) dengan tab jenis akun, serta alur daftar dengan kode keamanan untuk Petugas/Owner.
- Label status disesuaikan: *Menunggu Antrean, Diproses Mesin, Siap Diambil, Telah Diambil, Dibatalkan*; mesin *Tersedia, Mencuci, Selesai, Perbaikan, Nonaktif*; pembayaran *Belum bayar, Lunas* (QRIS / tunai).
- Sitemap, wireframe, dan alur diperbarui dengan nama menu asli, termasuk Pengaturan per peran, foto profil, Manajemen Karyawan, Pantau Kinerja, Update Status, struk, dan pembayaran QRIS.
- Ditambahkan Bagian 9 (catatan kesesuaian) dan Bagian 10 (daftar perubahan).
