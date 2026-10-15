## 8. Activity Diagram — Proses Pemesanan Smart Laundry

Activity Diagram ini menggambarkan alur aktivitas pelanggan ketika membuat pesanan laundry, mulai dari membuka aplikasi hingga pesanan tersimpan atau proses berakhir karena data tidak valid.

```mermaid
flowchart TD
    A([Mulai]) --> B[Pelanggan membuka aplikasi Smart Laundry]
    B --> C[Pelanggan melihat layanan dan harga]
    C --> D[Pelanggan memilih layanan]
    D --> E[Pelanggan mengisi detail cucian]
    E --> F{Data pesanan lengkap?}

    F -- Tidak --> G[Tampilkan pesan untuk melengkapi data]
    G --> E

    F -- Ya --> H[Sistem menghitung perkiraan biaya]
    H --> I[Pelanggan memeriksa rincian pesanan]
    I --> J{Pelanggan melanjutkan pesanan?}

    J -- Tidak --> K([Pesanan tidak dilanjutkan])
    J -- Ya --> L[Sistem menyimpan pesanan]
    L --> M[Sistem membuat nomor pesanan]
    M --> N[Sistem menampilkan konfirmasi pesanan]
    N --> O([Selesai])

    classDef startEnd fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#111
    classDef process fill:#e1f5fe,stroke:#0288d1,stroke-width:1.5px,color:#111
    classDef decision fill:#fff3e0,stroke:#fb8c00,stroke-width:1.5px,color:#111
    class A,K,O startEnd
    class B,C,D,E,G,H,I,L,M,N process
    class F,J decision
```

### Keterangan Aktivitas

1. **Mulai:** pelanggan membuka aplikasi Smart Laundry.
2. **Memilih layanan:** pelanggan melihat pilihan layanan dan harga, lalu memilih layanan yang dibutuhkan.
3. **Mengisi detail:** pelanggan memasukkan informasi cucian sesuai kebutuhan sistem.
4. **Validasi data:** sistem memeriksa apakah data pesanan sudah lengkap. Jika belum, pelanggan diminta melengkapinya.
5. **Menghitung biaya:** sistem menampilkan perkiraan biaya berdasarkan layanan yang dipilih.
6. **Konfirmasi pelanggan:** pelanggan memeriksa rincian dan menentukan apakah ingin melanjutkan pesanan.
7. **Menyimpan pesanan:** jika pelanggan melanjutkan, sistem menyimpan pesanan dan membuat nomor pesanan.
8. **Selesai:** sistem menampilkan konfirmasi bahwa pesanan berhasil dibuat.

### Tujuan Diagram

Diagram ini membantu menjelaskan urutan aktivitas dalam proses pemesanan Smart Laundry, termasuk keputusan ketika data belum lengkap atau pelanggan tidak melanjutkan pesanan.
