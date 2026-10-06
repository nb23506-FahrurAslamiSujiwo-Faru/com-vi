# Praktikum Bab 4 — Ekstraksi Fitur Tingkat Rendah

Materi Computer Vision MKB semester 5. Pendamping presentasi 20 slide Bab 4.

## Berkas

- `Bab4_Latihan_dan_Tugas_Colab.ipynb`: latihan terpandu, kode demo, pertanyaan, tugas, dan rubrik.
- `README_Bab4.md`: panduan penggunaan dan pengumpulan.

## Cara menjalankan di Google Colab

1. Unduh notebook `.ipynb`.
2. Buka https://colab.research.google.com/ lalu pilih **File → Upload notebook**.
3. Unggah notebook dan gunakan runtime Python CPU; GPU tidak diperlukan.
4. Jalankan sel instalasi, impor, dan latihan secara berurutan. Koneksi internet diperlukan saat instalasi paket.
5. Demo memakai citra sintetis sehingga tidak membutuhkan unduhan gambar.
6. Untuk tugas, ubah `RUN_UPLOAD = True` lalu unggah foto sendiri. Jika beberapa foto dipilih, kode membaca foto pertama.
7. Isi identitas dan jawaban pada sel Markdown di bawah kode. Tambahkan sel eksperimen sesuai kebutuhan.
8. Sebelum mengumpulkan, jalankan seluruh sel dari awal. Jika runtime direset, unggah kembali foto sumber.
9. Unduh notebook melalui **File → Download → Download .ipynb** dengan output tetap tersimpan.

## Latihan terpandu

| Latihan | Konsep | Eksperimen |
| --- | --- | --- |
| 1 | Sobel, Gx/Gy, magnitudo | Smoothing dan threshold gradien |
| 2 | Canny, NMS, hysteresis | Perbandingan tiga pasangan threshold |
| 3 | Harris dan maksimum lokal | Ambang respons dan jumlah titik |
| 4 | ORB dan jarak Hamming | Rotasi, skala, dan galat geometris |

Alokasi yang disarankan: 100 menit (persiapan 10, Sobel/Canny 30, Harris 20, ORB 25, diskusi tugas 15). Tugas mandiri diselesaikan di luar sesi; deadline ditetapkan dosen.

## Tugas dan penilaian

Gunakan foto sendiri yang cukup bertekstur. Ikuti rincian eksperimen pada notebook.

| Komponen | Poin | Dasar penilaian |
| --- | ---: | --- |
| A. Perbandingan tepi | 25 | Hasil lengkap, parameter tercatat, pilihan beralasan |
| B. Noise dan Harris | 30 | Kontrol eksperimen, visualisasi, interpretasi |
| C. Matching ORB | 30 | Enam kombinasi, metrik geometris, analisis kegagalan |
| D. Laporan dan reproducibility | 15 | Identitas, sumber foto, kesimpulan, sel dapat dijalankan |
| Total | 100 | |

Persentase piksel tepi dan jumlah match **bukan akurasi**. Untuk transformasi sintetis, gunakan galat posisi terhadap transformasi yang diketahui. Jika tidak ada pasangan, tulis `N/A` untuk statistik matching.

## Pengumpulan

- Notebook `NIM_Nama_Bab4.ipynb` dengan kode, output, tabel eksperimen, dan komentar/analisis di bawah kode.
- Foto sumber yang digunakan.
- Tautan Google Colab dengan akses lihat untuk dosen.
- Kesimpulan 150–250 kata dan sumber citra. Deadline mengikuti instruksi dosen.

## Kendala umum

- `NameError`: jalankan sel impor dan definisi fungsi terlebih dahulu.
- Foto tidak terbaca: unggah JPG/PNG yang valid; hindari HEIC atau konversikan terlebih dahulu.
- Tidak ada keypoint/match: pilih foto bertekstur, periksa ukuran gambar, dan laporkan hasil tanpa mengarang statistik.
- Hasil berbeda: gunakan seed, foto, ukuran, parameter, dan versi OpenCV yang sama.
- Tidak perlu mounting Google Drive. Berkas upload hanya tersedia selama sesi runtime aktif.

## Sumber materi

`bab4-MKB.pdf`, Bab 4 *Low-Level Feature Extraction (including Edge Detection)* dalam *Feature Extraction and Image Processing in Computer Vision*, hlm. 125–184. Fokus praktikum: §4.2.1, §4.4.1.4, dan §4.4.2.3. Kode adalah adaptasi praktikum OpenCV; pembahasan teori lengkap tersedia pada slide.
