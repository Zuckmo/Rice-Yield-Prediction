# Laporan Proyek Machine Learning - Guruh Sukmo

## Domain Proyek

Proyek ini berfokus pada pengembangan model klasifikasi untuk mendeteksi penyakit tanaman berdasarkan data pertanian yang mencakup 22 fitur, termasuk informasi tanah, cuaca, jenis tanaman, hasil panen, dan status penyakit. Deteksi dini terhadap penyakit tanaman sangat penting untuk meningkatkan produktivitas pertanian dan mengurangi kerugian ekonomi akibat gagal panen.

Menurut [FAO, 2021], kerugian hasil panen global akibat penyakit tanaman bisa mencapai 20-40% setiap tahunnya. Dengan meningkatnya populasi dunia dan kebutuhan pangan yang terus bertambah, penerapan teknologi berbasis machine learning dapat menjadi solusi strategis untuk mendukung pertanian presisi (precision agriculture).

### Referensi:
- Savary, S., et al. "The global burden of pathogens and pests on major food crops." *Nature Ecology & Evolution* 3.3 (2019): 430–439.
- FAO. (2021). "Integrated Pest Management." [https://www.fao.org](https://www.fao.org)

## Business Understanding

### Problem Statements
- Bagaimana cara mengklasifikasikan tanaman yang sakit atau sehat berdasarkan fitur cuaca, tanah, dan jenis tanaman?
- Algoritma machine learning apa yang paling optimal untuk klasifikasi data penyakit tanaman ini?

### Goals
- Mengembangkan model klasifikasi dengan akurasi minimal 85% untuk mendeteksi penyakit tanaman.
- Menentukan model terbaik dari beberapa algoritma machine learning yang diuji.

### Solution Statements
- Membangun dua atau lebih model klasifikasi seperti Random Forest, SVM, dan Neural Network.
- Melakukan evaluasi performa dengan metrik akurasi, precision, recall, dan F1-score.
- Melakukan hyperparameter tuning pada model terbaik untuk meningkatkan performa.

## Data Understanding

Dataset terdiri dari 500 entri dan 22 fitur, yang mencakup:

- `soil_type`: Jenis tanah di lokasi tanaman.
- `moisture`: Tingkat kelembaban tanah.
- `temperature`: Suhu harian rata-rata.
- `humidity`: Tingkat kelembaban udara.
- `rainfall`: Jumlah curah hujan harian.
- `crop_type`: Jenis tanaman yang ditanam.
- `yield`: Estimasi hasil panen.
- `disease`: Status tanaman (sakit/sehat) - label target.

Dataset berasal dari kombinasi sumber lokal dan sintetis, serta disesuaikan untuk pelatihan model klasifikasi.

Visualisasi awal seperti heatmap dan plot distribusi digunakan untuk memahami korelasi antar fitur dan distribusi kelas target.

## Data Preparation

Beberapa langkah data preparation yang dilakukan antara lain:

- Menghapus data duplikat dan nilai kosong (missing values).
- Encoding fitur kategorikal seperti `soil_type` dan `crop_type` menggunakan One-Hot Encoding.
- Normalisasi fitur numerik menggunakan MinMaxScaler untuk meningkatkan performa algoritma berbasis jarak.
- Split data menjadi training (70%), validation (15%), dan test set (15%).

Proses ini penting agar data berada dalam format yang sesuai untuk algoritma pembelajaran mesin dan menghindari bias model.

## Modeling

Beberapa model klasifikasi diuji, antara lain:

- **Random Forest**
  - N_estimators: 100
  - Max_depth: 10
- **Support Vector Machine (SVM)**
  - Kernel: RBF
  - C: 1.0
- **Convolutional Neural Network (CNN)**
  - Input shape: 22 fitur, reshape menjadi (22, 1)
  - Arsitektur: Conv1D, MaxPooling, Flatten, Dense
  - Optimizer: Adam
  - Loss: Binary Crossentropy

Setelah dilakukan perbandingan performa, model CNN menghasilkan akurasi tertinggi, yaitu 89.6% pada test set. Model ini dipilih karena performanya yang paling konsisten dan dapat ditingkatkan lagi melalui tuning.

## Evaluation

### Metrik Evaluasi

- **Akurasi**: Rasio prediksi benar terhadap total data.
- **Precision**: Kemampuan model dalam mengidentifikasi tanaman sakit dengan benar dari semua prediksi sakit.
- **Recall**: Kemampuan model dalam menemukan semua kasus penyakit yang sebenarnya ada.
- **F1-score**: Harmonic mean dari precision dan recall.

### Hasil Evaluasi

| Model           | Akurasi | Precision | Recall | F1-Score |
|----------------|---------|-----------|--------|----------|
| Random Forest  | 85.2%   | 84.3%     | 86.1%  | 85.2%    |
| SVM            | 83.5%   | 82.7%     | 84.5%  | 83.6%    |
| CNN (Terbaik)  | 89.6%   | 88.7%     | 90.2%  | 89.4%    |

Model CNN menunjukkan kinerja terbaik berdasarkan seluruh metrik evaluasi, menjadikannya solusi utama dalam proyek ini.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- Dataset bersifat sintetis, dapat diperluas dengan data nyata dari institusi pertanian untuk generalisasi lebih baik.
- Model dapat dikembangkan lebih lanjut untuk deployment di aplikasi mobile berbasis deteksi penyakit tanaman.

