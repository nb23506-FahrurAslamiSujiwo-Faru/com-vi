# Proyek Computer Vision — Segmentasi Objek pada Gambar
 
**Bentuk tugas:** Proyek individu  
**Platform:** Google Colab (Python + OpenCV)  
**Materi:** Digital Image Fundamentals; Image Enhancement & Filtering; Edge & Feature Detection

## 1. Tujuan

Mahasiswa membuat program pengolahan citra untuk **memisahkan objek atau wilayah tertentu dari sebuah gambar yang dipilih sendiri**, lalu menjelaskan langkah-langkah yang digunakan dari gambar asli (*raw image*) sampai hasil akhir.

Fokus penilaian adalah **pemahaman proses**, bukan hanya tampilan hasil akhir. Segmentasi yang dimaksud adalah pemisahan area/objek berdasarkan karakteristik citra; mahasiswa **tidak diwajibkan mengenali nama objek secara otomatis**.

## 2. Pemilihan gambar

1. Pilih **satu gambar berwarna (JPG/PNG)** milik sendiri atau dari sumber yang diizinkan untuk penggunaan akademik.
2. Gambar harus memuat **minimal dua objek atau wilayah berbeda** yang akan dicoba dipisahkan, misalnya buah dari latar, daun dari bunga, koin dari meja, kendaraan dari jalan, tulisan dari kertas, atau objek lain pilihan mahasiswa.
3. Pilih gambar dengan tingkat kesulitan **menengah**: objek terlihat jelas, tetapi setidaknya ada tantangan berupa variasi pencahayaan, bayangan, tekstur, atau warna yang agak mirip dengan latar.
4. Cantumkan asal gambar (foto sendiri/tautan sumber) dan jelaskan objek mana yang menjadi target segmentasi.
5. Hindari gambar yang mengandung informasi pribadi orang lain tanpa izin.

> **Catatan:** Setiap gambar memiliki karakteristik berbeda. Mahasiswa boleh memilih metode dan parameter yang paling cocok, tetapi harus menjelaskan alasan pemilihannya. Tidak ada keharusan semua gambar menghasilkan segmentasi sempurna.

## 3. Pekerjaan yang wajib dilakukan

Buat notebook Google Colab dengan urutan tahapan berikut.

| Tahap | Pekerjaan | Output yang harus ditampilkan |
|---|---|---|
| 1. Input & analisis | Membaca gambar, menampilkan ukuran/resolusi, serta membandingkan representasi RGB dan grayscale/HSV. | Gambar asli dan representasi warna yang dipilih |
| 2. Prapemrosesan | Menerapkan **minimal satu** teknik peningkatan kualitas/filtering (misalnya Gaussian, median, bilateral, atau pengaturan kontras). | Gambar sebelum dan sesudah filtering |
| 3. Deteksi tepi | Menerapkan **Sobel atau Canny** untuk melihat batas/struktur objek. | Gambar hasil deteksi tepi |
| 4. Segmentasi | Memisahkan objek/wilayah dengan metode yang sesuai, misalnya thresholding grayscale, threshold HSV, masking, atau kombinasi dengan morfologi dan kontur. | **Mask biner** objek/wilayah target |
| 5. Hasil akhir | Menggunakan mask untuk menampilkan objek yang berhasil dipisahkan dari latar, atau overlay batas/mask pada gambar asli. | **Gambar akhir tersegmentasi**, bukan hanya edge map |
| 6. Evaluasi | Menunjukkan bagian segmentasi yang berhasil dan yang masih keliru serta menjelaskan penyebabnya. | Perbandingan gambar asli, mask, dan hasil akhir |

**Ketentuan penting:**

- Tampilkan output **di setiap tahap**, jangan hanya hasil akhirnya.
- Tambahkan keterangan singkat pada tiap output: **metode, parameter utama, dan alasan penggunaannya**.
- Gunakan sedikitnya **dua variasi parameter** pada salah satu proses (contoh: nilai threshold atau ukuran kernel) lalu bandingkan hasilnya.
- Segmentasi harus benar-benar menghasilkan area objek/wilayah yang terpisah (mask), **bukan hanya recoloring menggunakan K-Means tanpa objek target yang jelas**.
- Program harus dapat dijalankan ulang mulai dari sel pertama; jangan mengandalkan path file lokal pribadi.
- **Tidak menggunakan pretrained AI segmentation/detection** (misalnya YOLO, SAM, Mask R-CNN) untuk menggantikan proses dasar yang sedang diuji.

## 4. Flowchart tulisan tangan (wajib)

Gambar **flowchart proses pengolahan citra dengan tulisan tangan di kertas**, bukan dibuat otomatis oleh program. Flowchart harus sesuai dengan algoritma yang benar-benar diterapkan di notebook, dan sekurang-kurangnya menunjukkan:

**Mulai → Input gambar → Analisis/konversi warna → Filtering → Deteksi tepi → Pembuatan mask → Hasil segmentasi → Evaluasi → Selesai**

Mahasiswa boleh menambahkan percabangan, pengulangan, dan langkah lain sesuai implementasinya. Foto atau pindai flowchart dengan jelas, kemudian masukkan ke notebook serta sertakan sebagai berkas terpisah.

## 5. Video demonstrasi (wajib)

Buat video **4–7 menit** dengan rekaman layar dan penjelasan suara mahasiswa sendiri. Video harus memuat:

1. **Pengenalan (±30 detik):** tunjukkan gambar asli, sumber, objek target, dan tantangan segmentasinya.
2. **Flowchart (±1 menit):** perlihatkan flowchart tulisan tangan dan jelaskan urutan proses serta alasan urutannya.
3. **Demonstrasi program (±2–3 menit):** jalankan/lihatkan bagian penting notebook; jelaskan input, filtering, deteksi tepi, pembuatan mask, dan hasil segmentasi.
4. **Analisis (±1–2 menit):** bandingkan dua parameter, tunjukkan hasil yang berhasil/gagal, serta jelaskan kemungkinan perbaikan.

Video harus memperlihatkan **cara menggunakan program**, bukan sekadar membaca slide atau menampilkan hasil jadi. Kamera wajah **tidak wajib**; suara dan rekaman layar harus jelas.

## 6. Berkas yang dikumpulkan

Kumpulkan dalam satu folder dengan nama `NIM_Nama_ProyekCV`:

```text
NIM_Nama_ProyekCV/
├── Proyek_Segmentasi.ipynb
├── gambar_asli.jpg                 # atau .png
├── hasil_segmentasi.png
├── flowchart_tulisan_tangan.jpg    # atau .pdf
└── link_video.txt                  # berisi tautan video yang dapat diakses dosen
```

Notebook wajib memuat identitas (nama, NIM, kelas), judul proyek, tujuan, gambar asli, kode yang dapat dijalankan, output tiap tahap, serta kesimpulan singkat.

Jika video tidak diunggah sebagai tautan, file MP4 dapat disertakan sesuai ketentuan platform pengumpulan kelas. Pastikan izin akses video benar sebelum mengumpulkan.

## 7. Rubrik penilaian

| Aspek | Bobot |
|---|---:|
| Analisis gambar, konversi warna, dan ketepatan pemilihan input | 10% |
| Filtering dan penjelasan pengaruh parameter | 15% |
| Deteksi tepi dan interpretasinya | 15% |
| Mask dan hasil akhir segmentasi objek/wilayah | 25% |
| Flowchart tulisan tangan yang benar dan sesuai kode | 15% |
| Video: demonstrasi, penjelasan alur, dan analisis hasil | 15% |
| Kerapian notebook, reproducibility, dan kelengkapan pengumpulan | 5% |
| **Total** | **100%** |

> Nilai segmentasi tidak hanya berdasarkan kerapian mask. Penjelasan mengenai keterbatasan, kegagalan, serta alasan pemilihan metode juga diperhitungkan.

## 8. Pertanyaan analisis yang harus dijawab di notebook

1. Mengapa gambar atau objek tersebut dipilih? Apa kesulitan segmentasinya?
2. Mengapa Anda menggunakan ruang warna dan filter tersebut?
3. Apa perbedaan hasil sebelum dan sesudah filtering?
4. Bagaimana hasil deteksi tepi membantu Anda memahami atau memperbaiki segmentasi?
5. Parameter mana yang paling memengaruhi hasil? Tunjukkan bukti perbandingannya.
6. Bagian mana yang belum berhasil disegmentasi dan apa penyebabnya?

## 9. Ketentuan keaslian

- Gambar bebas dipilih, tetapi **kode, percobaan parameter, flowchart, dan penjelasan video** harus dapat dipertanggungjawabkan oleh mahasiswa.
- Boleh mempelajari dokumentasi atau contoh kode dengan mencantumkan sumber; tidak boleh hanya menyerahkan hasil salinan tanpa memahami prosesnya.
- Pada saat penilaian, mahasiswa dapat diminta menjelaskan satu bagian kode atau mengubah satu parameter secara langsung.

**Target akhir:** satu notebook yang menunjukkan alur **raw image → preprocessing → edge detection → mask → segmented output**, disertai flowchart tulisan tangan dan video demonstrasi yang menjelaskan keputusan pada tiap langkah.
