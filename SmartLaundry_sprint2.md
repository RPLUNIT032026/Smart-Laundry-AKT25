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
