# CitradigialUTS
For the Midterm Exam Assignment


Review Filter Spasial
Sebelum membahas operasi morfologi, penting untuk memahami konsep filter spasial.
Filter spasial merupakan teknik pengolahan citra yang bekerja langsung pada domain spasial, yaitu dengan memanipulasi nilai-nilai piksel menggunakan masker (kernel) yang digeser di seluruh area citra.

Filter spasial dibagi menjadi dua jenis utama:
Filter Linier, seperti mean filter dan Gaussian filter, digunakan untuk proses perataan (smoothing) dan pengurangan noise.
Filter Non-Linier, seperti median filter, lebih efektif untuk menghilangkan noise impulsif (salt and pepper noise).
Contoh penerapan filter spasial menggunakan Python:

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

Filter spasial berperan penting dalam tahap pra-pemrosesan citra, karena dapat mengurangi noise dan memperjelas struktur objek sebelum dilakukan operasi morfologi.

Pengantar Operasi Morfologi
Operasi morfologi merupakan teknik pengolahan citra yang berfokus pada bentuk (morphology) dari objek dalam gambar.
Operasi ini bekerja dengan menggunakan elemen struktural (structuring element) untuk memodifikasi susunan piksel pada citra biner.

Tujuan utama dari operasi morfologi adalah untuk memperbaiki struktur objek, menghilangkan noise, menyambungkan bagian objek yang terputus, serta mengekstraksi fitur tertentu dari gambar.
Operasi Morfologi Dasar
Empat operasi dasar yang paling umum digunakan dalam morfologi citra adalah sebagai berikut.

a. Erosi (Erosion)
Operasi erosi adalah kebalikan dari operasi dilasi. Pada operasi ini, ukuran objek diperkecil dengan mengikis sekeliling objek. 
Cara yang dapat dilakukan juga ada 2, yaitu 
mengubah semua titik batas menjadi titik latar 
menset semua titik di sekeliling titik latar menjadi titik latar.

b. Dilasi (Dilation)
Operasi dilasi Dilakukan untuk memperbesar ukuran segmen objek dengan menambah lapisan di sekeliling objek. Terdapat 2 cara untuk melakukan operasi ini, yaitu dengan cara mengubah semua titik latar yang bertetangga dengan titik  batas menjadi titik objek, atau lebih mudahnya set setiap titik yang tetangganya adalah titik objek menjadi titik objek. Cara kedua yaitu dengan mengubah semua titik di sekeliling titik batas menjadi titik objek, atau lebih mudahnya set semua titik tetangga sebuah titik objek menjadi titik objek.

c. Opening
Operasi opening  merupakan kombinasi antara operasi erosi dan dilasi yang dilakukan secara berurutan, tetapi citra asli dierosi terlebih dahulu baru kemudian hasilnya didilasi. Operasi ini digunakan untuk memutus bagian-bagian dari objek yang hanya terhubung dengan 1 atau 2 buah titik saja, atau menghilangkan objekobjek kecil dan secara umum men smoothkan batas dari objek besar tanpa mengubah area objek secara signifikan. 

d. Closing
Operasi Closing adalah kombinasi antara operasi dilasi dan erosi yang dilakukan secara berurutan. Citra asli didilasi terlebih dahulu, kemudian hasilnya dierosi. Operasi ini digunakan untuk menutup atau menghilangkan lubang-lubang kecil yang ada dalam segmen objek, menggabungkan objek yang berdekatan dan secara umum men smoothkan batas dari objek besar tanpa mengubah objek secara signifikan

Contoh implementasi dalam Python:
kernel = np.ones((5,5), np.uint8)
erosion = cv2.erode(binary, kernel, iterations=1)
dilation = cv2.dilate(binary, kernel, iterations=1)
opening = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)
closing = cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)


Operasi Morfologi Turunan

Selain operasi dasar, terdapat beberapa operasi morfologi turunan yang memberikan hasil analisis lebih kompleks terhadap bentuk dan struktur objek.

a. Gradient Morfologi
Operasi ini menunjukkan perbedaan antara hasil dilasi dan erosi. Gradient digunakan untuk mendeteksi tepi objek.
gradient = cv2.morphologyEx(binary, cv2.MORPH_GRADIENT, kernel)

b. Top Hat
Menunjukkan perbedaan antara citra asli dan hasil operasi opening. Top Hat digunakan untuk menyoroti detail kecil yang lebih terang dari latar belakang.
tophat = cv2.morphologyEx(binary, cv2.MORPH_TOPHAT, kernel)

c. Black Hat
Menunjukkan perbedaan antara hasil closing dan citra asli. Black Hat digunakan untuk menyoroti area gelap pada latar belakang yang terang.
blackhat = cv2.morphologyEx(binary, cv2.MORPH_BLACKHAT, kernel)

Setiap operasi turunan memiliki fungsi analisis yang spesifik, tergantung pada kebutuhan dan jenis citra yang diolah.



Aplikasi Praktis

Operasi morfologi banyak digunakan di berbagai bidang pengolahan citra digital, antara lain:
Pengolahan Dokumen: Menghapus noise dari hasil pemindaian (scan) dan memperjelas bentuk teks.
Citra Medis: Mengekstraksi bentuk organ tubuh dari hasil MRI atau CT scan.
Visi Komputer (Computer Vision): Melakukan segmentasi objek, pendeteksian tepi, atau pelacakan bentuk pada video.
Industri Manufaktur: Mendeteksi cacat pada permukaan produk atau mengidentifikasi pola pada citra industri.

Contoh aplikasi sederhana: membersihkan noise dari citra hasil scan teks.
img = cv2.imread('teks_noise.png', 0)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)
kernel = np.ones((3,3), np.uint8)
cleaned = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)
cv2.imshow("Hasil Bersih", cleaned)
cv2.waitKey(0)

Setelah operasi dilakukan, teks pada dokumen menjadi lebih jelas dan mudah dibaca.



Kesimpulan
Operasi morfologi pada citra biner merupakan metode penting dalam pengolahan citra digital yang berfungsi untuk menganalisis bentuk dan struktur objek.
Dengan menerapkan kombinasi antara filter spasial dan operasi morfologi dasar maupun turunan, citra dapat diproses menjadi lebih bersih, informatif, dan siap digunakan untuk tahap analisis selanjutnya.



Referensi
Gonzalez, R. C., & Woods, R. E. (2018). Digital Image Processing (4th ed.). Pearson Education.
OpenCV Documentation. https://docs.opencv.org
Susanto, A. (2020). Pengolahan Citra Digital dengan Python dan OpenCV.
