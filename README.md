Berikut penjelasan lebih detail untuk setiap bagian dari skrip Python yang menyatukan semua transformasi gambar:

### 1. Import Pustaka
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
- **cv2**: OpenCV, pustaka untuk pemrosesan gambar dan video.
- **numpy**: Pustaka untuk operasi numerik dan manipulasi array.
- **matplotlib.pyplot**: Pustaka untuk visualisasi data, khususnya plotting gambar.

### 2. Fungsi `show_image`
```python
def show_image(image, title='Image'):
    plt.figure(figsize=(5, 5))
    plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
    plt.title(title)
    plt.axis('off')
    plt.show()
```
- **show_image(image, title='Image')**: Fungsi untuk menampilkan gambar.
  - **plt.figure(figsize=(5, 5))**: Membuat figure baru dengan ukuran 5x5 inci.
  - **plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))**: Menampilkan gambar setelah mengonversinya dari format BGR ke RGB (karena OpenCV menggunakan BGR sedangkan Matplotlib menggunakan RGB).
  - **plt.title(title)**: Memberi judul pada gambar.
  - **plt.axis('off')**: Menghilangkan sumbu pada plot.
  - **plt.show()**: Menampilkan plot.

### 3. Membaca Gambar Asli
```python
image_path = 'image.jpg'
original_image = cv2.imread(image_path)
if original_image is None:
    print(f"Error: Gambar '{image_path}' tidak ditemukan.")
else:
    show_image(original_image, 'Citra Asli')
```
- **cv2.imread(image_path)**: Membaca gambar dari path yang ditentukan (`image.jpg`).
- **if original_image is None**: Memeriksa apakah gambar berhasil dibaca.
  - **print(f"Error: Gambar '{image_path}' tidak ditemukan.")**: Menampilkan pesan kesalahan jika gambar tidak ditemukan.
  - **show_image(original_image, 'Citra Asli')**: Menampilkan gambar asli dengan judul "Citra Asli".

### 4. Rotasi Gambar
```python
h, w = original_image.shape[:2]
center = (w // 2, h // 2)
angle = 45  # Derajat rotasi
scale = 1.0  # Skala rotasi
M_rot = cv2.getRotationMatrix2D(center, angle, scale)
rotated_image = cv2.warpAffine(original_image, M_rot, (w, h))
show_image(rotated_image, 'Rotated Image')
```
- **original_image.shape[:2]**: Mendapatkan tinggi (h) dan lebar (w) gambar asli.
- **center = (w // 2, h // 2)**: Menentukan pusat rotasi (titik tengah gambar).
- **angle = 45**: Sudut rotasi sebesar 45 derajat.
- **scale = 1.0**: Skala rotasi (1.0 berarti tidak ada skala).
- **cv2.getRotationMatrix2D(center, angle, scale)**: Membuat matriks rotasi berdasarkan pusat, sudut, dan skala yang ditentukan.
- **cv2.warpAffine(original_image, M_rot, (w, h))**: Menerapkan rotasi pada gambar asli menggunakan matriks rotasi.
- **show_image(rotated_image, 'Rotated Image')**: Menampilkan gambar yang telah dirotasi dengan judul "Rotated Image".

### 5. Mengubah Ukuran Gambar (Resize)
```python
width = int(w * 0.5)  # 50% dari lebar asli
height = int(h * 0.5)  # 50% dari tinggi asli
dim = (width, height)
resized_image = cv2.resize(original_image, dim, interpolation=cv2.INTER_AREA)
show_image(resized_image, 'Resized Image')
```
- **int(w * 0.5)**: Menghitung lebar baru sebagai 50% dari lebar asli.
- **int(h * 0.5)**: Menghitung tinggi baru sebagai 50% dari tinggi asli.
- **dim = (width, height)**: Menentukan dimensi baru gambar.
- **cv2.resize(original_image, dim, interpolation=cv2.INTER_AREA)**: Mengubah ukuran gambar menggunakan interpolasi area.
- **show_image(resized_image, 'Resized Image')**: Menampilkan gambar yang telah diubah ukurannya dengan judul "Resized Image".

### 6. Memotong Gambar (Crop)
```python
start_row, start_col = int(h * 0.25), int(w * 0.25)
end_row, end_col = int(h * 0.75), int(w * 0.75)
cropped_image = original_image[start_row:end_row, start_col:end_col]
show_image(cropped_image, 'Cropped Image')
```
- **int(h * 0.25)**: Menentukan baris awal sebagai 25% dari tinggi gambar.
- **int(w * 0.25)**: Menentukan kolom awal sebagai 25% dari lebar gambar.
- **int(h * 0.75)**: Menentukan baris akhir sebagai 75% dari tinggi gambar.
- **int(w * 0.75)**: Menentukan kolom akhir sebagai 75% dari lebar gambar.
- **original_image[start_row:end_row, start_col:end_col]**: Memotong gambar berdasarkan baris dan kolom yang ditentukan.
- **show_image(cropped_image, 'Cropped Image')**: Menampilkan gambar yang telah dipotong dengan judul "Cropped Image".

### 7. Membalik Gambar (Flip)
```python
flipped_image = cv2.flip(original_image, 1)  # 1 untuk flip horizontal
show_image(flipped_image, 'Flipped Image')
```
- **cv2.flip(original_image, 1)**: Membalik gambar secara horizontal (1 untuk flip horizontal).
- **show_image(flipped_image, 'Flipped Image')**: Menampilkan gambar yang telah dibalik dengan judul "Flipped Image".

### 8. Translasi Gambar
```python
M_trans = np.float32([[1, 0, 60], [0, 1, 40]])  # Geser 60 piksel ke kanan dan 40 piksel ke bawah
translated_image = cv2.warpAffine(original_image, M_trans, (w, h))
show_image(translated_image, 'Translated Image')
```
- **np.float32([[1, 0, 60], [0, 1, 40]])**: Membuat matriks translasi untuk menggeser gambar.
  - **[[1, 0, 60], [0, 1, 40]]**: Geser 60 piksel ke kanan dan 40 piksel ke bawah.
- **cv2.warpAffine(original_image, M_trans, (w, h))**: Menerapkan translasi pada gambar asli menggunakan matriks translasi.
- **show_image(translated_image, 'Translated Image')**: Menampilkan gambar yang telah ditranslasi dengan judul "Translated Image".

Dengan penjelasan ini, Anda dapat memahami setiap langkah dalam skrip Python untuk melakukan berbagai transformasi gambar. Simpan skrip ini sebagai file Python (misalnya, `image_transformations.py`) dan jalankan menggunakan interpreter Python Anda. Pastikan gambar `image.jpg` yang merupakan foto diri Anda berada di direktori yang sama dengan skrip ini.
