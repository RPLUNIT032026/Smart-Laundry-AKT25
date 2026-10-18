##  State Diagram

State Diagram menunjukkan perubahan status suatu objek selama proses berlangsung.

###  Status Pesanan Laundry

<img width="2849" height="420" alt="smart_laundry_state_diagram" src="https://github.com/user-attachments/assets/8a6136c6-0f8c-4b80-b41f-53f43ff1c754" />

| Status | Keterangan |
|---|---|
| Menunggu konfirmasi | Pesanan baru masuk dan menunggu pemeriksaan petugas. |
| Menunggu proses | Pesanan dikonfirmasi dan menunggu giliran pengerjaan. |
| Sedang dicuci | Cucian sedang melalui proses pencucian. |
| Sedang dikeringkan | Cucian berada pada proses pengeringan. |
| Siap diambil | Cucian selesai diproses dan menunggu diambil pelanggan. |
| Selesai | Cucian telah diserahkan kepada pelanggan. |
| Dibatalkan | Pesanan dibatalkan sebelum proses pengerjaan berlangsung. |

###  Status Mesin Laundry

<img width="1242" height="176" alt="status_mesin_laundry drawio" src="https://github.com/user-attachments/assets/c859826b-cc84-46bb-afc0-fcef1648202f" />


| Status | Keterangan |
|---|---|
| Siaga | Mesin tersedia dan belum menjalankan siklus. |
| Beroperasi | Mesin sedang menjalankan proses laundry. |
| Selesai | Siklus mesin selesai, tetapi perlu dikosongkan atau diperiksa sebelum digunakan kembali. |
| Gangguan | Sistem mendeteksi masalah sehingga mesin perlu diperiksa. |
| Perawatan | Mesin sedang diperiksa atau diperbaiki oleh petugas. |
