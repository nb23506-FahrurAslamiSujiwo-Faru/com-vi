# Quiz Digital Image Fundamentals — Google Colab

**Mata Kuliah:** Computer Vision  
**Materi:** Digital Image Fundamentals  
**Platform:** Google Colab  
**Bahasa:** Python  
**Library:** OpenCV, NumPy, Matplotlib  

# Aturan Pengisian Jawaban

Setiap pertanyaan analisis harus dijawab **di bawah kode pada cell yang sama** menggunakan komentar Python.

Contoh:

```python
print("Shape:", img.shape)

# Jawaban:
# H = ...
# W = ...
# C = ...
# Penjelasan:
# ...
```

Untuk pertanyaan yang tidak membutuhkan kode, tetap tuliskan jawaban dalam komentar:

```python
# Jawaban:
# Menurut saya ...
```

---

# Persiapan Google Colab

Jalankan:

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

print("OpenCV:", cv2.__version__)

# Jawaban:
# Versi OpenCV yang digunakan:
# ...
```

Upload satu gambar berwarna:

```python
from google.colab import files

uploaded = files.upload()
filename = next(iter(uploaded))
print("File:", filename)

# Jawaban:
# Nama file:
# ...
```

Fungsi bantu:

```python
def show_bgr(img, title="Image"):
    rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    plt.figure(figsize=(7,5))
    plt.imshow(rgb)
    plt.title(title)
    plt.axis("off")
    plt.show()
```

---

# PROJECT 1 — Mengenal Citra Digital

## Eksperimen 1.1 — Membaca Citra

```python
img = cv2.imread(filename)

if img is None:
    raise FileNotFoundError("Gambar gagal dibaca")

print("Shape :", img.shape)
print("dtype :", img.dtype)
print("Jumlah elemen:", img.size)

show_bgr(img, "Gambar Asli")

# Jawaban:
# H =
# W =
# C =
# dtype =
# Jumlah elemen =
# Arti output (H, W, 3):
# ...
```

## Eksperimen 1.2 — Mengakses Piksel

```python
h, w = img.shape[:2]

print("Piksel kiri atas :", img[0,0])
print("Piksel tengah    :", img[h//2, w//2])
print("Piksel kanan bawah:", img[h-1,w-1])

# Jawaban:
# Nilai piksel kiri atas =
# Nilai piksel tengah =
# Nilai piksel kanan bawah =
# Urutan nilai warna yang digunakan OpenCV adalah:
# ...
```

Modifikasi area:

```python
modified = img.copy()
modified[50:150, 50:150] = [0, 255, 0]

show_bgr(modified, "Modifikasi Nilai Piksel")

# Jawaban:
# Apa yang terjadi pada area [50:150, 50:150]?
# ...
#
# Jelaskan hubungan img[y,x] dengan posisi piksel:
# ...
```

## Tugas Project 1

Tampilkan nilai piksel pada titik:

- `(10,10)`
- titik tengah
- `(w-10, h-10)`

```python
# Tulis kode Anda di sini


# Jawaban:
# Piksel 1 =
# Piksel 2 =
# Piksel 3 =
```

Buat kotak berwarna biru berukuran `100 × 100` piksel pada bagian tengah gambar.

```python
# Tulis kode Anda di sini


# Jawaban:
# Koordinat area yang diubah:
# ...
# Mengapa nilai BGR untuk biru adalah [255, 0, 0]?
# ...
```

Hitung nilai rata-rata B, G, dan R seluruh citra tanpa menggunakan `cv2.mean()`.

```python
# Tulis kode Anda di sini


# Jawaban:
# Mean B =
# Mean G =
# Mean R =
# Channel dominan =
# ...
```

---

# PROJECT 2 — Eksplorasi Color Space

## Eksperimen 2.1 — BGR vs RGB

```python
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(12,5))

plt.subplot(1,2,1)
plt.imshow(img)
plt.title("BGR ditampilkan langsung")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(img_rgb)
plt.title("BGR → RGB")
plt.axis("off")

plt.show()

# Jawaban:
# Mengapa gambar kiri dapat terlihat memiliki warna yang salah?
# ...
```

## Eksperimen 2.2 — RGB, Grayscale, HSV

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
hsv  = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

print("BGR :", img.shape)
print("Gray:", gray.shape)
print("HSV :", hsv.shape)

# Jawaban:
# Shape BGR =
# Shape Gray =
# Shape HSV =
# Mengapa grayscale hanya memiliki dua dimensi?
# ...
```

```python
plt.figure(figsize=(15,4))

plt.subplot(1,3,1)
plt.imshow(img_rgb)
plt.title("RGB")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(hsv)
plt.title("HSV (raw display)")
plt.axis("off")

plt.show()

# Jawaban:
# Jelaskan perbedaan representasi RGB, grayscale, dan HSV:
# ...
```

## Eksperimen 2.3 — Memisahkan Channel

```python
B, G, R = cv2.split(img)

plt.figure(figsize=(15,4))
for i, (channel, title) in enumerate(zip([B,G,R], ["Blue","Green","Red"]), 1):
    plt.subplot(1,3,i)
    plt.imshow(channel, cmap="gray")
    plt.title(title)
    plt.axis("off")

plt.show()

# Jawaban:
# Channel yang terlihat paling terang pada objek dominan:
# ...
# Alasannya:
# ...
```

## Tugas Project 2

Tampilkan rata-rata intensitas masing-masing channel.

```python
# Tulis kode Anda di sini


# Jawaban:
# Mean Blue =
# Mean Green =
# Mean Red =
```

Buat tiga citra baru:

- hanya channel biru,
- hanya channel hijau,
- hanya channel merah.

```python
# Tulis kode Anda di sini


# Jawaban:
# Channel mana yang paling banyak menyimpan informasi objek?
# ...
```

### HARD

Konversikan citra ke HSV lalu cari nilai rata-rata H, S, dan V.

```python
# Tulis kode Anda di sini


# Jawaban:
# Mean H =
# Mean S =
# Mean V =
#
# Interpretasi:
# ...
```

---

# PROJECT 3 — ROI dan Transformasi Citra

## Eksperimen 3.1 — Region of Interest

```python
h, w = img.shape[:2]

x1, x2 = int(w*0.25), int(w*0.75)
y1, y2 = int(h*0.25), int(h*0.75)

roi = img[y1:y2, x1:x2]

show_bgr(roi, "Region of Interest")

print("Ukuran asli:", img.shape)
print("Ukuran ROI :", roi.shape)

# Jawaban:
# Ukuran asli =
# Ukuran ROI =
# Persentase area yang diambil kira-kira =
# ...
```

## Eksperimen 3.2 — Flip dan Rotate

```python
flip_horizontal = cv2.flip(img, 1)
rotate90 = cv2.rotate(img, cv2.ROTATE_90_CLOCKWISE)

show_bgr(flip_horizontal, "Horizontal Flip")
show_bgr(rotate90, "Rotate 90°")

# Jawaban:
# Apakah dimensi berubah setelah flip?
# ...
# Bagaimana H dan W berubah setelah rotasi 90°?
# ...
```

## Tugas Project 3


Crop bagian tengah citra sebesar 50% dari ukuran asli.

```python
# Tulis kode Anda di sini


# Jawaban:
# Shape hasil crop =
```

Buat hasil transformasi:

- flip horizontal,
- flip vertical,
- rotasi 180°.

```python
# Tulis kode Anda di sini


# Jawaban:
# Operasi mana yang mengubah orientasi paling besar?
# ...
```


Buat ROI berdasarkan input persentase.

Contoh:

```python
percent = 30
```

Program harus mengambil 30% area tengah citra secara otomatis.

```python
# Tulis kode Anda di sini


# Jawaban:
# Persentase ROI =
# Shape ROI =
# Mengapa ROI dapat mempercepat Computer Vision?
# ...
```

---

# PROJECT 4 — Brightness, Contrast, dan Histogram

## Eksperimen 4.1 — Brightness dan Contrast

```python
dark = cv2.convertScaleAbs(img, alpha=1.0, beta=-60)
bright = cv2.convertScaleAbs(img, alpha=1.0, beta=60)
high_contrast = cv2.convertScaleAbs(img, alpha=1.7, beta=0)

show_bgr(dark, "Brightness -60")
show_bgr(img, "Original")
show_bgr(bright, "Brightness +60")
show_bgr(high_contrast, "Contrast 1.7")

# Jawaban:
# Efek beta negatif:
# ...
# Efek beta positif:
# ...
# Efek alpha > 1:
# ...
```

## Eksperimen 4.2 — Histogram

```python
gray_original = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
gray_dark = cv2.cvtColor(dark, cv2.COLOR_BGR2GRAY)
gray_bright = cv2.cvtColor(bright, cv2.COLOR_BGR2GRAY)

plt.figure(figsize=(10,5))

plt.hist(gray_original.ravel(), 256, [0,256], alpha=0.5, label="Original")
plt.hist(gray_dark.ravel(), 256, [0,256], alpha=0.5, label="Dark")
plt.hist(gray_bright.ravel(), 256, [0,256], alpha=0.5, label="Bright")

plt.xlabel("Intensitas")
plt.ylabel("Jumlah Piksel")
plt.legend()
plt.show()

# Jawaban:
# Histogram citra gelap bergeser ke:
# ...
# Histogram citra terang bergeser ke:
# ...
```

## Eksperimen 4.3 — Exposure Classification

```python
mean_intensity = gray_original.mean()

if mean_intensity < 80:
    status = "Under-exposed"
elif mean_intensity > 180:
    status = "Over-exposed"
else:
    status = "Normal"

print("Mean intensity:", mean_intensity)
print("Status:", status)

# Jawaban:
# Mean intensity =
# Status =
# Apakah aturan ini selalu dapat dipercaya?
# ...
```

## Tugas Project 4


Buat citra dengan:

- brightness +30
- brightness -30

```python
# Tulis kode Anda di sini


# Jawaban:
# Mean citra asli =
# Mean brightness +30 =
# Mean brightness -30 =
```

Bandingkan contrast `0.5`, `1.0`, `1.5`, dan `2.0`.

```python
# Tulis kode Anda di sini


# Jawaban:
# Contrast terbaik menurut pengamatan =
# Alasannya =
# ...
```

Buat fungsi otomatis untuk menentukan exposure:

```python
def classify_exposure(gray):
    # lengkapi
    pass
```

Uji pada tiga citra dengan pencahayaan berbeda.

```python
# Jawaban:
# Citra 1 =
# Citra 2 =
# Citra 3 =
#
# Keterbatasan metode mean intensity:
# ...
```

---

# PROJECT 5 — Sampling, Quantization, Resize, dan Interpolation

## Eksperimen 5.1 — Sampling

```python
scales = [1.0, 0.5, 0.25, 0.1]

for scale in scales:
    new_w = max(1, int(w * scale))
    new_h = max(1, int(h * scale))

    temp = cv2.resize(img, (new_w, new_h), interpolation=cv2.INTER_AREA)

    print(scale, temp.shape)
    show_bgr(temp, f"Scale {scale}")

# Jawaban:
# Pada skala berapa detail kecil mulai sulit dikenali?
# ...
```

## Eksperimen 5.2 — Aspect Ratio

```python
new_w = 640
new_h = int(h * new_w / w)

correct = cv2.resize(img, (new_w, new_h))
wrong = cv2.resize(img, (640, 640))

show_bgr(correct, "Aspect Ratio Dipertahankan")
show_bgr(wrong, "Dipaksa 640 × 640")

# Jawaban:
# Apa yang terjadi pada bentuk objek ketika aspect ratio tidak dipertahankan?
# ...
```

## Eksperimen 5.3 — Interpolation

```python
small = cv2.resize(
    img, None,
    fx=0.25, fy=0.25,
    interpolation=cv2.INTER_AREA
)

area = cv2.resize(small, (w,h), interpolation=cv2.INTER_AREA)
linear = cv2.resize(small, (w,h), interpolation=cv2.INTER_LINEAR)
cubic = cv2.resize(small, (w,h), interpolation=cv2.INTER_CUBIC)

show_bgr(area, "INTER_AREA")
show_bgr(linear, "INTER_LINEAR")
show_bgr(cubic, "INTER_CUBIC")

# Jawaban:
# Hasil paling tajam =
# Hasil paling halus =
# ...
```

## Eksperimen 5.4 — Quantization

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

def quantize(gray, levels):
    step = 256 // levels
    q = (gray // step) * step
    return q.astype(np.uint8)

for levels in [256, 32, 8, 4, 2]:
    q = quantize(gray, levels)

    plt.figure(figsize=(5,4))
    plt.imshow(q, cmap="gray", vmin=0, vmax=255)
    plt.title(f"{levels} intensity levels")
    plt.axis("off")
    plt.show()

# Jawaban:
# Pada level berapa gradasi mulai hilang secara jelas?
# ...
```

## Tugas Project 5

Resize citra menjadi 50% dan 25% dari ukuran asli.

```python
# Tulis kode Anda di sini


# Jawaban:
# Shape 50% =
# Shape 25% =
```

Bandingkan interpolation:

- nearest,
- linear,
- cubic.

```python
# Tulis kode Anda di sini


# Jawaban:
# Metode terbaik untuk memperbesar gambar =
# Alasannya =
# ...
```


Hitung pengurangan jumlah piksel antara citra asli dan citra skala 25%.

```python
# Tulis kode Anda di sini


# Jawaban:
# Jumlah piksel asli =
# Jumlah piksel 25% =
# Pengurangan (%) =
# Dampak terhadap biaya komputasi =
# ...
```

---

# PROJECT 6 — Segmentasi Warna HSV

## Eksperimen 6.1 — Segmentasi Warna Merah

```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

lower1 = np.array([0, 80, 70])
upper1 = np.array([10, 255, 255])

lower2 = np.array([170, 80, 70])
upper2 = np.array([180, 255, 255])

mask1 = cv2.inRange(hsv, lower1, upper1)
mask2 = cv2.inRange(hsv, lower2, upper2)

mask_red = cv2.bitwise_or(mask1, mask2)

result = cv2.bitwise_and(img, img, mask=mask_red)

show_bgr(img, "Original")

plt.figure(figsize=(6,4))
plt.imshow(mask_red, cmap="gray")
plt.title("Red Mask")
plt.axis("off")
plt.show()

show_bgr(result, "Red Object")

# Jawaban:
# Area putih pada mask berarti:
# ...
```

## Eksperimen 6.2 — Menghitung Area Warna

```python
red_pixels = cv2.countNonZero(mask_red)
total_pixels = mask_red.size
red_ratio = red_pixels / total_pixels

print("Red pixels :", red_pixels)
print("Total      :", total_pixels)
print("Red ratio  :", round(red_ratio, 4))

# Jawaban:
# Red pixels =
# Total pixels =
# Red ratio =
```

```python
if red_ratio > 0.15:
    print("Objek/area merah banyak")
else:
    print("Objek/area merah sedikit")

# Jawaban:
# Keputusan sistem =
# ...
```

## Tugas Project 6

Ubah segmentasi untuk mencari satu warna lain:

- hijau,
- biru,
- atau kuning.

```python
# Tulis kode Anda di sini


# Jawaban:
# Warna yang dipilih =
# Range HSV =
# ...
```

Hitung persentase warna tersebut terhadap seluruh citra.

```python
# Tulis kode Anda di sini


# Jawaban:
# Jumlah pixel warna target =
# Rasio =
```

Buat sistem sederhana:

```text
Jika rasio warna target > threshold
→ Object Detected
Jika tidak
→ Object Not Detected
```

```python
# Tulis kode Anda di sini


# Jawaban:
# Threshold =
# Hasil keputusan =
# Mengapa threshold tersebut dipilih?
# ...
```

---

# PROJECT 7 — Thresholding dan Masking

## Eksperimen 7.1 — Global Threshold

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

_, mask_global = cv2.threshold(
    gray, 120, 255, cv2.THRESH_BINARY
)

plt.figure(figsize=(6,4))
plt.imshow(mask_global, cmap="gray")
plt.title("Global Threshold = 120")
plt.axis("off")
plt.show()

# Jawaban:
# Piksel dengan intensitas di atas threshold menjadi:
# ...
```

Uji beberapa threshold:

```python
for t in [50, 100, 150, 200]:
    _, mask = cv2.threshold(gray, t, 255, cv2.THRESH_BINARY)

    plt.figure(figsize=(5,4))
    plt.imshow(mask, cmap="gray")
    plt.title(f"Threshold = {t}")
    plt.axis("off")
    plt.show()

# Jawaban:
# Threshold terbaik =
# Alasannya =
# ...
```

## Eksperimen 7.2 — Adaptive Threshold

```python
adaptive = cv2.adaptiveThreshold(
    gray,
    255,
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)

plt.figure(figsize=(6,4))
plt.imshow(adaptive, cmap="gray")
plt.title("Adaptive Threshold")
plt.axis("off")
plt.show()

# Jawaban:
# Perbedaan hasil global dan adaptive threshold:
# ...
```

## Eksperimen 7.3 — Masking

```python
selected = cv2.bitwise_and(img, img, mask=mask_global)
show_bgr(selected, "Area yang Dipilih Mask")

# Jawaban:
# Bagian citra yang dipertahankan adalah:
# ...
```

## Tugas Project 7


Gunakan threshold `100`, `150`, dan `200`.

```python
# Tulis kode Anda di sini


# Jawaban:
# Threshold yang memberikan objek paling jelas =
# ...
```


Bandingkan global threshold dengan adaptive threshold pada area dengan pencahayaan tidak merata.

```python
# Tulis kode Anda di sini


# Jawaban:
# Metode terbaik =
# Alasannya =
# ...
```

Hitung persentase foreground dari hasil threshold.

```python
# Tulis kode Anda di sini


# Jawaban:
# Foreground pixels =
# Total pixels =
# Foreground ratio =
# ...
```

---

# FINAL MINI PROJECT — Image Analysis Pipeline

Pilih salah satu kasus:

- analisis buah berdasarkan warna;
- inspeksi produk sederhana;
- ekstraksi objek berwarna;
- pemisahan foreground/background;
- analisis area tertentu pada benda;
- kasus lain yang relevan.

## Pipeline Wajib

```text
INPUT IMAGE
     ↓
READ & VALIDATE
     ↓
CHECK H × W × C / dtype
     ↓
COLOR CONVERSION
     ↓
ROI
     ↓
RESIZE
     ↓
BRIGHTNESS / CONTRAST ANALYSIS
     ↓
HISTOGRAM
     ↓
HSV / GRAYSCALE
     ↓
THRESHOLD / MASK
     ↓
MEASURE RESULT
     ↓
SIMPLE DECISION
```

---

# FINAL PROJECT - 1

Gunakan satu citra dengan objek berwarna.

Ketentuan:

1. Baca citra.
2. Tampilkan ukuran citra.
3. Konversi ke HSV.
4. Segmentasi satu warna.
5. Hitung rasio warna.
6. Buat keputusan sederhana.

```python
# =====================================
# FINAL PROJECT EASY
# =====================================

# Tulis kode Anda di sini



# Jawaban:
# Kasus yang dipilih:
# ...
#
# Warna target:
# ...
#
# Rasio warna:
# ...
#
# Keputusan sistem:
# ...
#
# Kesimpulan:
# ...
```

---

# FINAL PROJECT - 2

Buat sistem inspeksi sederhana.

Contoh:

```text
Input produk
    ↓
ROI
    ↓
Grayscale / HSV
    ↓
Threshold
    ↓
Hitung foreground
    ↓
Decision
```

Contoh keputusan:

```text
foreground ratio > 0.30
→ PASS

foreground ratio <= 0.30
→ FAIL
```

```python
# =====================================
# FINAL PROJECT INTERMEDIATE
# =====================================

# Tulis kode Anda di sini



# Jawaban:
# Kasus:
# ...
#
# Metode preprocessing:
# ...
#
# Threshold yang digunakan:
# ...
#
# Nilai hasil pengukuran:
# ...
#
# Keputusan:
# ...
#
# Kelebihan metode:
# ...
#
# Keterbatasan:
# ...
```

---

# FINAL PROJECT — 3

Buat pipeline yang mampu membuat keputusan otomatis berdasarkan minimal **dua fitur citra**.

Contoh:

```text
INPUT
 ↓
ROI
 ↓
HSV
 ↓
COLOR MASK
 ↓
GRAYSCALE
 ↓
THRESHOLD
 ↓
FEATURE 1: COLOR RATIO
FEATURE 2: FOREGROUND RATIO
 ↓
DECISION
```

Contoh aturan:

```text
Jika red_ratio > 0.20
dan foreground_ratio > 0.35
    → ACCEPTED

Selain itu
    → REJECTED
```

```python
# =====================================
# FINAL PROJECT HARD
# =====================================

# Tulis kode Anda di sini



# Jawaban:
# Kasus:
# ...
#
# Feature 1:
# ...
#
# Nilai feature 1:
# ...
#
# Feature 2:
# ...
#
# Nilai feature 2:
# ...
#
# Aturan keputusan:
# ...
#
# Output akhir:
# ...
#
# Apakah sistem ini sudah dapat disebut Computer Vision?
# Jelaskan:
# ...
```

---

# Tambahan — BONUS

Gunakan beberapa citra sebagai data pengujian.

Minimal:

```text
5 gambar
```

Program harus memproses seluruh gambar secara otomatis dan menghasilkan:

```text
filename | feature 1 | feature 2 | decision
```

Contoh:

```text
apple01.jpg | 0.38 | 0.42 | ACCEPTED
apple02.jpg | 0.12 | 0.33 | REJECTED
```

```python
# =====================================
# BONUS
# =====================================

# Tulis kode Anda di sini



# Jawaban:
# Jumlah gambar yang diuji:
# ...
#
# Jumlah ACCEPTED:
# ...
#
# Jumlah REJECTED:
# ...
#
# Apakah aturan yang sama cocok untuk semua gambar?
# ...
```

---

# Pertanyaan Diskusi Akhir

Jawab menggunakan satu cell kode:

```python
# 1. Apa perbedaan output Image Processing dan Computer Vision?
# Jawaban:
# ...

# 2. Mengapa OpenCV membaca citra dalam format BGR?
# Jawaban:
# ...

# 3. Apa dampak resolusi terhadap informasi visual dan biaya komputasi?
# Jawaban:
# ...

# 4. Apa perbedaan sampling dan quantization?
# Jawaban:
# ...

# 5. Mengapa HSV berguna untuk segmentasi berdasarkan warna?
# Jawaban:
# ...

# 6. Apa fungsi ROI dalam sistem Computer Vision?
# Jawaban:
# ...

# 7. Apa hubungan brightness/contrast dengan histogram?
# Jawaban:
# ...

# 8. Mengapa global threshold dapat gagal ketika pencahayaan tidak merata?
# Jawaban:
# ...

# 9. Apa dampak resize tanpa mempertahankan aspect ratio?
# Jawaban:
# ...

# 10. Pada tahap mana Image Processing mulai menghasilkan keputusan Computer Vision?
# Jawaban:
# ...
```

---

# Luaran yang Dikumpulkan

Mahasiswa mengumpulkan:

1. Notebook Google Colab (`.ipynb`).
2. Jawaban analisis dalam komentar `# Jawaban:`.


Format nama:

```text
NIM_Nama_DigitalImageFundamentals.ipynb
```

---

