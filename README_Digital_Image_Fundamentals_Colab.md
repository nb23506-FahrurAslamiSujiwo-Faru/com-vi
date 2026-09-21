# Praktikum Digital Image Fundamentals — Google Colab

**Mata Kuliah:** Computer Vision  
**Materi:** Digital Image Fundamentals (Slide 1–20)  
**Platform:** Google Colab  
**Bahasa:** Python  
**Library:** OpenCV, NumPy, Matplotlib

## Capaian Praktikum

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:

1. Membaca dan menampilkan citra digital.
2. Menjelaskan ukuran citra `H × W × C`, nilai piksel, dan tipe data.
3. Membedakan BGR, RGB, HSV, dan grayscale.
4. Menggunakan ROI/cropping dan transformasi dasar.
5. Mengubah brightness dan contrast serta menganalisis histogram.
6. Memahami efek sampling, quantization, resize, dan interpolation.
7. Melakukan segmentasi warna menggunakan HSV.
8. Melakukan thresholding dan masking.
9. Menghubungkan operasi Image Processing dengan keluaran Computer Vision.

---

# Persiapan Google Colab

Buka Google Colab dan buat notebook baru. Jalankan:

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

print("OpenCV:", cv2.__version__)
```

Upload satu gambar berwarna:

```python
from google.colab import files

uploaded = files.upload()
filename = next(iter(uploaded))
print("File:", filename)
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

## Tujuan

Membuktikan bahwa citra digital merupakan matriks angka dan memahami `height`, `width`, `channel`, koordinat piksel, serta tipe data.

## Eksperimen 1.1 — Membaca citra

```python
img = cv2.imread(filename)

if img is None:
    raise FileNotFoundError("Gambar gagal dibaca")

print("Shape :", img.shape)
print("dtype :", img.dtype)
print("Jumlah elemen:", img.size)

show_bgr(img, "Gambar Asli")
```

### Pertanyaan

- Apa arti output `(H, W, 3)`?
- Mengapa jumlah channel citra berwarna adalah 3?
- Apa tipe data citra yang dibaca?

## Eksperimen 1.2 — Mengakses piksel

```python
h, w = img.shape[:2]

print("Piksel kiri atas :", img[0,0])
print("Piksel tengah    :", img[h//2, w//2])
print("Piksel kanan bawah:", img[h-1,w-1])
```

OpenCV menggunakan urutan:

```text
[B, G, R]
```

Coba ubah sebuah area:

```python
modified = img.copy()
modified[50:150, 50:150] = [0, 255, 0]

show_bgr(modified, "Modifikasi Nilai Piksel")
```

### Analisis

Jelaskan hubungan antara indeks array `img[y,x]` dan lokasi piksel pada citra.

---

# PROJECT 2 — Eksplorasi Color Space

Materi ini menguji RGB/BGR, HSV, grayscale, dan channel warna.

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
```

### Pertanyaan

Mengapa warna gambar kiri dapat terlihat salah?

## Eksperimen 2.2 — RGB, Grayscale, HSV

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
hsv  = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

print("BGR :", img.shape)
print("Gray:", gray.shape)
print("HSV :", hsv.shape)
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
```

## Eksperimen 2.3 — Memisahkan channel

```python
B, G, R = cv2.split(img)

plt.figure(figsize=(15,4))
for i, (channel, title) in enumerate(zip([B,G,R], ["Blue","Green","Red"]), 1):
    plt.subplot(1,3,i)
    plt.imshow(channel, cmap="gray")
    plt.title(title)
    plt.axis("off")

plt.show()
```

### Tugas analisis

Tentukan channel yang memberikan intensitas paling tinggi pada objek dominan di gambar Anda.

---

# PROJECT 3 — ROI dan Transformasi Citra

## Eksperimen 3.1 — Region of Interest

Tentukan area objek secara manual.

```python
h, w = img.shape[:2]

x1, x2 = int(w*0.25), int(w*0.75)
y1, y2 = int(h*0.25), int(h*0.75)

roi = img[y1:y2, x1:x2]

show_bgr(roi, "Region of Interest")
```

Bandingkan:

```python
print("Ukuran asli:", img.shape)
print("Ukuran ROI :", roi.shape)
```

## Eksperimen 3.2 — Flip dan Rotate

```python
flip_horizontal = cv2.flip(img, 1)
rotate90 = cv2.rotate(img, cv2.ROTATE_90_CLOCKWISE)

show_bgr(flip_horizontal, "Horizontal Flip")
show_bgr(rotate90, "Rotate 90°")
```

### Pertanyaan

- Apakah dimensi citra berubah setelah flip?
- Bagaimana `H` dan `W` berubah setelah rotasi 90°?
- Mengapa ROI dapat mempercepat sistem Computer Vision?

---

# PROJECT 4 — Brightness, Contrast, dan Histogram

## Eksperimen 4.1 — Brightness dan contrast

Persamaan:

```text
g(x,y) = α f(x,y) + β
```

`α` mengontrol contrast dan `β` mengontrol brightness.

```python
dark = cv2.convertScaleAbs(img, alpha=1.0, beta=-60)
bright = cv2.convertScaleAbs(img, alpha=1.0, beta=60)
high_contrast = cv2.convertScaleAbs(img, alpha=1.7, beta=0)

show_bgr(dark, "Brightness -60")
show_bgr(img, "Original")
show_bgr(bright, "Brightness +60")
show_bgr(high_contrast, "Contrast 1.7")
```

## Eksperimen 4.2 — Histogram grayscale

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
```

### Analisis

Jelaskan pergeseran histogram ketika citra dibuat lebih gelap dan lebih terang.

### Tantangan

Buat aturan sederhana:

```text
mean intensity < 80   → under-exposed
80–180                → normal
> 180                 → over-exposed
```

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
```

Diskusikan: apakah aturan tersebut selalu dapat dipercaya?

---

# PROJECT 5 — Sampling, Quantization, Resize, dan Interpolation

## Eksperimen 5.1 — Sampling / penurunan resolusi

```python
scales = [1.0, 0.5, 0.25, 0.1]

for scale in scales:
    new_w = max(1, int(w * scale))
    new_h = max(1, int(h * scale))

    temp = cv2.resize(img, (new_w, new_h), interpolation=cv2.INTER_AREA)

    print(scale, temp.shape)
    show_bgr(temp, f"Scale {scale}")
```

### Pertanyaan

Pada skala berapa detail kecil mulai sulit dikenali?

## Eksperimen 5.2 — Menjaga aspect ratio

```python
new_w = 640
new_h = int(h * new_w / w)

correct = cv2.resize(img, (new_w, new_h))
wrong = cv2.resize(img, (640, 640))

show_bgr(correct, "Aspect Ratio Dipertahankan")
show_bgr(wrong, "Dipaksa 640 × 640")
```

Jelaskan perubahan bentuk objek.

## Eksperimen 5.3 — Interpolation

```python
small = cv2.resize(img, None, fx=0.25, fy=0.25,
                   interpolation=cv2.INTER_AREA)

area = cv2.resize(small, (w,h), interpolation=cv2.INTER_AREA)
linear = cv2.resize(small, (w,h), interpolation=cv2.INTER_LINEAR)
cubic = cv2.resize(small, (w,h), interpolation=cv2.INTER_CUBIC)

show_bgr(area, "INTER_AREA")
show_bgr(linear, "INTER_LINEAR")
show_bgr(cubic, "INTER_CUBIC")
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
```

### Analisis

Bandingkan efek pengurangan resolusi spasial dengan pengurangan jumlah level intensitas.

---

# PROJECT 6 — Segmentasi Warna HSV

## Tujuan

Menggunakan warna sebagai informasi untuk memisahkan objek dari background.

Contoh berikut mencari warna merah.

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
```

## Menghitung rasio area merah

```python
red_pixels = cv2.countNonZero(mask_red)
total_pixels = mask_red.size
red_ratio = red_pixels / total_pixels

print("Red pixels :", red_pixels)
print("Total      :", total_pixels)
print("Red ratio  :", round(red_ratio, 4))
```

Buat keputusan:

```python
if red_ratio > 0.15:
    print("Objek/area merah banyak")
else:
    print("Objek/area merah sedikit")
```

### Eksperimen lanjutan

Ubah batas HSV dan catat bagaimana hasil mask berubah.

---

# PROJECT 7 — Thresholding dan Masking

## Eksperimen 7.1 — Global threshold

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
```

Ulangi dengan:

```python
for t in [50, 100, 150, 200]:
    _, mask = cv2.threshold(gray, t, 255, cv2.THRESH_BINARY)

    plt.figure(figsize=(5,4))
    plt.imshow(mask, cmap="gray")
    plt.title(f"Threshold = {t}")
    plt.axis("off")
    plt.show()
```

## Eksperimen 7.2 — Adaptive threshold

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
```

## Eksperimen 7.3 — Masking

```python
selected = cv2.bitwise_and(img, img, mask=mask_global)
show_bgr(selected, "Area yang Dipilih Mask")
```

### Pertanyaan

Bandingkan global dan adaptive threshold. Pada kondisi pencahayaan tidak merata, metode mana yang memberikan pemisahan area lebih baik pada gambar Anda?

---

# FINAL MINI PROJECT — Image Analysis Pipeline

Gabungkan konsep dari slide 1–20 menjadi satu pipeline.

## Skenario

Pilih satu kasus:

- analisis buah berdasarkan warna;
- inspeksi produk sederhana;
- ekstraksi objek berwarna;
- pemisahan foreground/background;
- analisis area tertentu pada benda;
- kasus lain yang disetujui dosen.

## Pipeline wajib

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

Contoh ukuran hasil:

```python
object_pixels = cv2.countNonZero(mask_global)
ratio = object_pixels / mask_global.size

print("Selected area ratio:", ratio)
```

Mahasiswa harus menentukan sendiri aturan keputusan berdasarkan kasus yang dipilih.

---

# Luaran yang Dikumpulkan

Setiap mahasiswa/kelompok mengumpulkan:

1. Notebook Google Colab (`.ipynb`).
2. Gambar input.
3. Screenshot hasil utama.
4. Penjelasan setiap eksperimen.
5. Jawaban pertanyaan analisis.
6. Mini project akhir.
7. Kesimpulan.

Format nama:

```text
NIM_Nama_DigitalImageFundamentals.ipynb
```

---

# Format Laporan Singkat

## 1. Tujuan

Tuliskan tujuan eksperimen.

## 2. Input

Jelaskan gambar yang digunakan, resolusi, channel, dan tipe datanya.

## 3. Metode

Jelaskan operasi OpenCV yang digunakan.

## 4. Hasil

Tampilkan gambar sebelum dan sesudah proses.

## 5. Analisis

Jangan hanya menulis *“program berhasil”*. Jelaskan **mengapa hasil berubah**.

Contoh:

> Setelah brightness ditingkatkan, histogram bergeser ke intensitas yang lebih tinggi. Sebagian piksel mendekati nilai 255 sehingga detail pada daerah terang mulai hilang.

## 6. Kesimpulan

Tuliskan 3–5 poin yang diperoleh dari eksperimen.

---

# Pertanyaan Diskusi Akhir

1. Apa perbedaan output Image Processing dan Computer Vision?
2. Mengapa OpenCV membaca citra dalam format BGR?
3. Apa dampak resolusi terhadap informasi visual dan biaya komputasi?
4. Apa perbedaan sampling dan quantization?
5. Mengapa HSV berguna untuk segmentasi berdasarkan warna?
6. Apa fungsi ROI dalam sistem Computer Vision?
7. Apa hubungan brightness/contrast dengan histogram?
8. Mengapa global threshold dapat gagal ketika pencahayaan tidak merata?
9. Apa dampak resize tanpa mempertahankan aspect ratio?
10. Dari seluruh eksperimen, operasi mana yang termasuk **Image Processing**, dan pada tahap mana hasil mulai menjadi **Computer Vision**?

---

# Catatan untuk Google Colab

Jika runtime di-reset, file hasil upload akan hilang. Upload ulang menggunakan:

```python
from google.colab import files
uploaded = files.upload()
```

Untuk menyimpan hasil:

```python
cv2.imwrite("hasil.jpg", result)
files.download("hasil.jpg")
```

---

## Struktur Praktikum

Praktikum ini sengaja dibagi menjadi beberapa project kecil agar mahasiswa tidak hanya menjalankan satu pipeline panjang. Project 1–3 berfokus pada representasi citra dan transformasi dasar; Project 4 pada pencahayaan dan histogram; Project 5 pada sampling, quantization, resize dan interpolation; Project 6 pada HSV; Project 7 pada thresholding/masking; dan Final Mini Project mengintegrasikan seluruh konsep menjadi sebuah sistem analisis citra sederhana.
