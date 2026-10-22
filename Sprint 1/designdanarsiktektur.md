# Desain dan Arsitektur — Smart Laundry Digital Twin

## 1. Konsep Sistem
Smart Laundry adalah aplikasi web layanan laundry dengan Digital Twin mesin. Pelanggan memesan layanan, petugas memproses cucian, owner memantau operasional, dan simulator/perangkat mengirim status mesin. **Status pesanan berbeda dari status mesin.**

## 2. Arsitektur Logis
```mermaid
flowchart LR
  P[Pelanggan] --> W[Web UI]
  T[Petugas] --> W
  O[Owner] --> W
  W <--> API[Backend API + Otorisasi]
  API <--> DB[(Database)]
  M[Mesin / Simulator] --> ING[Status Ingestion]
  ING --> API
  API --> DT[Representasi Digital Twin]
  DT --> W
```
**Catatan:** diagram ini rancangan, bukan bukti integrasi perangkat nyata.

## 3. Alur Bisnis
```mermaid
flowchart TD
  A[Login atau identifikasi pelanggan] --> B[Buat pesanan]
  B --> C[Pesanan tersimpan]
  C --> D[Catat / konfirmasi pembayaran]
  D --> E[Petugas menerima pesanan]
  E --> F[Tetapkan mesin yang tersedia]
  F --> G[Mesin berjalan dan mengirim status]
  G --> H[Digital Twin dan dashboard diperbarui]
  H --> I[Proses pencucian selesai]
  I --> J[Petugas menuntaskan pesanan]
  J --> K[Pelanggan melihat status akhir]
```
Urutan pembayaran terhadap pencucian harus mengikuti aturan yang ditetapkan kelompok dan transisi State Pesanan Sprint 2.

## 4. Model Data Konseptual
```mermaid
erDiagram
  USERS ||--o{ ORDERS : creates
  ORDERS ||--o{ PAYMENTS : has
  ORDERS }o--o| MACHINES : uses
  MACHINES ||--o{ MACHINE_STATUS_HISTORY : reports
  ORDERS ||--o{ ORDER_STATUS_HISTORY : tracks
  USERS { int id PK string name string role string password_hash }
  ORDERS { int id PK int customer_id FK int machine_id FK string service_type decimal price string status datetime created_at }
  PAYMENTS { int id PK int order_id FK decimal amount string status string method datetime paid_at }
  MACHINES { int id PK string name string status int remaining_minutes datetime updated_at }
  MACHINE_STATUS_HISTORY { int id PK int machine_id FK string status string source datetime recorded_at }
  ORDER_STATUS_HISTORY { int id PK int order_id FK string status datetime recorded_at }
```
**Catatan relasi:** `ORDERS.machine_id` boleh kosong sebelum mesin dialokasikan. Untuk siklus multi-mesin di masa depan, gunakan tabel penugasan terpisah.

## 5. Komponen
- **Frontend:** halaman pelanggan, petugas, owner, dan monitoring.
- **Backend:** autentikasi, pesanan, pembayaran, mesin, riwayat, laporan.
- **Database:** users, orders, payments, machines, riwayat status.
- **Simulator / adapter:** mengirim data status mesin ke backend.
- **Digital Twin service:** memelihara representasi mesin terkini dari update bertimestamp.

## 6. Integritas Status
Pisahkan enumerasi `order_status`, `payment_status`, dan `machine_status`. Nilai akhir harus mengikuti diagram State Sprint 2; jangan menyamakan `Finished` pada pesanan dengan `Available` pada mesin tanpa aturan transisi.

## 7. Keterkaitan UML
Context = aktor dan sistem eksternal; Use Case = kemampuan aktor; Activity = monitoring mesin; Sequence = skenario pelanggan, petugas, owner; State = status pesanan dan mesin; Class = model domain; Component = layanan; Deployment = lokasi runtime.
