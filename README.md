# Penanganan Missing Value Menggunakan Model Transformer

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Method](https://img.shields.io/badge/Method-Deep%20Learning-blue)
![Framework](https://img.shields.io/badge/Framework-PyTorch-orange)

> **Tugas Besar IF25-32025 Penambangan Data - Kelompok 2**
>
> Repository ini berisi implementasi penelitian kami mengenai penggunaan Deep Learning untuk mengisi data yang hilang (*imputation*) pada dataset transaksi farmasi.

## 👥 Anggota Kelompok
| Nama | NIM |
| :--- | :--- |
| **Muhammad Zahran Albara** | 122140240 |
| **Revolusi A-Ghifari** | 123140199 |
| **Royfran Roger Valentino** | 122140239 |
| **Casey Z.D Manurung** | 122140054 |
| **Pricelia Putri** | 123140075 |
| **Hayyatul Fajri** | 122140103 |

---

## 📖 Tentang Proyek Ini
Masalah utama yang kami angkat adalah **Missing Value** (data yang hilang) pada data tabular. Metode tradisional seperti mengisi dengan rata-rata (*Mean*) atau nilai yang sering muncul (*Mode*) sering kali tidak akurat karena mengabaikan hubungan antar-fitur.

**Solusi Kami:**
Kami membangun model berbasis **Transformer** (arsitektur yang biasa dipakai di ChatGPT/NLP) yang diadaptasi untuk data tabel. Tujuannya adalah agar model bisa "membaca" konteks baris data secara utuh untuk memprediksi nilai yang hilang dengan lebih cerdas, bukan sekadar menebak rata-ratanya.

## 🧠 Mengapa Transformer?
Di proyek ini, kami menggunakan arsitektur **GenericTab Transformer**. Keunggulannya terletak pada mekanisme **Self-Attention**.

* **Cara Kerja Tradisional:** Melihat kolom secara independen (misal: kolom harga dirata-rata).
* **Cara Kerja Transformer:** Menggunakan *Attention* untuk mempelajari konteks global. Model akan melihat hubungan antar kolom dalam satu baris.
    * *Contoh:* Jika `Nama Produk` adalah "Obat A" dan `Unit` adalah "Botol", model akan memprediksi `Harga` yang sesuai dengan konteks tersebut, bukan harga rata-rata semua obat.

## ⚙️ Garis Besar Proses (Workflow)
Berikut adalah tahapan yang kami lakukan dalam penelitian ini:

1.  **Data Preparation:**
    * Menggunakan dataset transaksi farmasi tahun 2021.
    * Memisahkan fitur menjadi tipe Numerik (angka) dan Kategorikal (teks/kode).
2.  **Artificial Masking (Simulasi):**
    * Kami sengaja menghapus 20% data secara acak (*Missing Completely At Random*) untuk membuat skenario pengujian. Hal ini dilakukan agar kami punya "kunci jawaban" (ground truth) untuk mengukur kehebatan model.
3.  **Preprocessing:**
    * *Kategorikal:* Diubah menjadi angka menggunakan Label Encoding.
    * *Numerik:* Diskalakan (Scaling) agar distribusinya stabil.
4.  **Modeling & Training:**
    * Membangun arsitektur Transformer dengan 2 layer encoder dan 4 attention heads.
    * Melatih model selama 30 epochs untuk meminimalisir error prediksi pada bagian data yang hilang.
5.  **Evaluasi:**
    * Membandingkan hasil prediksi Transformer melawan metode standar (Mean Imputation) menggunakan metrik RMSE.

## 📊 Kesimpulan & Hasil
Berdasarkan eksperimen yang dilakukan, pendekatan Deep Learning (Transformer) terbukti jauh lebih efektif dibandingkan metode statistik biasa.

**Highlight Hasil:**
* Model Transformer mampu menurunkan tingkat kesalahan (RMSE) secara signifikan pada semua fitur numerik.
* Peningkatan performa (*Improvement*) rata-rata mencapai **~28.5%** dibandingkan metode Mean Imputation.
* Fitur dengan variansi tinggi seperti `NILAI_KLR` mengalami perbaikan paling besar (**32.1%**), membuktikan model berhasil menangkap pola data yang kompleks.

> **Kesimpulan Akhir:** Penggunaan arsitektur Transformer sangat direkomendasikan untuk menangani missing value pada data transaksi yang kompleks karena mampu menjaga distribusi data asli jauh lebih baik daripada sekadar mengisi dengan nilai rata-rata.

---
*Dibuat untuk Tugas Besar IF25-32025 Penambangan Data - ITERA 2025*
