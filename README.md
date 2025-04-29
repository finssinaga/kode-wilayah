# 📍 Kode Wilayah

Struktur kode wilayah Indonesia berdasarkan **Permendagri No. 72 Tahun 2019**.  
Data lengkap dari tingkat provinsi hingga desa, dengan dukungan **foreign key constraints** untuk integritas referensial antar wilayah.

📦 Sumber: [kodewilayah.id](https://kodewilayah.id)

---

## 🗂️ Struktur Tabel

Setiap wilayah menggunakan kode dari wilayah di atasnya sebagai bagian dari **foreign key**.

```
provinsi (kode)
└── kabupaten (kode, kode_provinsi)
    └── kecamatan (kode, kode_kabupaten)
        └── desa (kode, kode_kecamatan)
```

---

## 🗃️ Contoh Struktur SQL

```sql
CREATE TABLE provinsi (
    kode CHAR(2) PRIMARY KEY,
    nama VARCHAR(100) NOT NULL
);

CREATE TABLE kabupaten (
    kode CHAR(4) PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    kode_provinsi CHAR(2),
    FOREIGN KEY (kode_provinsi) REFERENCES provinsi(kode)
);

CREATE TABLE kecamatan (
    kode CHAR(6) PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    kode_kabupaten CHAR(4),
    FOREIGN KEY (kode_kabupaten) REFERENCES kabupaten(kode)
);

CREATE TABLE desa (
    kode CHAR(10) PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    kode_kecamatan CHAR(6),
    FOREIGN KEY (kode_kecamatan) REFERENCES kecamatan(kode)
);
```

---

## 📌 Tujuan

- Menyediakan struktur wilayah Indonesia dalam bentuk database relasional
- Memastikan relasi antar wilayah valid via foreign key

---
