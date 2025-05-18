#  Laporan Proyek Machine Learning: Prediksi Hasil Panen  
**Disusun oleh: Guruh Sukmo**

---

##  Domain Proyek

Proyek ini berfokus pada pengembangan model regresi untuk memprediksi hasil panen berdasarkan data pertanian yang mencakup 22 fitur, termasuk informasi tanah, cuaca, jenis tanaman, dan status penyakit.

Prediksi hasil panen yang akurat sangat penting untuk mendukung pertanian presisi dan membantu petani mengurangi risiko gagal panen.

>  *FAO (2021) mencatat bahwa kerugian hasil panen global akibat faktor lingkungan dan penyakit tanaman bisa mencapai 20–40% tiap tahun.*

**Referensi:**
- Savary, S., et al. *Nature Ecology & Evolution*, 2019
- FAO (2021). (https://www.fao.org](https://www.fao.org/pest-and-pesticide-management/about/understanding-the-context/en/)

---

##  Business Understanding

### Problem Statements
- Bagaimana cara memprediksi hasil panen dari kondisi cuaca, jenis tanah, dan tanaman?
- Algoritma regresi mana yang memberikan prediksi paling akurat?

### Goals
- Mengembangkan model regresi dengan RMSE minimum dan R² maksimum.
- Menentukan model terbaik antara Random Forest dan XGBoost.

### Solution Strategy
- Membangun pipeline preprocessing dan modeling.
- Evaluasi performa menggunakan RMSE dan R² score.
- Hyperparameter tuning dengan `GridSearchCV`.

---

##  Data Understanding

Jumlah data: 500 entri, 22 kolom

Target variabel: yield_kg_per_hectare (float64)

Fitur penting yang tersedia:

Lingkungan: soil_moisture_%, soil_pH, temperature_C, rainfall_mm, humidity_%, sunlight_hours
Agronomi: irrigation_type, fertilizer_type, pesticide_usage_ml
Tanggal tanam dan panen: sowing_date, harvest_date, total_days
Lokasi dan waktu: latitude, longitude, timestamp
Citra dan penyakit: NDVI_index, crop_disease_status


Kemudian dilakukan penghapusan data yang tidak relevan sehingga variabel yang tersisa untuk digunakan adalah: 
`crop_type`, `soil_moisture_%`, `soil_pH`, `temperature_C`, `rainfall_mm`, `sunlight_hours`, `fertilizer_type`, `pesticide_usage_ml`, `crop_disease_status`

`yield_kg_per_hectare` (target)



---

##  Data Preparation

- **Numerik**: Distandarisasi menggunakan `StandardScaler`
- **Kategorikal**: Diolah dengan One-Hot Encoding
- **Split Data**: 70% pelatihan, 30% pengujian
- **Preprocessing** dilakukan menggunakan `ColumnTransformer` dalam pipeline Scikit-learn

---

##  Modeling

### 1. Random Forest Regressor
- N_estimators: 100
- **RMSE (awal)**: 1215.90
- **R² (awal)**: -0.049

### 2. XGBoost Regressor
- N_estimators: 200, learning_rate: 0.05, max_depth: 5
- **RMSE (awal)**: 1282.78
- **R² (awal)**: -0.168

---

##  Hyperparameter Tuning

###  Random Forest
**Best Params:**
{
  'n_estimators': 50,
  'max_depth': 10,
  'min_samples_split': 5,
  'min_samples_leaf': 1
}

###  Hasil Evaluasi Model

**Best RMSE (CV)**: `1176.97`  
**Test RMSE (tuned)**: `1197.89`  
**Test R²**: `-0.019`

---

###  Evaluasi Model

| Model         | RMSE (Test) | R² Score |
|---------------|-------------|----------|
| Random Forest | 1224.72     | -0.065   |
| XGBoost       | 1197.89     | -0.019   |

---

###  Kesimpulan

Meskipun **XGBoost** memiliki RMSE yang sedikit lebih rendah dibandingkan **Random Forest**, **kedua model masih menunjukkan nilai R² negatif**.  
Hal ini mengindikasikan bahwa model belum cukup menjelaskan variabilitas hasil panen yang sebenarnya.

➡ **Diperlukan perbaikan lebih lanjut** baik dari segi data maupun pemilihan/penyesuaian model.

---

### Penutup

Model **Random Forest** dan **XGBoost** berhasil dibangun dan diuji.  
Namun, hasil saat ini **belum optimal**.

Beberapa strategi lanjutan yang dapat diterapkan:

- Menggunakan **dataset yang lebih besar dan lebih representatif**
- Melakukan **feature engineering lanjutan**
- Mengeksplorasi **model alternatif seperti LightGBM atau ensemble stacking**

