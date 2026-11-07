# Kamus Data: Dataset Analitik Taksi NYC

| Nama Kolom | Tipe Data | Satuan | Sumber Asal | Penanganan Missing Value | Aturan Validitas | Keterangan |
|---|---|---|---|---|---|---|
| `tpep_pickup_datetime` | datetime | Waktu lokal | TLC Parquet | Drop | Sesuai target bulan | Waktu penumpang naik |
| `tpep_dropoff_datetime` | datetime | Waktu lokal | TLC Parquet | Drop | > pickup_datetime | Waktu penumpang turun |
| `passenger_count` | float64 | Orang | TLC Parquet | Isi median per jam | not null | Jumlah penumpang |
| `trip_distance` | float64 | Mil | TLC Parquet | - | 0.01 - 100 mil | Jarak perjalanan |
| `trip_distance_capped` | float64 | Mil | Rekayasa | - | Maksimal P99.5 | Jarak setelah di-winsorize |
| `durasi_menit` | float64 | Menit | Rekayasa | - | 1 - 180 menit | Waktu tempuh |
| `total_amount` | float64 | USD ($) | TLC Parquet | Drop | > 0 | Total tarif |
| `tarif_ekstrem` | int8 | Boolean | Rekayasa | - | 0 atau 1 | Penanda outlier IQR |
| `borough_naik` | string | Kategori | Taxi Zone CSV | Drop | Valid borough | Area penjemputan |
| `payment_type` | int64 | Kategori | TLC Parquet | Drop | 1 s.d. 6 | Kode pembayaran |
| `nama_pembayaran` | string | Kategori | SQLite Latihan| Drop | Ada di tabel dimensi | Label teks pembayaran |
| `suhu_c` | float64 | Celcius | Open-Meteo API| Dibiarkan NaN | - | Suhu saat penjemputan |
| `hujan_mm` | float64 | mm | Open-Meteo API| Dibiarkan NaN | >= 0 | Curah hujan (mm) |
| `hujan` | int8 | Boolean | Rekayasa | 0 (Kering) | 0 atau 1 | 1 jika hujan_mm > 0.1 |
| `tanggal` | string | YYYY-MM-DD| Rekayasa | - | Format ISO valid | Kolom partisi |
| `is_libur` | int8 | Boolean | API Nager.Date| 0 jika tak match | 0 atau 1 | 1 jika libur nasional US |
