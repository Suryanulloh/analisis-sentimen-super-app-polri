# Analisis Sentimen Ulasan Super App Polri

Perbandingan algoritma Naïve Bayes dan Random Forest untuk klasifikasi sentimen (positif dan negatif) pada ulasan pengguna Super App Polri di Google Play Store. Proyek ini merupakan bagian dari skripsi S1 Sistem Informasi, Universitas Gunadarma (2026).

## Tujuan
Membandingkan performa Naïve Bayes dan Random Forest dalam mengklasifikasikan sentimen ulasan pengguna, serta mengetahui keluhan utama pengguna.

## Data
- 3.000 ulasan terbaru yang dikumpulkan dari Google Play Store dengan google-play-scraper (bahasa Indonesia, periode 16 Juni - 7 Agustus 2026).
- Pelabelan berdasarkan rating: bintang 4-5 = positif, bintang 1-2 = negatif, bintang 3 dibuang (111 ulasan karena ambigu).
- Setelah pelabelan tersisa 2.889 ulasan (81,2% positif, 18,8% negatif). Setelah preprocessing, ulasan yang menjadi kosong dibuang, sehingga 2.556 ulasan dipakai untuk pemodelan.
- Pembagian data 80:20 (stratified): 2.044 data latih dan 512 data uji.

## Metode
1. Preprocessing teks: case folding, cleaning, normalisasi kata tidak baku, tokenisasi, penghapusan stopword, dan stemming (PySastrawi). Kata negasi (tidak, tak, bukan, belum, tanpa, jangan, tiada, kurang) dipertahankan agar konteks sentimen tetap utuh.
2. Ekstraksi fitur: TF-IDF unigram dan bigram (1.346 fitur).
3. Ketidakseimbangan kelas: membandingkan baseline, class weight, dan SMOTE. Class weight dipilih untuk model final.
4. Tuning: GridSearchCV 5-fold. Naïve Bayes alpha = 0,1. Random Forest n_estimators = 200, max_depth = None.
5. Evaluasi: akurasi, presisi, recall, F1-score, confusion matrix, ROC-AUC, 5-fold cross-validation, dan uji McNemar.

## Hasil utama
| Metrik (data uji) | Naïve Bayes | Random Forest |
| --- | --- | --- |
| Akurasi | 90,82% | 92,58% |
| Presisi (tertimbang) | 92,53% | 92,69% |
| Recall (tertimbang) | 90,82% | 92,58% |
| F1-score (tertimbang) | 91,23% | 92,63% |
| Recall kelas negatif | 94% | 84% |
| ROC-AUC | 0,970 | 0,964 |
| Cross-validation 5-fold | 90,22% ± 2,03% | 91,74% ± 1,11% |

- Random Forest lebih stabil terhadap variasi data, sedangkan Naïve Bayes lebih sensitif mendeteksi ulasan negatif.
- Uji McNemar menghasilkan p-value 0,1884 (> 0,05), jadi perbedaan kedua model tidak signifikan secara statistik.
- Sentimen positif dominan. Keluhan utama pengguna berkaitan dengan kendala verifikasi akun, sistem pembayaran, dan pencetakan dokumen.

## Cara menjalankan
1. Buka notebook `Perbandingan_NaiveBayes_vs_RandomForest_.ipynb` di Google Colab.
2. Jalankan sel secara berurutan. Library dipasang pada Tahap 1.
3. Catatan: scraping mengambil ulasan terbaru, jadi hasil bisa sedikit berbeda dari angka di atas.

## Teknologi
- Python, Google Colab
- Pengumpulan data: google-play-scraper
- Pengolahan dan visualisasi: pandas, NumPy, Matplotlib, Seaborn, WordCloud
- Preprocessing teks: NLTK, PySastrawi
- Pemodelan dan evaluasi: scikit-learn (TF-IDF, MultinomialNB, RandomForest, GridSearchCV), imbalanced-learn (SMOTE)
- Uji statistik: statsmodels (McNemar)
- Penyimpanan model: joblib

## Penulis
Ilham Suryanulloh
