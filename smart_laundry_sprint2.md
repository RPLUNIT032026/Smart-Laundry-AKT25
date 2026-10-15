# Dokumentasi Sprint 2 — Smart Laundry

## 1. Gambaran Umum Sistem

**Smart Laundry** adalah sistem pengelolaan laundry berbasis digital yang membantu pelanggan melihat layanan, membuat pesanan, dan memantau status cucian. Petugas laundry dapat mencatat pesanan, memperbarui proses pencucian, serta mengelola data mesin.

Sistem ini juga dapat menerima informasi status mesin dari simulator atau perangkat IoT, sehingga status operasional lebih mudah dipantau.

## 2. Alur MDA Sederhana

Model-Driven Architecture (MDA) menjelaskan bagaimana rancangan sistem dapat dijadikan dasar untuk mengembangkan aplikasi pada platform berbeda.

```mermaid
flowchart TD
    A["PIM<br/>Model Sistem Smart Laundry"]
    A --> B["Transformasi ke Web"]
    A --> C["Transformasi ke Android"]
    B --> D["PSM Web"]
    C --> E["PSM Android"]
    D --> F["Implementasi Aplikasi Web"]
    E --> G["Implementasi Aplikasi Android"]
    F --> H["Smart Laundry versi Web"]
    G --> I["Smart Laundry versi Android"]

    classDef model fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#111
    classDef result fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#111
    class A,D,E model
    class H,I result
```

PIM (Platform Independent Model) adalah rancangan sistem yang belum terikat pada platform tertentu. PSM (Platform Specific Model) menyesuaikan rancangan tersebut dengan teknologi web atau Android.

**Catatan:** Diagram ini menggambarkan konsep MDA. Pembuatan kode otomatis tetap memerlukan alat transformasi atau generator yang sesuai.

## 3. Context Model — Smart Laundry

Context Model memperlihatkan hubungan sistem Smart Laundry dengan pihak dan layanan yang berinteraksi dengannya.

```mermaid
flowchart TB
    A["Pelanggan"]
    B["Petugas Laundry"]
    C["Mesin Cuci dan Pengering"]
    D["Layanan Notifikasi"]
    E["Database Pesanan"]
    F["Layanan Pembayaran"]
    G["SISTEM SMART LAUNDRY"]

    A --- G
    B --- G
    C --- G
    D --- G
    E --- G
    F --- G

    style G fill:#d9f2ff,stroke:#168aad,stroke-width:3px,color:#111
    style A fill:#fff3e0,stroke:#fb8c00,stroke-width:2px,color:#111
    style B fill:#fff3e0,stroke:#fb8c00,stroke-width:2px,color:#111
    style C fill:#ffffff,stroke:#168aad,stroke-width:2px,color:#111
    style D fill:#ffffff,stroke:#168aad,stroke-width:2px,color:#111
    style E fill:#ffffff,stroke:#168aad,stroke-width:2px,color:#111
    style F fill:#ffffff,stroke:#168aad,stroke-width:2px,color:#111
```

### Keterangan

1. **Pelanggan:** membuat pesanan dan melihat perkembangan cucian.
2. **Petugas Laundry:** mencatat pesanan, mengelola antrean, dan memperbarui status proses.
3. **Mesin Cuci dan Pengering:** menyediakan informasi status mesin, misalnya siaga, beroperasi, atau selesai.
4. **Layanan Notifikasi:** menyampaikan informasi ketika status cucian berubah atau pesanan selesai.
5. **Database Pesanan:** menyimpan data pelanggan, layanan, transaksi, dan status cucian.
6. **Layanan Pembayaran:** mencatat informasi pembayaran pesanan.

## 4. Use Case Diagram

Diagram ini menunjukkan fungsi utama yang digunakan pelanggan dan petugas dalam sistem Smart Laundry.

```mermaid
flowchart LR
    P["Pelanggan"]
    T["Petugas Laundry"]
    M["Mesin Laundry"]

    subgraph SYS["Sistem Smart Laundry"]
        U1(["Lihat layanan dan harga"])
        U2(["Buat pesanan laundry"])
        U3(["Lihat status cucian"])
        U4(["Periksa pembayaran"])
        U5(["Kelola pesanan"])
        U6(["Perbarui status cucian"])
        U7(["Pantau status mesin"])
    end

    P --- U1
    P --- U2
    P --- U3
    P --- U4
    T --- U4
    T --- U5
    T --- U6
    T --- U7
    M --- U7

    classDef actor fill:#fff3e0,stroke:#fb8c00,stroke-width:2px,color:#111
    classDef usecase fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#111
    class P,T,M actor
    class U1,U2,U3,U4,U5,U6,U7 usecase
```

## 5. Deskripsi Use Case

### Use Case: Membuat Pesanan Laundry

| Elemen | Deskripsi |
|---|---|
| Nama use case | Membuat pesanan laundry |
| Aktor utama | Pelanggan |
| Aktor pendukung | Petugas laundry dan layanan pembayaran |
| Tujuan | Pelanggan membuat pesanan sesuai layanan yang tersedia |
| Prasyarat | Layanan laundry dan harga sudah tercatat dalam sistem |
| Pemicu | Pelanggan memilih layanan dan menekan tombol buat pesanan |
| Alur utama | 1. Pelanggan membuka daftar layanan. 2. Pelanggan memilih layanan dan memasukkan informasi cucian. 3. Sistem menghitung perkiraan biaya. 4. Pelanggan memeriksa rincian pesanan. 5. Sistem menyimpan pesanan dan memberikan nomor pesanan. |
| Alur alternatif | Jika informasi pesanan belum lengkap, sistem meminta pelanggan melengkapinya. Jika layanan tidak tersedia, sistem meminta pelanggan memilih layanan lain. |
| Hasil akhir | Pesanan tercatat dan dapat dipantau melalui aplikasi. |
| Aturan | Harga dan status pesanan mengikuti data yang dikelola oleh pihak laundry. |

## 6. Sequence Diagram

### 6.1 Proses Membuat Pesanan

Diagram ini menunjukkan urutan komunikasi saat pelanggan membuat pesanan laundry.

```mermaid
sequenceDiagram
    actor P as Pelanggan
    participant A as Aplikasi Smart Laundry
    participant S as Layanan Pesanan
    participant DB as Database
    participant N as Layanan Notifikasi

    P->>A: Pilih layanan dan isi detail cucian
    A->>S: Kirim data pesanan
    S->>S: Validasi data dan hitung biaya
    S->>DB: Simpan pesanan
    DB-->>S: Konfirmasi penyimpanan
    S-->>A: Kirim nomor dan rincian pesanan
    A-->>P: Tampilkan pesanan berhasil dibuat
    S->>N: Kirim informasi pesanan baru
    N-->>P: Tampilkan konfirmasi pesanan
```

### 6.2 Pemantauan Status Mesin

Diagram ini menunjukkan bagaimana status mesin diperbarui dan ditampilkan kepada petugas.

```mermaid
sequenceDiagram
    participant M as Mesin atau Simulator
    participant S as Layanan Monitoring
    participant DB as Database
    participant A as Dashboard Petugas
    actor T as Petugas

    M->>S: Kirim status mesin
    S->>S: Validasi data status
    S->>DB: Simpan status terbaru
    DB-->>S: Konfirmasi data tersimpan
    S-->>A: Kirim pembaruan status
    A-->>T: Tampilkan status mesin
    alt Mesin mengalami gangguan
        S-->>A: Kirim peringatan gangguan
        A-->>T: Tampilkan notifikasi peringatan
    else Mesin beroperasi normal
        S-->>A: Tampilkan status normal
    end
```

## 7. State Diagram

State Diagram menunjukkan perubahan status suatu objek selama proses berlangsung.

### 7.1 Status Pesanan Laundry

```mermaid
stateDiagram-v2
    direction LR
    state "Menunggu konfirmasi" as Menunggu
    state "Menunggu proses" as Antrean
    state "Sedang dicuci" as Dicuci
    state "Sedang dikeringkan" as Dikeringkan
    state "Siap diambil" as Siap

    [*] --> Menunggu: Pelanggan membuat pesanan
    Menunggu --> Antrean: Pesanan dikonfirmasi
    Menunggu --> Dibatalkan: Pesanan dibatalkan
    Antrean --> Dicuci: Proses pencucian dimulai
    Dicuci --> Dikeringkan: Pencucian selesai
    Dikeringkan --> Siap: Pengeringan dan pemeriksaan selesai
    Siap --> Selesai: Cucian diserahkan kepada pelanggan
    Dibatalkan --> [*]
    Selesai --> [*]
```

| Status | Keterangan |
|---|---|
| Menunggu konfirmasi | Pesanan baru masuk dan menunggu pemeriksaan petugas. |
| Menunggu proses | Pesanan dikonfirmasi dan menunggu giliran pengerjaan. |
| Sedang dicuci | Cucian sedang melalui proses pencucian. |
| Sedang dikeringkan | Cucian berada pada proses pengeringan. |
| Siap diambil | Cucian selesai diproses dan menunggu diambil pelanggan. |
| Selesai | Cucian telah diserahkan kepada pelanggan. |
| Dibatalkan | Pesanan dibatalkan sebelum proses pengerjaan berlangsung. |

### 7.2 Status Mesin Laundry

```mermaid
stateDiagram-v2
    direction LR
    state "Siaga" as Siaga
    state "Beroperasi" as Operasi
    state "Selesai" as Selesai
    state "Gangguan" as Gangguan
    state "Perawatan" as Perawatan

    [*] --> Siaga: Mesin siap digunakan
    Siaga --> Operasi: Siklus laundry dimulai
    Operasi --> Selesai: Siklus selesai
    Selesai --> Siaga: Mesin dikosongkan dan siap kembali
    Siaga --> Gangguan: Gangguan terdeteksi
    Operasi --> Gangguan: Terjadi gangguan saat bekerja
    Gangguan --> Perawatan: Pemeriksaan dimulai
    Perawatan --> Siaga: Mesin dinyatakan normal
```

| Status | Keterangan |
|---|---|
| Siaga | Mesin tersedia dan belum menjalankan siklus. |
| Beroperasi | Mesin sedang menjalankan proses laundry. |
| Selesai | Siklus mesin selesai, tetapi perlu dikosongkan atau diperiksa sebelum digunakan kembali. |
| Gangguan | Sistem mendeteksi masalah sehingga mesin perlu diperiksa. |
| Perawatan | Mesin sedang diperiksa atau diperbaiki oleh petugas. |

## 8. Kesimpulan

Smart Laundry menggabungkan pengelolaan pesanan pelanggan, pemantauan proses cucian, dan pemantauan status mesin. MDA menjelaskan kemungkinan pengembangan rancangan ke platform web dan Android. Context Model memperlihatkan hubungan sistem dengan pihak luar, Use Case menggambarkan fungsi pengguna, Sequence Diagram menunjukkan urutan interaksi, sedangkan State Diagram menjelaskan perubahan status pesanan dan mesin.
