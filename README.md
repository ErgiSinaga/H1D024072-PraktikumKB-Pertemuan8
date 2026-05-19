# H1D024072-PraktikumKB-Pertemuan8
Yustinus Ergi Owen Sinaga - Shift C

## Deskripsi Program
Program ini menggunakan TensorFlow dan Keras untuk membuat model klasifikasi gambar sederhana yang dapat mengenali tiga kelas: `rock`, `paper`, dan `scissors`.

## Struktur Proyek
- `main.py`: kode utama yang memuat dataset, membangun model CNN, melatih model, dan melakukan evaluasi.
- `rockpaperscissors/`: folder dataset yang berisi subfolder `rock/`, `paper/`, dan `scissors/` dengan gambar masing-masing kelas.

## Penjelasan `main.py`
1. Impor pustaka
   - `numpy` dan `pandas`: tersedia untuk kebutuhan umum, meskipun tidak digunakan langsung dalam kode ini.
   - `tensorflow`, `keras.models.Sequential`, dan beberapa layer untuk membangun model CNN.
   - `ImageDataGenerator` untuk memuat dan memproses gambar dari folder.

2. Menentukan path dataset
   - `dataset_path = "./rockpaperscissors"`
   - Data diambil dari folder ini, yang harus berisi subfolder terpisah untuk setiap kelas.

3. Membuat `ImageDataGenerator`
   - `rescale=1/255` untuk menormalisasi nilai pixel menjadi rentang 0 sampai 1.
   - `validation_split=0.2` untuk memisahkan 20% data sebagai data validasi.

4. Menyiapkan data latih dan validasi
   - `train_generator` dibuat dengan `subset='training'`.
   - `validation_generator` dibuat dengan `subset='validation'`.
   - Gambar diubah ukurannya menjadi `(150,150)` dan batch diatur ke 32.
   - `class_mode='categorical'` karena ini klasifikasi multi-kelas.

5. Membangun model CNN
   - `Conv2D` dan `MaxPooling2D` digunakan untuk mengekstrak fitur dari gambar.
   - Tiga blok konvolusi diikuti pooling untuk menangkap pola visual.
   - `Flatten()` meratakan output sebelum masuk ke layer dense.
   - Layer dense pertama memiliki 512 neuron dengan aktivasi `relu`.
   - Output layer memiliki 3 neuron dengan aktivasi `softmax` untuk tiga kelas.

6. Menampilkan ringkasan model
   - `model.summary()` menampilkan arsitektur jaringan, jumlah parameter, dan ukuran output setiap layer.

7. Kompilasi model
   - `loss='categorical_crossentropy'` cocok untuk klasifikasi multi-kelas.
   - `optimizer='adam'` untuk pembaruan bobot.
   - `metrics=['accuracy']` untuk memantau akurasi selama pelatihan.

8. Melatih model
   - `model.fit` menggunakan `train_generator` dan `validation_generator`.
   - Pelatihan berlangsung selama 10 epoch.

9. Evaluasi dan prediksi
   - `model.evaluate` menghitung loss dan akurasi pada data validasi.
   - `model.predict` menghasilkan prediksi probabilitas untuk setiap gambar validasi.

## Cara Menjalankan
1. Pastikan semua dependensi terinstal, termasuk `tensorflow`.
2. Jalankan perintah:
   ```bash
   python main.py
   ```
3. Periksa output di terminal untuk ringkasan model, nilai loss, dan akurasi validasi.

## Output yang Diharapkan
- Ringkasan model CNN.
- Nilai `Validation loss` dan `Validation accuracy` setelah evaluasi.
- Matriks prediksi probabilitas untuk batch validasi terakhir.

## Catatan
- Dataset harus terstruktur dengan benar di dalam `rockpaperscissors/`.
- Jika dataset tidak lengkap atau folder kosong, program akan gagal memuat data.
