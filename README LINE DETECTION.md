
# LINE DETECTION
### Import Library

```bash
import numpy as np 
import cv2 
import matplotlib.pyplot as plt
%matplotlib inline

import skimage
```
- import numpy as np
Numpy adalah pustaka fundamental untuk komputasi ilmiah di Python. Ia menyediakan dukungan untuk array besar multi-dimensi dan berbagai fungsi matematika untuk operasi pada array tersebut. Contoh Penggunaan: Membuat array, melakukan operasi matematika pada array.

- import cv2
Opencv-python adalah pustaka untuk pengolahan citra dan komputer visi. Ia menyediakan alat untuk membaca, menulis, dan memanipulasi gambar dan video. Contoh Penggunaan: Membaca gambar dari file, menerapkan filter, mendeteksi tepi.

- import matplotlib.pyplot as plt
Matplotlib adalah pustaka plotting 2D yang menghasilkan grafik dan visualisasi data. Modul pyplot menyediakan antarmuka seperti MATLAB untuk pembuatan grafik.Contoh Penggunaan: Membuat plot garis, scatter plot, histogram

- %matplotlib inline
Memastikan bahwa grafik yang dihasilkan oleh matplotlib ditampilkan dalam sel notebook dan tidak dalam jendela terpisah.

- import skimage
Menyediakan algoritma untuk transformasi gambar, filtrasi, analisis, dan lebih banyak lagi. Contoh Penggunaan: Segmentasi gambar, transformasi geometris, pengukuran properti gambar.

### Membaca Gambar
```bash
parkir =cv2.imread("ganjil.jpg")
```
cv2.imread() membaca gambar dan mengembalikannya sebagai array NumPy.

### 
``` bash
cv2.imshow("gambar parkir", parkir)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
- cv2.imshow(): Menampilkan gambar dalam jendela baru.
- cv2.waitKey(0): Menunggu penekanan tombol untuk menutup jendela.
- cv2.destroyAllWindows(): Menutup semua jendela yang dibuka oleh OpenCV.

```bash
gray = cv2.cvtColor(parkir, cv2.COLOR_BGR2GRAY)
edges= cv2.Canny(parkir,100,150)
```

- cv2.cvtColor(parkir, cv2.COLOR_BGR2GRAY):
Mengonversi gambar parkir dari format warna BGR (Blue, Green, Red) ke citra skala abu-abu (grayscale). Variabel gray akan menyimpan citra skala abu-abu yang dihasilkan.
- cv2.Canny(parkir, 100, 150):
Menggunakan algoritma Canny untuk mendeteksi tepi pada gambar parkir. Parameter 100 dan 150 adalah nilai threshold yang digunakan untuk deteksi tepi. Variabel edges akan menyimpan citra hasil deteksi tepi.

```bash
fig,axs = plt.subplots(1,2,figsize=(10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap='gray')
ax[0].set_title("Gambar Asli")

ax[1].imshow(edges, cmap='gray')
ax[1].set_title("Gambar yang udah dideteksi")
```
- fig, axs = plt.subplots(1, 2, figsize=(10, 10)): Membuat satu figur (fig) dengan 1 baris (1) dan 2 kolom (2) subplot, dengan ukuran figur figsize=(10, 10) (10 inch x 10 inch).

- ax = axs.ravel(): Mengubah array axs dari subplot menjadi satu dimensi menggunakan ravel(), sehingga ax dapat digunakan untuk mengakses setiap subplot secara terpisah.

- ax[0].imshow(gray, cmap='gray'): Menampilkan citra skala abu-abu (gray) pada subplot pertama (ax[0]) dengan menggunakan colormap gray untuk visualisasi yang lebih baik.

- ax[0].set_title("Gambar Asli"): Memberikan judul "Gambar Asli" pada subplot pertama.

- ax[1].imshow(edges, cmap='gray'): Menampilkan hasil deteksi tepi (edges) pada subplot kedua (ax[1]) dengan menggunakan colormap gray.

- ax[1].set_title("Gambar yang sudah dideteksi"):Memberikan judul "Gambar yang sudah dideteksi" pada subplot kedua.

- plt.show(): Menampilkan seluruh figur beserta subplot yang telah diatur sebelumnya.

```bash
lines = cv2.HoughLinesP(edges, 1, np.pi/180, 100, minLineLength=50, maxLineGap=20)
image_line = parkir.copy()
```
- cv2.HoughLinesP(edges, 1, np.pi/180, 100, minLineLength=50, maxLineGap=20):Menggunakan transformasi Hough probabilistik untuk mendeteksi garis dalam citra yang telah diproses dengan deteksi tepi (edges).

- parameter:
    1. edges: Citra hasil deteksi tepi.
    2. 1: Resolusi rho (jarak dari titik ke garis).
    3. np.pi/180: Resolusi theta (sudut rotasi garis).
    4. 100: Ambang batas untuk mendeteksi  garis. Nilai ini menentukan berapa banyak suara yang diperlukan untuk mengakui garis.
    5. minLineLength: Panjang minimum garis. Garis lebih pendek dari nilai ini akan diabaikan.
    6. maxLineGap: Jarak maksimum antara segmen garis yang dianggap sebagai bagian dari garis tunggal.

```bash
for line in lines:
    x1, y1, x2, y2 = line[0]
    cv2.line(image_line, (x1, y1), (x2, y2), (207,107,169),1)
```
- for line in lines::Loop ini akan mengiterasi melalui setiap garis yang terdeteksi dalam array lines yang dihasilkan oleh cv2.HoughLinesP().

- x1, y1, x2, y2 = line[0]:Memecah setiap garis dalam lines menjadi koordinat titik awal (x1, y1) dan titik akhir (x2, y2).

- cv2.line(image_line, (x1, y1), (x2, y2), (207, 107, 169), 1):Menggambar garis dari (x1, y1) ke (x2, y2) pada citra image_line. Warna garis ditentukan oleh (207, 107, 169) yang mewakili nilai RGB untuk warna ungu. Ketebalan garis ditentukan oleh 1.

```bash
fig,axs = plt.subplots(1,2,figsize=(10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap='gray')
ax[0].set_title("Gambar Asli")

ax[1].imshow(image_line, cmap='gray')
ax[1].set_title("Gambar yang udah dideteksi")
```
- Gambar Pertama (gray): Tetap menampilkan citra skala abu-abu dari gambar asli.

- Gambar Kedua (image_line): Menampilkan gambar asli (parkir) yang telah dimodifikasi dengan menggambar garis-garis yang terdeteksi menggunakan transformasi Hough probabilistik.