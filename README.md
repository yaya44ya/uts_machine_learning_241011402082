# Tugas UTS Machine Learning

Repositori ini berisi pengerjaan Ujian Tengah Semester (UTS) mata kuliah Machine Learning untuk implementasi algoritma Linear Regression dan Logistic Regression secara mandiri menggunakan Python dan NumPy.

---

## Identitas Mahasiswa
- **Nama:** Ahmad Yahya
- **NIM:** 241011402082
- **Kelas:** 05TPLM003
- **Jenis Perkuliahan:** Reguler B
- **Program Studi:** Teknik Informatika (S-1)
- **Random State:** 82 (2 digit terakhir NIM)

---

## Ringkasan Hasil Pengerjaan

### 1. Bagian A — Linear Regression (Dataset: `Ads_Data.csv`)
Tujuan bagian ini adalah memodelkan pengaruh biaya iklan ($X$, dalam juta rupiah) terhadap omset penjualan ($y$, dalam juta rupiah).

- **Persamaan Regresi (Normal Equation):**  
  $$\hat{y} = 27.7772 + 9.1849 \cdot X$$
  - Nilai intercept ($27.78$) artinya estimasi penjualan dasar saat biaya iklan nol adalah sekitar Rp27,78 juta.
  - Koefisien ($9.18$) menandakan setiap penambahan biaya iklan Rp1 juta diperkirakan menaikkan penjualan rata-rata Rp9,18 juta.

- **Tabel Evaluasi Model:**
  | Dataset | MAE (Juta Rp) | MSE | RMSE (Juta Rp) | $R^2$ Score |
  |---|:---:|:---:|:---:|:---:|
  | **Training** | 3.8318 | 22.3475 | 4.7273 | 0.9692 (96.92%) |
  | **Testing** | 7.1269 | 90.9550 | 9.5370 | **0.6618 (66.18%)** |

- **Eksperimen Learning Rate pada Gradient Descent (5000 iterasi):**
  - `lr = 0.001`: Terlalu lambat, belum konvergen setelah 5000 iterasi ($b = 19.9702, m = 10.3553$).
  - `lr = 0.02`: Paling optimal, hasilnya sama persis dengan Normal Equation ($b = 27.7772, m = 9.1849$).
  - `lr = 0.1`: Divergen (gagal konvergen) karena langkah pembaruan terlalu besar sehingga loss mengalami overflow.

- **Hasil Prediksi Kasus Baru:**
  - Iklan Rp4,5 Juta $\rightarrow$ Prediksi Penjualan: **Rp69,11 Juta**
  - Iklan Rp7,0 Juta $\rightarrow$ Prediksi Penjualan: **Rp92,07 Juta**
  - Iklan Rp12,0 Juta $\rightarrow$ Prediksi Penjualan: **Rp138,00 Juta** *(Ekstrapolasi: perlu dicermati karena angka 12 juta berada di luar rentang data historis 0.8–9.9 juta)*.

---

### 2. Bagian B — Logistic Regression (Dataset: `Email_Data.csv`)
Tujuan bagian ini adalah mengklasifikasikan email menjadi Spam (1) atau Bukan Spam (0) berdasarkan jumlah link ($X_1$) dan kata promo ($X_2$).

- **Persamaan Probabilitas:**  
  $$P(\text{Spam}) = \sigma(-12.4712 + 1.0385 \cdot \text{JumlahLink} + 1.0533 \cdot \text{KataPromo})$$

- **Garis Batas Keputusan (*Decision Boundary* pada $P=0.5$):**  
  $$\text{KataPromo} = 11.8398 - 0.9859 \cdot \text{JumlahLink}$$

- **Eksperimen Ambang Batas (*Threshold*):**
  | Threshold | Akurasi | Precision | Recall | F1-Score | Keterangan |
  |:---:|:---:|:---:|:---:|:---:|---|
  | **0.3** | 80.00% | 87.50% | 77.78% | 0.8235 | Lebih longgar (terdapat 1 FP email normal tertandai spam) |
  | **0.5** | 80.00% | 87.50% | 77.78% | 0.8235 | Ambang batas standar |
  | **0.7 (Dipilih)** | **80.00%** | **100.00%** | **66.67%** | **0.8000** | **Terbaik: Presisi 100% (FP = 0), aman dari email penting terbuang** |

- **Prediksi Email Baru (Threshold 0.7):**
  - E1 (1 link, 2 promo) $\rightarrow P(\text{Spam}) = 0.0001 \rightarrow$ **Bukan Spam (0)**
  - E2 (5 link, 6 promo) $\rightarrow P(\text{Spam}) = 0.2771 \rightarrow$ **Bukan Spam (0)**
  - E3 (9 link, 10 promo) $\rightarrow P(\text{Spam}) = 0.9994 \rightarrow$ **Spam (1)**
  - E4 (2 link, 11 promo) $\rightarrow P(\text{Spam}) = 0.7670 \rightarrow$ **Spam (1)**

---

### 3. Bagian C — Pemahaman Konsep
Seluruh 5 pertanyaan konsep pada notebook sudah dijawab lengkap, mencakup alasan penamaan regresi logistik, fungsi sigmoid, perbandingan Normal Equation vs Gradient Descent, penyebab overfitting, perbandingan MSE vs Log Loss, serta pengaruh variasi NIM pada random state.

---

### 4. Bagian Bonus — Perbandingan dengan Scikit-Learn
- Pada Linear Regression, nilai intercept, koefisien, MSE, dan $R^2$ antara implementasi manual dengan scikit-learn menghasilkan angka yang persis sama.
- Pada Logistic Regression, saat regularisasi scikit-learn dinonaktifkan (`penalty=None`), hasil akurasi pada data testing sama persis dengan kode Gradient Descent manual (80.00%).

---

## Berkas dalam Repositori
- `README.md` : Dokumentasi identitas dan ringkasan hasil UTS
- `tugas_UTS.ipynb` : Jupyter Notebook lengkap dengan kode, grafik, dan jawaban analisis
- `Ads_Data.csv` : Dataset untuk Linear Regression
- `Email_Data.csv` : Dataset untuk Logistic Regression
