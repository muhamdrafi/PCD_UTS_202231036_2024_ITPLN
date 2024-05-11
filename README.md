# PCD_UTS_202231036_2024_ITPLN

1. Deteksi Warna Pada Citra
   
-import library
```python
import cv2
import matplotlib.pyplot as plt 
import numpy as np
```
Kode tersebut menggunakan OpenCV dan Matplotlib untuk membaca dan menampilkan gambar. Pertama, gambar dibaca menggunakan OpenCV, kemudian ditampilkan menggunakan Matplotlib. Ini dilakukan dengan menggunakan fungsi imread dari OpenCV untuk membaca gambar dan fungsi imshow dari Matplotlib untuk menampilkannya dalam plot.

-Membaca data gambar
```python
img = cv2.imread("fotorafi.jpeg")
```
Kode di atas menggunakan OpenCV untuk membaca gambar yang disebut "fotorafi.jpeg" dan menyimpannya dalam variabel img.

```python
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
Kode tersebut mengonversi gambar dari format warna BGR (Blue-Green-Red) ke format warna RGB (Red-Green-Blue) menggunakan fungsi cvtColor dari OpenCV. Hasil konversi disimpan dalam variabel rgb.

```python
plt.imshow(rgb)
```
Kode itu menggunakan Matplotlib untuk menampilkan gambar yang sudah dikonversi ke format warna RGB dalam plot.

```python
(baris, kolom)= rgb.shape[:2]

beta = 30 #bias untuk kecerahan
citra_cerah = np.zeros((baris, kolom, 3)) #np zeros = mengubah semua elemen array menjadi 0
 
for x in range(baris) :
    for y in range(kolom) :
        gyx = rgb[x,y] + beta
        citra_cerah[x,y] = gyx
citra_cerah = citra_cerah.astype(np.uint8)
 
fig, axs = plt.subplots(2,2, figsize=(15,5))
axs[0,0].imshow(rgb)
axs[0,1].hist(img.ravel(),256,[0,256])
axs[1,0].imshow(citra_cerah)
axs[1,1].hist(citra_cerah.ravel(),256,[0,256])
plt.show()
```
Codingan di atas bertujuan untuk meningkatkan kecerahan citra dengan menambahkan nilai ke setiap piksel citra. Pertama, ukuran citra (jumlah baris dan kolom) diambil menggunakan .shape, dan kemudian sebuah citra nol dengan ukuran yang sama dengan citra asli dibuat menggunakan np.zeros. Selanjutnya, dilakukan iterasi melalui setiap piksel dalam citra asli, di mana nilai kecerahan (intensitas) ditambahkan dengan nilai beta. Hasilnya adalah citra yang lebih cerah. Setelah itu, kedua citra, baik citra asli maupun citra yang telah ditingkatkan kecerahannya, ditampilkan dalam subplot pertama dan kedua, sementara subplot ketiga dan keempat menampilkan histogram dari masing-masing citra untuk menganalisis distribusi intensitas piksel.

```python
# 2. Convert to Grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# 3. Adjust Contrast and Brightness
alpha = 1.5  # kontras
beta = 30    # kecerahan
adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta)

# 4. Display Results
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.title('Original Image')
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.subplot(1, 2, 2)
plt.title('Brightened Image')
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.show()
```
Kode tersebut melakukan beberapa operasi pada gambar. Pertama, gambar dikonversi menjadi citra grayscale menggunakan fungsi cvtColor dari OpenCV. Selanjutnya, kontras dan kecerahan disesuaikan menggunakan fungsi convertScaleAbs dari OpenCV dengan parameter kontras alpha set ke 1.5 dan kecerahan beta set ke 30. Hasil dari penyesuaian tersebut ditampilkan dalam plot menggunakan Matplotlib dalam sebuah subplot, dimana subplot pertama menampilkan gambar asli dalam format RGB, sedangkan subplot kedua menampilkan gambar yang telah disesuaikan kecerahan dalam format RGB. Setelah itu, plot ditampilkan menggunakan plt.show().

Setelah itu gunakan perintah ini untuk mendeteksi warna merah, hijau, dan biru pada gambar:
```python
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.title('Original Image')

# Display the red channel
plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray")
plt.title('Red')

# Display the green channel
plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1], cmap="gray")
plt.title('Green')

# Display the blue channel
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2], cmap="gray")
plt.title('Blue')

plt.show()
```
Kode di atas menggunakan Matplotlib untuk membagi plot menjadi empat subplot. Subplot pertama menampilkan gambar asli yang telah disesuaikan kecerahan sebelumnya dalam format RGB. Subplot kedua, ketiga, dan keempat masing-masing menampilkan saluran warna merah, hijau, dan biru dari gambar yang telah disesuaikan tersebut dalam format skala abu-abu menggunakan cmap="gray". Setiap subplot diberi judul sesuai dengan saluran warna yang ditampilkan. Setelah itu, keseluruhan plot ditampilkan menggunakan plt.show().

```python
merah=citra_cerah[:,:,0] #Merah
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([merah],[0],None,[256],[0,256])
axs[0].imshow(merah, cmap='gray')
axs[1].plot(hist)
plt.show()
```
Kode di atas bertujuan untuk menampilkan histogram dari saluran warna merah dalam gambar yang telah disesuaikan sebelumnya. Pertama, saluran warna merah diekstrak dari gambar yang disesuaikan menggunakan konversi warna dengan cv2.cvtColor, dan kemudian hanya saluran warna merahnya saja yang diambil menggunakan indeks [0]. Setelah itu, histogram dari saluran warna merah tersebut dihitung menggunakan fungsi cv2.calcHist, dan hasilnya ditampilkan dalam subplot pertama. Subplot kedua menampilkan plot histogram yang dihasilkan. Keseluruhan plot ditampilkan menggunakan plt.show().

```python
hijau=citra_cerah[:,:,1] #hijau
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([hijau],[0],None,[256],[0,256])
axs[0].imshow(hijau, cmap='gray')
axs[1].plot(hist)
plt.show()
```
Kode di atas mirip dengan kode sebelumnya, namun kali ini fokus pada saluran warna hijau dari gambar yang telah disesuaikan. Prosesnya sama, di mana saluran warna hijau diekstrak menggunakan konversi warna dengan cv2.cvtColor dan mengambil saluran hijaunya dengan indeks [1]. Kemudian histogram dari saluran warna hijau dihitung menggunakan cv2.calcHist, dan hasilnya ditampilkan dalam subplot pertama. Subplot kedua menampilkan plot histogram yang dihasilkan. Hasil akhir ditampilkan menggunakan plt.show().

```python
biru=citra_cerah[:,:,2] #biru
fig, axs = plt.subplots(1,2, figsize = (15,5))
hist = cv2.calcHist([biru],[0],None,[256],[0,256])
axs[0].imshow(biru, cmap='gray')
axs[1].plot(hist)
plt.show()
```
Kode di atas mirip dengan dua kode sebelumnya, tetapi kali ini fokus pada saluran warna biru dari gambar yang telah disesuaikan. Pertama, saluran warna biru diekstrak menggunakan konversi warna dengan cv2.cvtColor, dengan mengambil saluran birunya menggunakan indeks [2]. Kemudian histogram dari saluran warna biru dihitung menggunakan cv2.calcHist, dan hasilnya ditampilkan dalam subplot pertama. Subplot kedua menampilkan plot histogram yang dihasilkan. 

Selanjutnya, berdasarkan analisis saya, beberapa proses telah dilakukan pada citra yang disesuaikan sebelumnya:
-	Konversi ke Citra Grayscale: Citra asli dikonversi ke citra grayscale. Ini menghasilkan citra yang hanya memiliki satu saluran warna, yaitu tingkat keabuan, tanpa informasi warna.
-	Penyesuaian Kontras dan Kecerahan: Kontras dan kecerahan citra disesuaikan dengan meningkatkan kontras sebesar 1.5 kali dan kecerahan sebesar 30 nilai kecerahan. Hal ini mengubah distribusi intensitas piksel dalam citra, meningkatkan perbedaan antara area yang lebih gelap dan lebih terang.
-	Pemisahan Saluran Warna: Citra yang telah disesuaikan dibagi menjadi tiga saluran warna, yaitu merah, hijau, dan biru. Histogram dari setiap saluran warna kemudian diplotkan untuk menganalisis distribusi intensitas piksel dalam masing-masing saluran warna.
Dari hasil-hasil tersebut, kita dapat menganalisis perubahan-perubahan yang terjadi pada citra, seperti peningkatan kontras dan kecerahan, serta distribusi intensitas piksel dalam setiap saluran warna. Dengan demikian, dapat dilakukan analisis lebih lanjut terkait dengan karakteristik visual dan representasi warna dalam citra yang telah dimodifikasi. Lalu setelah itu dengan melihat histogram dari masing-masing saluran warna, kita dapat mengevaluasi distribusi intensitas piksel dalam citra yang telah disesuaikan. Histogram memberikan gambaran visual tentang sebaran nilai piksel dalam citra, yang berguna untuk mengetahui tingkat kontras, kecerahan, dan distribusi warna dalam citra. Dengan memeriksa histogram masing-masing saluran warna, kita dapat melihat apakah terdapat konsentrasi tertentu dalam intensitas piksel, apakah ada puncak yang dominan, serta seberapa jauh distribusi intensitas tersebut menyebar. Analisis ini dapat memberikan wawasan lebih lanjut tentang struktur dan karakteristik citra yang telah dimodifikasi, yang dapat digunakan untuk keperluan pemrosesan lanjutan, seperti segmentasi, deteksi fitur, atau pengenalan pola.

2. Nilai Ambang Batas
   - membaca data gambar
     ```python
     color_image = cv2.imread('fotorafi.jpeg')
     ```
     Kode di atas menggunakan OpenCV untuk membaca gambar yang disebut "fotorafi.jpeg" dan 
     menyimpannya dalam variabel img.
     
   - Koversi citra ke dalam ruang warna HSV
     ```python
     hsv_image = cv2.cvtColor(color_image, cv2.COLOR_BGR2HSV)
     ```
     Kode tersebut menggunakan opencv untuk mengonversi citra warna dari ruang warna RGB 
     menjadi ruang warna HSV. Konversi ini penting karena memungkinkan analisis citra berbasis 
     warna yang lebih intuitif, seperti segmentasi warna atau deteksi objek, karena ruang 
     warna HSV memisahkan komponen warna, intensitas, dan kecerahan.

   - Mendefinisikan rentang warna pada setiap warna
```python
lower_blue = np.array([90, 100, 100])
upper_blue = np.array([130, 255, 255])

lower_green = np.array([40, 100, 100])
upper_green = np.array([80, 255, 255])

lower_red1 = np.array([0, 100, 100])
upper_red1 = np.array([10, 255, 255])
lower_red2 = np.array([160, 100, 100])
upper_red2 = np.array([180, 255, 255])
```
Kode di atas mendefinisikan rentang nilai untuk deteksi warna tertentu dalam format ruang warna HSV. Setiap warna (biru, hijau, merah) memiliki batas bawah (lower_) dan batas atas (upper_) yang menentukan rentang nilai untuk setiap komponen ruang warna HSV: Hue (H), Saturation (S), dan Value (V). Misalnya, untuk deteksi warna biru, lower_blue dan upper_blue menentukan rentang nilai Hue (90-130), Saturation (100-255), dan Value (100-255). Ini digunakan dalam operasi segmentasi untuk mengekstrak area dalam citra yang sesuai dengan rentang warna yang ditentukan.

 - Mendeteksi warna biru, hijau dan merah
   ```python
   mask_blue = cv2.inRange(hsv_image, lower_blue, upper_blue)
   ```
Kode ini menggunakan cv2.inRange untuk membuat masker biner yang menyoroti area dalam citra yang sesuai dengan rentang warna biru yang telah ditentukan dalam format ruang warna HSV. Masker biner ini dapat digunakan untuk mengidentifikasi area warna biru dalam citra.

```python
mask_green = cv2.inRange(hsv_image, lower_green, upper_green)
```
Kode di atas menggunakan cv2.inRange untuk membuat masker biner yang menyoroti area dalam citra yang sesuai dengan rentang warna hijau yang telah ditentukan dalam format ruang warna HSV. Masker ini memungkinkan identifikasi area warna hijau dalam citra.

```python
mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
mask_red = cv2.bitwise_or(mask_red1, mask_red2)
```
Kode ini membuat dua masker biner terpisah (mask_red1 dan mask_red2) yang menyoroti area dalam citra yang sesuai dengan rentang warna merah yang telah ditentukan sebelumnya dalam format ruang warna HSV (lower_red1, upper_red1 dan lower_red2, upper_red2). Setelah itu, kedua masker tersebut digabungkan menggunakan operasi bitwise OR (cv2.bitwise_or) untuk menghasilkan masker biner tunggal (mask_red) yang mencakup semua area warna merah dalam citra.’

- Menggabungkan mask untuk warna merah dan biru
  ```python
  mask_red_blue = cv2.bitwise_or(mask_red, mask_blue)
  ```
Kode tersebut menggunakan operasi bitwise OR (cv2.bitwise_or) untuk menggabungkan dua masker biner terpisah, mask_red dan mask_blue, menjadi satu masker biner tunggal, mask_red_blue, yang mencakup area yang sesuai dengan rentang warna merah atau biru dalam citra.

- Menggabungkan mask untuk warna merah, biru, dan hijau
  ```python
  mask_red_blue_green = cv2.bitwise_or(cv2.bitwise_or(mask_red, mask_blue), mask_green)
  ```
Kode di atas menggabungkan tiga masker biner terpisah, yaitu mask_red, mask_blue, dan mask_green, menggunakan operasi bitwise OR (cv2.bitwise_or). Hasilnya adalah satu masker biner tunggal, mask_red_blue_green, yang mencakup area dalam citra yang sesuai dengan rentang warna merah, biru, atau hijau yang telah ditentukan sebelumnya dalam format ruang warna HSV.

-Plot Hasil
```python
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

plt.subplot(2, 2, 2)
plt.imshow(mask_blue, cmap='gray')
plt.title('Blue')
plt.xticks(np.arange(0, mask_blue.shape[1]+1, 800))
plt.yticks(np.arange(0, mask_blue.shape[0]+1, 500))
plt.axis('on')

plt.subplot(2, 2, 3)
plt.imshow(np.maximum(mask_red, mask_blue), cmap='gray')
plt.title('reed-blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

(thresh, binary4) = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')
```
Codingan tersebut melakukan beberapa operasi pemrosesan citra dan visualisasi hasilnya menggunakan Matplotlib. Pertama, citra awal (img) dikonversi menjadi citra keabuan (gray) menggunakan cv2.cvtColor. Selanjutnya, empat subplot ditampilkan dalam satu gambar. Subplot pertama menampilkan citra biner hasil thresholding dengan ambang nol (NONE). Subplot kedua menampilkan masker biner area warna biru. Subplot ketiga menampilkan gabungan dari masker biner area warna merah dan biru. Terakhir, subplot keempat menampilkan citra biner hasil thresholding dengan ambang 150, yang menghasilkan deteksi area yang lebih terang dalam citra keabuan, potensial untuk deteksi fitur yang lebih besar atau lebih terang.

- Teori yang mendukung mengenai projek terkait
  
1. Konversi Ruang Warna
- Teori: Ruang warna RGB (Merah, Hijau, Biru) adalah representasi umum untuk citra digital. Namun, untuk tugas tertentu, ruang warna lain seperti HSV (Hue, Saturation, Value) bisa lebih nyaman digunakan.
- Aplikasi: Kode tersebut mengonversi citra dari BGR (default OpenCV) ke RGB untuk keperluan plotting dan kemudian ke HSV untuk deteksi warna. HSV memisahkan informasi warna (hue) dari intensitas (value) dan saturasi, sehingga lebih mudah untuk menentukan rentang untuk deteksi warna.

2. Penyesuaian Kecerahan dan Kontras Citra
- Teori: Transformasi linear merupakan dasar untuk penyesuaian intensitas citra.
Penyesuaian kecerahan dicapai dengan menambahkan nilai konstan (beta) ke setiap intensitas piksel.
- Penyesuaian kontras dapat dilakukan dengan mengalikan setiap intensitas piksel dengan faktor konstan (alpha).
- Aplikasi: Kode mengimplementasikan konsep ini menggunakan cv2.convertScaleAbs dengan parameter alpha dan beta untuk mencerahkan citra.

3. Pemrosesan Histogram
- Teori: Histogram citra menggambarkan distribusi intensitas piksel di seluruh citra. Ini adalah alat yang berharga untuk memahami karakteristik citra dan melakukan operasi berbasis intensitas.
- Aplikasi: Kode menghitung histogram untuk saluran merah, hijau, dan biru dari citra yang telah dicerahkan, yang menunjukkan distribusi intensitas piksel dalam setiap komponen warna.
  
4. Deteksi Warna dengan Thresholding
- Teori: Thresholding adalah teknik untuk segmentasi citra yang mengubah citra grayscale menjadi citra biner (foreground dan background). Piksel dengan intensitas melebihi ambang batas tertentu (thresh) diberi nilai foreground (biasanya putih), sedangkan yang di bawahnya diberi nilai background (biasanya hitam). Deteksi warna dapat dicapai dengan menerapkan thresholding pada ruang warna yang sesuai.
- Aplikasi: Kode menggunakan thresholding dalam domain HSV. Ini mendefinisikan rentang tertentu untuk warna merah, hijau, dan biru dan membuat mask menggunakan cv2.inRange. Masker ini mengisolasi piksel dalam rentang warna yang ditentukan.

Singkatnya, proyek ini secara efektif menggunakan teori pemrosesan citra inti untuk peningkatan citra (kecerahan/kontras), analisis (histogram), segmentasi (thresholding dan deteksi warna) untuk mencapai berbagai tujuan pemrosesan citra.
