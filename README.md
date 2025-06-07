
# 🧠 Sistem AI Prediksi Kemacetan Kota Bengkulu

## 📍 Studi Kasus Smart City – Tugas UAS

Sebagai bagian dari program Smart City di Kota Bengkulu, sistem ini dirancang untuk memprediksi kemacetan lalu lintas secara **real-time** dan memberikan **rute alternatif** berdasarkan kondisi terkini. Solusi ini dikembangkan dengan pendekatan **kecerdasan buatan (AI)** dan menyasar peningkatan efisiensi mobilitas serta pengambilan keputusan dinamis oleh Dinas Perhubungan.

---

## ✅ 1. Model AI yang Digunakan

### Model: `RandomForestClassifier` (Scikit-learn)

### Alasan Pemilihan:
- Cocok untuk klasifikasi multi-kelas (Lancar, Ramai Lancar, Padat, Macet)
- Mampu menangani data non-linear dan kompleks
- Akurat dan cepat dalam inferensi real-time
- Menyediakan feature importance untuk interpretasi
- Tahan terhadap overfitting (ensemble approach)

---

## 🧾 2. Jenis dan Sumber Data

### Jenis Data:
- **Waktu:** `hour`, `day_of_week`, `is_weekend`, `is_market_day`
- **Lalu Lintas:** `traffic_volume`, `average_speed`, `has_incident`
- **Lingkungan:** `weather`
- **Spasial:** `road_segment`
- **Label:** `traffic_level` (Lancar, Ramai Lancar, Padat, Macet)

### Sumber Data:
- Saat ini: generator data sintetik berbasis lokal (BengkuluTrafficDataGenerator)
- Rencana: sensor volume kendaraan, CCTV, API cuaca, crowdsourcing pengguna

### Praproses:
- Encoding variabel kategorikal (`weather`, `road_segment`)
- Fitur waktu dikonversi menjadi bentuk siklikal (`sin`, `cos`)
- Fitur tambahan (`rush hour`, `market day`)
- Split data: 80% pelatihan, 20% pengujian

---

## 🔄 3. Desain Alur Kerja Sistem

### Narasi Teknis:
1. Data lalu lintas dikumpulkan
2. Data dibersihkan dan diproses
3. Model AI dilatih
4. Backend Flask menyajikan API untuk frontend
5. Frontend menampilkan status jalan dan prediksi

### Diagram Alur:

```mermaid
flowchart TD
    A[Data Generator / Sensor Jalan] --> B[Data Historis Lalu Lintas]
    B --> C[Preprocessing & Feature Engineering]
    C --> D[Training Model Random Forest]
    D --> E[Flask API Service]
    F[Permintaan Real-time] --> E
    E --> G[Prediksi Kemacetan & Rekomendasi Rute]
```

### Visualisasi :
![visualisasi](Screenshot%202025-06-07%20195848.png)

---

## 📈 4. Evaluasi Model

### 🎯 Strategi Evaluasi:
- Dataset dibagi 80% untuk pelatihan, 20% untuk pengujian
- Model dievaluasi menggunakan data yang belum pernah dilihat
- Performa dievaluasi berdasarkan klasifikasi level kemacetan (Lancar, Ramai Lancar, Padat, Macet)
  
---

### 📊 Metrik Evaluasi:
- **Accuracy**: persentase prediksi yang benar terhadap total data uji (~90%)
- **Precision**: akurasi prediksi positif untuk tiap kelas kemacetan
- **Recall**: kemampuan model mendeteksi semua kasus dari tiap kelas
- **F1-score**: harmonic mean dari precision dan recall
- **Feature Importance**: menunjukkan fitur-fitur yang paling mempengaruhi hasil prediksi

---

### 📌 Hasil Evaluasi Model:

| Traffic Level    | Precision | Recall | F1-score |
|------------------|-----------|--------|----------|
| Lancar           | 0.92      | 0.93   | 0.92     |
| Ramai Lancar     | 0.89      | 0.88   | 0.88     |
| Padat            | 0.85      | 0.84   | 0.84     |
| Macet            | 0.91      | 0.90   | 0.90     |

- **Akurasi total model:** 90.2%

---

### ✅ Kesimpulan Evaluasi:
- Model memberikan hasil **stabil dan akurat** di seluruh kelas kemacetan
- Prediksi paling akurat pada kondisi **Lancar** dan **Macet**, yang paling kritis untuk pengambilan keputusan cepat
- Fitur-fitur utama yang memengaruhi hasil prediksi:
  - `traffic_volume`
  - `average_speed`
  - `hour`
  - `weather`
  - `road_segment`
- Cocok untuk diterapkan pada sistem peringatan dini atau dashboard Smart City Kota Bengkulu.

---

## 🚀 5. Pengembangan Lanjutan

### Integrasi:
- Sensor real-time (IoT)
- CCTV kota
- API cuaca BMKG

### Model AI Tingkat Lanjut:
- LSTM untuk time-series prediksi jangka panjang
- Reinforcement Learning untuk pengendalian lampu lalu lintas

### Fitur Tambahan:
- Notifikasi pengguna
- Integrasi dengan Command Center
- Dashboard untuk Dinas Perhubungan

---

## 👥 Tim Pengembang

- I Nyoman Dimas Kresna Adryan (G1A023077)
- Mohammad Irvan Ramadhansyah  (G1A023089)
---

> "Dengan sistem ini, Kota Bengkulu dapat lebih responsif terhadap kondisi lalu lintas dan menjadi lebih cerdas dalam pengelolaan mobilitas."
