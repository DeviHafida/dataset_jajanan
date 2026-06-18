# 🥮 Klasifikasi Jajanan Pasar Tradisional Indonesia menggunakan SVM dan MobileNetV2

Proyek ini merupakan tugas akhir (UAS) untuk mata kuliah Machine & Deep Learning di Program Studi Teknologi Informasi, Universitas Lambung Mangkurat (ULM). Penelitian ini berfokus pada komparasi performa antara metode Machine Learning konvensional (**SVM**) dan Deep Learning (**MobileNetV2**) dalam mengklasifikasikan 6 jenis jajanan pasar tradisional.

---

## 📌 1. Penjelasan Singkat Proyek

Sistem ini dirancang untuk mengenali dan mengklasifikasikan citra 6 jenis jajanan pasar tradisional Indonesia, khususnya kue khas Banjar, Kalimantan Selatan, yaitu:
* **Bingka**
* **Putu Ayu**
* **Cincin**
* **Bakpao**
* **Soes**
* **Amparan Tatak**

### Alur Kerja Sistem:
1. **Pendekatan Machine Learning (SVM):** Citra dikonversi ke format *Grayscale* dan ruang warna *HSV*. Selanjutnya dilakukan ekstraksi fitur tekstur menggunakan **GLCM** (20 fitur) dan fitur warna menggunakan **Color Histogram HSV** (24 fitur). Vektor fitur gabungan (44 fitur) kemudian diklasifikasikan menggunakan algoritma *Support Vector Machine* (SVM).
2. **Pendekatan Deep Learning (MobileNetV2):** Menggunakan teknik *Transfer Learning* dengan memodifikasi *custom fully connected layer* (GAP, Dense 128, Dropout 0.4, Softmax 6). Proses *training* dilakukan dalam dua fase: *Feature Extraction* (mengunci *base layers*) dan dilanjutkan dengan fase *Fine-tuning* pada 5 lapisan terakhir model.

---

## 🛠️ 2. Cara Menjalankan Program

Seluruh kode program eksperimen ini dirancang dan dijalankan di dalam satu *notebook* **Google Colaboratory** yang sama agar proses pelatihan berbasis GPU dapat berjalan optimal.

### Langkah-langkah Eksekusi:
1. **Persiapan Dataset:**
   * Unggah folder dataset berlabel `dataset_balanced` ke dalam Google Drive Anda.
   * Pastikan struktur folder di dalam Drive berbentuk: `/MyDrive/dataset_balanced/{nama_kelas}/*.jpg`.

2. **Menjalankan Eksperimen di Google Colab:**
   * Buka file `.ipynb` proyek ini di Google Colab.
   * Aktifkan runtime GPU (*Runtime > Change runtime type > T4 GPU*).
   * Jalankan *cell* bagian **1. IMPORT LIBRARY** untuk menghubungkan (*mount*) Google Colab dengan Google Drive Anda.
   * Eksekusi seluruh *cell* secara berurutan mulai dari tahap *Configuration*, *Loading Dataset*, *Preprocessing/Augmentasi*, hingga proses *Training* selesai.

3. **Menyimpan Model Hasil Training:**
   * Untuk mengamankan bobot jaringan saraf MobileNetV2 yang telah matang, jalankan *cell* penyimpanan model untuk menghasilkan file `model_mobilenetv2_jajanan.h5`.

---

## 📊 3. Hasil Utama Model

Berdasarkan pengujian menyeluruh menggunakan subset data pengujian (*testing set* yang tidak pernah dilihat model selama training), berikut adalah ringkasan performa akhir kedua metode:

| Metrik Evaluasi | SVM (GLCM + HSV Histogram) | Deep Learning (MobileNetV2) |
| :--- | :---: | :---: |
| **Akurasi Akhir** | **95.00 %** | **100.00 %** |
| **Precision (Macro)** | 95.20 % | 100.00 % |
| **Recall (Macro)** | 95.00 % | 100.00 % |
| **F1-Score (Macro)** | 94.95 % | 100.00 % |

### Kesimpulan Hasil:
* **SVM dengan Fitur GLCM + HSV** memberikan performa yang sangat kompetitif sebesar **95,00%**. Model ini sangat efisien untuk perangkat komputasi rendah, namun memiliki sedikit bias spasial pada kelas objek yang memiliki bentuk geometri serupa (seperti antara bakpao dan soes).
* **MobileNetV2 dengan Transfer Learning** mendominasi secara mutlak dengan raihan akurasi sempurna **100,00%**. Kombinasi *Inverted Residual Blocks* dan strategi *Fine-tuning* terbukti sangat sahih dan presisi dalam mengekstraksi representasi visual tingkat tinggi dari jajanan pasar tradisional tanpa mengalami gejala *overfitting*.

---
💡 *Proyek ini disusun sebagai pemenuhan syarat kelulusan komponen UAS praktikum Machine & Deep Learning.*
