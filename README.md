# CitradigialUTS  
**For the Midterm Exam Assignment**

---

## Review Filter Spasial

Sebelum membahas operasi morfologi, penting untuk memahami konsep **filter spasial**.  
Filter spasial merupakan teknik pengolahan citra yang bekerja langsung pada domain spasial, yaitu dengan memanipulasi nilai-nilai piksel menggunakan masker (*kernel*) yang digeser di seluruh area citra.

### Jenis-jenis Filter Spasial
1. **Filter Linier** — seperti *mean filter* dan *Gaussian filter*, digunakan untuk proses perataan (*smoothing*) dan pengurangan *noise*.  
2. **Filter Non-Linier** — seperti *median filter*, lebih efektif untuk menghilangkan *impulsive noise* (*salt and pepper noise*).

---

### Contoh Penerapan Filter Spasial (Python)

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

img = cv2.imread('contoh_citra.png', 0)

# Filter rata-rata (mean)
mean = cv2.blur(img, (5,5))

# Filter median
median = cv2.medianBlur(img, 5)

# Filter Gaussian
gauss = cv2.GaussianBlur(img, (5,5), 0)

titles = ['Citra Asli', 'Mean Filter', 'Median Filter', 'Gaussian Filter']
images = [img, mean, median, gauss]

for i in range(4):
    plt.subplot(2,2,i+1)
    plt.imshow(images[i], 'gray')
    plt.title(titles[i])
    plt.xticks([]), plt.yticks([])
plt.show()
```
Filter spasial berperan penting dalam tahap pra-pemrosesan citra, karena dapat mengurangi noise dan memperjelas struktur objek sebelum dilakukan operasi morfologi.

Pengantar Operasi Morfologi

Operasi morfologi merupakan teknik pengolahan citra yang berfokus pada bentuk (morphology) dari objek dalam gambar.
Operasi ini bekerja dengan menggunakan structuring element untuk memodifikasi susunan piksel pada citra biner.

Tujuan utamanya adalah:

Memperbaiki struktur objek

Menghilangkan noise

Menyambungkan bagian objek yang terputus

Mengekstraksi fitur tertentu dari gambar

Operasi Morfologi Dasar
a. Erosi (Erosion)

Operasi ini memperkecil ukuran objek dengan mengikis tepiannya.
Dilakukan dengan cara mengubah semua titik batas menjadi titik latar atau menset semua titik di sekeliling titik latar menjadi titik latar.

b. Dilasi (Dilation)

Operasi ini memperbesar ukuran objek dengan menambah lapisan di sekelilingnya.
Setiap titik yang bertetangga dengan titik objek diubah menjadi titik objek.

c. Opening

Merupakan kombinasi erosi diikuti dengan dilasi.
Digunakan untuk menghilangkan objek kecil atau noise dan membuat batas objek lebih halus tanpa mengubah bentuk utamanya.

d. Closing

Merupakan kombinasi dilasi diikuti dengan erosi.
Digunakan untuk menutup lubang kecil pada objek atau menggabungkan objek yang berdekatan.

Contoh Implementasi (Python)
```python
kernel = np.ones((5,5), np.uint8)
erosion = cv2.erode(binary, kernel, iterations=1)
dilation = cv2.dilate(binary, kernel, iterations=1)
opening = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)
closing = cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)
```
Operasi Morfologi Turunan

Selain operasi dasar, terdapat operasi turunan untuk analisis bentuk yang lebih kompleks:

a. Gradient Morfologi

Menunjukkan perbedaan antara hasil dilasi dan erosi.
Digunakan untuk mendeteksi tepi objek.
```python
gradient = cv2.morphologyEx(binary, cv2.MORPH_GRADIENT, kernel)
```
b. Top Hat

Menunjukkan perbedaan antara citra asli dan hasil opening.
Digunakan untuk menyoroti detail kecil yang lebih terang dari latar belakang.
```python
tophat = cv2.morphologyEx(binary, cv2.MORPH_TOPHAT, kernel)
```
c. Black Hat

Menunjukkan perbedaan antara hasil closing dan citra asli.
Digunakan untuk menyoroti area gelap pada latar belakang yang terang.
```python
blackhat = cv2.morphologyEx(binary, cv2.MORPH_BLACKHAT, kernel)
```
Kesimpulan

Operasi morfologi pada citra biner merupakan metode penting dalam pengolahan citra digital untuk menganalisis bentuk dan struktur objek.
Dengan menerapkan kombinasi antara filter spasial dan operasi morfologi dasar maupun turunan, citra dapat diproses menjadi lebih bersih, informatif, dan siap digunakan untuk tahap analisis selanjutnya.

```Install
pip install numpy opencv-python matplotlib
```
