
# EKTRASI FITUR

### IMPORT LIBRARY
```bash
import cv2 
import matplotlib.pyplot as plt
import numpy as np
import skimage
from skimage.feature import graycomatrix, graycoprops
```
- cv2: Pustaka OpenCV, digunakan untuk pemrosesan gambar komputer seperti membaca, menulis, dan melakukan transformasi.
- matplotlib.pyplot as plt: Digunakan untuk plot dan visualisasi data, termasuk gambar.
- numpy as np: Digunakan untuk operasi matematika dan manipulasi array, sering digunakan dalam konteks pengolahan gambar untuk manipulasi dan analisis data.
- skimage: Modul utama scikit-image untuk pengolahan gambar ilmiah. 
- from skimage.feature import graycomatrix, - graycoprops: Mengimpor fungsi graycomatrix dan graycoprops dari scikit-image. Ini digunakan untuk menghitung matriks ko-occurance abu-abu dan propertinya, yang sering digunakan dalam ekstraksi fitur gambar untuk pengenalan pola dan analisis tekstur.

``` bash
img_hsv = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)

fig, axs = plt.subplots(1, 2, figsize=(10, 10))
ax = axs.ravel()

ax[0].imshow(img)
ax[0].set_title("RGB")


ax[1].imshow(img_hsv)
ax[1].set_title("HSV")

plt.show()
```
- Fungsi cv2.cvtColor() digunakan untuk mengubah citra img dari format warna RGB menjadi format warna HSV. Hasil konversi disimpan dalam variabel img_hsv.
- plt.subplots(1, 2, figsize=(10, 10)): Membuat figur (fig) dengan satu baris (1) dan dua subplot sejajar (2). Ukuran figur ditentukan sebagai 10x10 inch.
- axs.ravel(): Mengubah array dari subplot menjadi satu dimensi agar lebih mudah diakses.
- ax[0].imshow(img): Menampilkan citra asli (RGB) pada subplot pertama (ax[0]) dengan judul "RGB".
- ax[1].imshow(img_hsv): Menampilkan citra yang sudah dikonversi ke HSV pada subplot kedua (ax[1]) dengan judul "HSV".
- plt.show(): Menggambar dan menampilkan seluruh figur dan subplot yang telah disiapkan menggunakan Matplotlib

```bash
mean = np.mean(img_hsv.ravel())  
std = np.std(img_hsv.ravel()) 
print("Rata-rata:", mean)
print("Standar deviasi:", std)
```
- img_hsv.ravel(): Mengubah citra dalam format array satu dimensi agar lebih mudah dihitung rata-rata dan standar deviasinya menggunakan fungsi np.mean() dan np.std() dari NumPy.
- mean: Variabel yang menyimpan nilai rata-rata dari seluruh nilai piksel dalam citra.
- std: Variabel yang menyimpan nilai standar deviasi dari seluruh nilai piksel dalam citra.

Rata-rata (mean): Mencerminkan tingkat kecerahan rata-rata dari citra dalam ruang warna HSV. Informasi ini dapat digunakan untuk normalisasi citra atau untuk analisis yang memerlukan penyesuaian berdasarkan kecerahan relatif.

Standar Deviasi (std): Menunjukkan sebaran atau variasi dari nilai intensitas piksel dalam citra. Hal ini dapat digunakan untuk mengevaluasi seberapa seragam distribusi intensitas piksel dalam citra, atau sebagai faktor dalam deteksi outlier atau noise.

```bash
glcm = graycomatrix(hue, distances=[1], angles=[0], levels=256, symmetric=True, normed=True)
```
- greycomatrix(): Fungsi dari skimage.feature untuk menghitung GLCM dari citra yang diberikan.
- hue: Citra komponen Hue yang telah dipilih.
- distances=[1]: Jarak piksel untuk mencocokkan pasangan piksel.
- angles=[0]: Sudut dalam derajat untuk mencocokkan pasangan piksel.
- levels=256: Jumlah tingkat intensitas piksel dalam citra.
- symmetric=True, normed=True: Parameter untuk mengatur sifat simetri dan normalisasi matriks GLCM.

```bash
contrast = graycoprops(glcm, 'contrast')[0,0]
dissimilarity = graycoprops(glcm, 'dissimilarity')[0,0]
homogeneity = graycoprops(glcm, 'homogeneity')[0,0]
energy = graycoprops(glcm, 'energy')[0,0]
correlation = graycoprops(glcm, 'correlation')[0,0]

print (f'contrast : {contrast}')
print (f'dissimilarity : {dissimilarity}')
print (f'homogeneity : {homogeneity}')
print (f'energy : {energy}')
print (f'correlation : {correlation}')
```
## Manfaat Fitur Tekstur
1. Contrast (Kontras): Mengukur variasi intensitas antara pasangan piksel.
2. Dissimilarity (Dissimilarity): Mengukur seberapa berbeda intensitas antara pasangan piksel.
3. Homogeneity (Homogeneity): Mengukur seberapa seragam distribusi intensitas dalam citra.
4. Energy (Energy): Mengukur "ketajaman" atau kekuatan distribusi intensitas piksel.
5. Correlation (Korelasi): Mengukur hubungan linier antara intensitas piksel dalam pasangan.

    Kemudian mencetak nilai dari setiap fitur tekstur untuk memberikan wawasan tentang karakteristik tekstur dari citra yang dianalisis.
