# PCD_UTS_202231115_2024_ITPLN
Tri Biakto Rajagukguk
202231115
Pengolahan Citra Digital A

Soal No 1(untitled)
1. Import Library:

import cv2
import matplotlib.pyplot as plt
Di sini, dua library diimpor: OpenCV (cv2) untuk pengolahan gambar dan Matplotlib (matplotlib.pyplot) untuk visualisasi data.

2. Membaca Gambar:

gambar = cv2.imread('tri.jpg')
Gambar dengan nama 'tri.jpg' dibaca menggunakan OpenCV dan disimpan dalam variabel gambar.

3. Konversi Gambar ke Ruang Warna BGR dan RGB:

img_RGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
Gambar diubah ke ruang warna RGB menggunakan OpenCV. Konversi ini diperlukan karena OpenCV menggunakan skema warna BGR secara default, sedangkan Matplotlib menggunakan skema warna RGB.

4. Memisahkan Kanal Warna:

kanal_merah = img_RGB[:,:,0]
kanal_hijau = img_RGB[:,:,1]
kanal_biru = img_RGB[:,:,2]
Kanal warna (merah, hijau, biru) dipisahkan dari gambar RGB untuk analisis lebih lanjut..

5. Menampilkan Gambar Kanal Warna dalam Skala Abu-abu:

plt.figure(figsize=(15, 4))

# Gambar Asli
plt.subplot(1, 4, 1)
plt.imshow(cv2.cvtColor(gambar_RGB, cv2.COLOR_RGB2BGR))
plt.title('Gambar Asli')
plt.axis('off')

# Gambar Kanal Merah
plt.subplot(1, 4, 2)
plt.imshow(kanal_merah, cmap='gray')
plt.title('Kanal Merah')
plt.axis('off')

# Gambar Kanal Hijau
plt.subplot(1, 4, 3)
plt.imshow(kanal_hijau, cmap='gray')
plt.title('Kanal Hijau')
plt.axis('off')

# Gambar Kanal Biru
plt.subplot(1, 4, 4)
plt.imshow(kanal_biru, cmap='gray')
plt.title('Kanal Biru')
plt.axis('off')

plt.tight_layout()
plt.show()
Gambar kanal warna (merah, hijau, biru) ditampilkan dalam subplot dengan skala abu-abu menggunakan Matplotlib.

6. Menghitung Histogram untuk Setiap Kanal Warna:

hist_merah = cv2.calcHist([kanal_merah], [0], None, [256], [0,256])
hist_hijau = cv2.calcHist([kanal_hijau], [0], None, [256], [0,256])
hist_biru = cv2.calcHist([kanal_biru], [0], None, [256], [0,256])
Histogram dihitung untuk setiap kanal warna menggunakan fungsi cv2.calcHist. Ini memberikan informasi tentang distribusi intensitas piksel dalam setiap kanal warna.

7. Menampilkan Histogram:

plt.plot(hist_merah, color='r')
plt.plot(hist_hijau, color='g')
plt.plot(hist_biru, color='b')
plt.title('Histogram Warna Merah, Hijau, dan Biru')
plt.xlabel('Nilai Intensitas')
plt.ylabel('Frekuensi')
plt.show()
Histogram untuk setiap kanal warna (merah, hijau, biru) ditampilkan menggunakan Matplotlib dengan warna yang sesuai. Ini membantu dalam analisis distribusi intensitas piksel dalam gambar.

Soal No 2(Untitled1)
1. Import Library:

import cv2
import numpy as np
import matplotlib.pyplot as plt
Pada langkah ini, library yang diperlukan diimpor. cv2 untuk pengolahan gambar dan visi komputer, numpy untuk manipulasi array, dan matplotlib.pyplot untuk visualisasi data.

2. Membaca Gambar:

gambar = cv2.imread('tri.jpg')
Gambar dengan nama 'tri.jpg' dibaca menggunakan OpenCV (cv2.imread) dan disimpan dalam variabel gambar.

3. KKonversi Gambar ke Ruang Warna HSV:

hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
Gambar yang telah dibaca dikonversi ke ruang warna HSV (Hue, Saturation, Value) menggunakan OpenCV.

4. Definisi Ambang Batas (Rentang) Warna untuk Biru, Merah, dan Hijau:

biru_bawah = np.array([100, 43, 46])
biru_atas = np.array([130, 255, 255])
merah_bawah = np.array([160, 43, 46])
merah_atas = np.array([180, 255, 255])
hijau_bawah = np.array([36, 43, 46])
hijau_atas = np.array([70, 255, 255])
Rentang warna untuk biru, merah, dan hijau didefinisikan dalam format HSV. Nilai-nilai ini menentukan rentang warna yang akan dideteksi.

5. Membuat Masker untuk Setiap Warna:

biru_mask = cv2.inRange(hsv, biru_bawah, biru_atas)
merah_mask = cv2.inRange(hsv, merah_bawah, merah_atas)
hijau_mask = cv2.inRange(hsv, hijau_bawah, hijau_atas)
Masker (binary image) dibuat untuk setiap warna berdasarkan rentang warna yang telah ditentukan.

6. Temukan Piksel yang Cocok dengan Setiap Warna:

biru_piksel = cv2.bitwise_and(img, img, mask=biru_mask)
merah_piksel = cv2.bitwise_and(img, img, mask=merah_mask)
hijau_piksel = cv2.bitwise_and(img, img, mask=hijau_mask)
Piksel yang cocok dengan setiap warna ditentukan dengan menggunakan operasi bitwise AND antara gambar asli dan masker warna.

7. Menampilkan Gambar Asli dan Hasil Deteksi Warna:

plt.figure(figsize=(10, 5))
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(biru_piksel, cv2.COLOR_BGR2RGB))
plt.title('Biru')
plt.axis('off')

plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(merah_piksel, cv2.COLOR_BGR2RGB))
plt.title('Merah')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(hijau_piksel, cv2.COLOR_BGR2RGB))
plt.title('Hijau')
plt.axis('off')

plt.tight_layout()
plt.show()
Gambar asli dan gambar yang telah dideteksi untuk setiap warna (biru, merah, hijau) ditampilkan dalam subplot menggunakan Matplotlib. Gambar disertai dengan judul dan sumbu x dan y dinonaktifkan untuk memperbaiki tampilan.

Teori Yang Mendukung
Berikut adalah teori yang mendukung proyek ini:

Pengolahan Gambar dengan OpenCV: OpenCV (Open Source Computer Vision Library) adalah library populer untuk pemrosesan gambar dan visi komputer. Dengan OpenCV, Anda dapat melakukan berbagai operasi seperti membaca, menulis, dan memanipulasi gambar.

Konversi Ruang Warna: Ruang warna adalah model matematis yang digunakan untuk merepresentasikan warna. Salah satu ruang warna yang umum digunakan adalah RGB (Red, Green, Blue) dan HSV (Hue, Saturation, Value). Konversi ruang warna berguna ketika bekerja dengan beberapa operasi pemrosesan gambar karena beberapa algoritma lebih efektif dalam ruang warna tertentu. Misalnya, deteksi warna sering dilakukan dalam ruang warna HSV karena memisahkan informasi tentang warna (hue), kejenuhan (saturation), dan nilai (value).

Deteksi Warna Menggunakan Ambang Batas: Deteksi warna dilakukan dengan menentukan rentang nilai untuk setiap komponen warna dalam ruang warna yang dipilih. Rentang ini disebut sebagai ambang batas. Ketika sebuah gambar dikonversi ke ruang warna yang tepat, kita dapat menggunakan metode cv2.inRange() untuk membuat sebuah masker (binary image) yang menunjukkan di mana warna yang sesuai muncul dalam gambar.

Operasi Bitwise untuk Pemrosesan Masker: Operasi bitwise dilakukan untuk mengaplikasikan masker pada gambar asli. Ini dilakukan dengan menggunakan operasi bitwise AND antara gambar asli dan masker warna. Hasilnya adalah gambar yang hanya menunjukkan bagian dari gambar asli yang sesuai dengan warna yang dideteksi.

Visualisasi dengan Matplotlib: Matplotlib digunakan untuk visualisasi data, termasuk gambar. Dengan Matplotlib, kita dapat membuat subplot untuk menampilkan gambar asli dan hasil deteksi warna secara bersamaan. Ini memungkinkan untuk perbandingan yang mudah antara gambar asli dan hasil pemrosesan.
