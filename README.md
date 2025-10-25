# CitradigialUTS  
**For the Midterm Exam Assignment**

---

## Review Filter Spasial

Sebelum membahas operasi morfologi, penting untuk memahami konsep **filter spasial**.  
Filter spasial merupakan teknik pengolahan citra yang bekerja langsung pada domain spasial, yaitu dengan memanipulasi nilai-nilai piksel menggunakan masker (kernel) yang digeser di seluruh area citra.

### Jenis-jenis Filter Spasial
1. **Filter Linier** — seperti *mean filter* dan *Gaussian filter*, digunakan untuk proses perataan (*smoothing*) dan pengurangan *noise*.  
2. **Filter Non-Linier** — seperti *median filter*, lebih efektif untuk menghilangkan *impulsive noise* (*salt and pepper noise*).

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
