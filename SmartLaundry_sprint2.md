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
