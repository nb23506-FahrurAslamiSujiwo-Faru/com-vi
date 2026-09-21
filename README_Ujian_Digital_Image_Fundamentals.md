# Tugas Praktikum — Digital Image Fundamentals

**Mata Kuliah:** Computer Vision  
**Platform:** Google Colab  
**Materi:** Digital Image Fundamentals, berdasarkan materi slide 1–20  
**Library utama:** Python, OpenCV, NumPy, Matplotlib

## Tujuan
Mahasiswa menerapkan konsep citra digital sebagai matriks, H×W×C, BGR/RGB/HSV/grayscale, ROI, brightness/contrast, histogram, sampling/quantization, resize/interpolation, transformasi, thresholding, dan masking.

## Ketentuan
- Kerjakan menggunakan Google Colab.
- Gunakan **1 foto berwarna milik sendiri/bebas** dengan objek utama yang jelas.
- Jangan menggunakan model AI/ML siap pakai. Fokus ujian adalah operasi citra dasar.
- Setiap soal harus menampilkan **kode, output visual/numerik, dan interpretasi singkat**.
- Parameter seperti ROI, threshold, brightness, contrast, dan HSV boleh disesuaikan dengan gambar.
- Jangan hanya menjalankan kode; mahasiswa harus menjelaskan hasil.

## Soal 1 — Representasi Citra (15 poin)
Upload gambar dan tampilkan gambar dengan warna yang benar. Tampilkan:
1. filename;
2. `shape`;
3. height, width, channel;
4. `dtype`;
5. nilai piksel kiri-atas dan tengah.

**Pertanyaan:** Jelaskan arti `H × W × C` dan mengapa OpenCV menggunakan akses `img[y,x]`.

## Soal 2 — Color Space dan Channel (15 poin)
Konversikan gambar menjadi:
- RGB;
- grayscale;
- HSV.

Pisahkan channel B, G, dan R. Hitung mean intensity masing-masing channel.

**Pertanyaan:** Channel mana yang memiliki mean terbesar? Jelaskan perbedaan fungsi RGB/BGR, grayscale, dan HSV dalam konteks materi.

## Soal 3 — ROI dan Transformasi (15 poin)
Buat ROI yang mengambil objek utama. Kemudian:
- crop ROI;
- flip horizontal;
- rotate 90°;
- tampilkan ukuran sebelum dan sesudah operasi.

**Pertanyaan:** Mengapa ROI berguna dalam sistem Computer Vision?

## Soal 4 — Brightness, Contrast, dan Histogram (20 poin)
Buat tiga versi:
- original;
- lebih gelap;
- lebih terang/lebih kontras.

Tampilkan histogram grayscale ketiganya dan hitung mean intensity.

**Pertanyaan:** Jelaskan hubungan perubahan brightness/contrast dengan distribusi histogram. Sebutkan risiko nilai brightness/contrast yang terlalu tinggi.

## Soal 5 — Sampling, Quantization, dan Resize (15 poin)
Lakukan:
- resize 50% dan 25%;
- resize dengan aspect ratio dipertahankan;
- satu contoh resize yang sengaja merusak aspect ratio;
- quantization grayscale menjadi 8 level dan 4 level.

**Pertanyaan:** Bedakan sampling dan quantization berdasarkan hasil visual.

## Soal 6 — Thresholding/Masking dan Keputusan (20 poin)
Pilih salah satu:
- **A. Grayscale thresholding**, atau
- **B. HSV color masking**.

Hasil wajib:
1. gambar asli;
2. mask;
3. hasil masking;
4. jumlah piksel terseleksi;
5. rasio area terseleksi;
6. keputusan sederhana berdasarkan rasio.

Contoh keputusan: `ratio > 0.30 → area target dominan`.

**Pertanyaan:** Jelaskan mengapa threshold yang Anda pilih sesuai/tidak sesuai dengan kondisi gambar.

---


## Berkas yang Dikumpulkan
- `NIM_Nama_Ujian_DigitalImage.ipynb`
- gambar input yang digunakan
- tului jawaban di bawah cell code menggunakan cell text
