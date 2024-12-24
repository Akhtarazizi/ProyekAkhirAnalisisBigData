# ProyekAkhirAnalisisBigData
**Proyek Akhir Analisis Big Data** adalah luaran mata kuliah yang diampu oleh **Bapak Yuda Munarko, S.Kom., M.Sc.** Proyek ini bertujuan menganalisis data Spotify untuk memahami pola genre musik melalui klasifikasi, visualisasi, dan eksplorasi data. Luaran ini bermanfaat untuk penyedia konten, konsumen, dan pengembang fitur berbasis data.

# Spotify Genre Analysis

## Tim Kami
1. **Marsela Margareta** - NIM: 202110370311247 (Kelas: Analisis Big Data A)  
2. **Uswatun Chasanah** - NIM: 202110370311274 (Kelas: Analisis Big Data A)  
3. **Akhtar Azizi Farid** - NIM: 202110370311281 (Kelas: Analisis Big Data C)  

---

## Pendahuluan
### Pernyataan Masalah
Popularitas sebuah lagu sering kali menjadi tolok ukur kesuksesan dalam industri musik. Bagi artis, produser, dan label rekaman, memahami faktor yang menentukan popularitas lagu sangatlah penting untuk menciptakan karya yang tidak hanya relevan secara artistik tetapi juga menarik bagi audiens. Dengan meningkatnya platform streaming musik seperti Spotify, data terkait performa lagu kini dapat diakses dengan lebih mudah. Penelitian untuk memprediksi popularitas lagu dapat membantu industri musik membuat keputusan yang lebih strategis dan meningkatkan peluang sukses lagu baru. Topik ini menarik karena menggabungkan dunia musik dengan teknologi data science untuk memberikan wawasan yang berharga.

Analisis ini penting untuk memahami preferensi pendengar musik, yang berguna bagi pengembang konten, penyusun playlist, maupun konsumen umum.

### Rencana Penyelesaian Masalah
1. **Dataset**: Data diperoleh dari [link ini](https://www.dropbox.com/sh/qj0ueimxot3ltbf/AACzMOHv7sZCJsj3ErjtOG7ya?dl=1). Dataset ini mencakup berbagai informasi tentang lagu, seperti genre, durasi, energy, dan atribut lain yang relevan.
2. **Metodologi**: Kami akan membersihkan data, mengeksplorasi metrik penting, dan menggunakan teknik seperti visualisasi data dan klasifikasi untuk memahami pola dalam genre musik.
3. **Teknik Analisis**: Menggunakan eksplorasi data deskriptif, klasifikasi dengan KNNClassifier, SVMClassifier dan XGBOOST, serta visualisasi mendalam menggunakan Matplotlib dan Seaborn.

### Manfaat Analisis
Hasil analisis ini akan membantu:
- Konsumen dalam menemukan genre yang sesuai dengan preferensi mereka.
- Spotify untuk mengembangkan fitur-fitur yang lebih relevan berdasarkan data analitik.
- Penyedia konten untuk menyusun strategi distribusi musik.

---

## Memuat Package yang Diperlukan
- pandas
- numpy
- matplotlib.pyplot
- seaborn
- scikit-learn

# Menonaktifkan pesan peringatan
``` python
import warnings
warnings.filterwarnings("ignore")
```
---

## Data Preparation
### Sumber Data
- Dataset diperoleh dari [link ini](https://www.dropbox.com/sh/qj0ueimxot3ltbf/AACzMOHv7sZCJsj3ErjtOG7ya?dl=1).
- Dataset mencakup informasi tentang berbagai atribut lagu, seperti genre, durasi, energy, danceability, dan lain-lain.

### Deskripsi Dataset
- **Tujuan Awal**: Menganalisis data genre musik di Spotify untuk mendapatkan wawasan menarik.
- **Jumlah Variabel**: Dataset awal memiliki 24 kolom.
- **Kekhasan Dataset**: Data berisi beberapa nilai kosong (missing values) yang perlu diimputasi dan beberapa atribut numerik yang memerlukan normalisasi.
  
### Langkah Pembersihan Data
1. **Mengimpor Data**:
   Dataset diimpor menggunakan Pandas.
2. **Penanganan Missing Values**:
   Missing values diisi menggunakan strategi mean/mode dengan `SimpleImputer`.
3. **Normalisasi Data**:
   Data numerik dinormalisasi menggunakan `MinMaxScaler`.
4. **Menghapus Kolom Yang Tidak di Gunakan**:
   Data atau kolom yang tidak relevan dan tidak memiliki keterkaitan terhadap proses analisis di drop atau dihapus kolom tersebut guna mempermudah dalam melakukan proses analisis selanjutnya dan menghasilkan data yang bersih, kolom `track_id`, `track_album_id`, dan `playlist_id` dihapus karena kolom-kolom tersebut tidak terdapat nilai yang spesifik sehingga tidak dapat atau tidak ada kelayakan untuk melakukan analisis dimana kolom tersebut berisikan angka dan huruf bercampuran.

### Dataset Setelah Dibersihkan
Setelah pembersihan, data final mencakup 21 kolom utama yang siap untuk dianalisis lebih lanjut. Berikut adalah cuplikan data:
|index|track\_name|track\_artist|track\_popularity|track\_album\_name|track\_album\_release\_date|playlist\_name|playlist\_genre|playlist\_subgenre|danceability|energy|key|loudness|mode|speechiness|acousticness|instrumentalness|liveness|valence|tempo|duration\_ms|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|i dont care with justin bieber  loud luxury remix|ed sheeran|66\.0|i dont care with justin bieber loud luxury remix|2019-06-14|pop remix|pop|dance pop|0\.748|0\.916|6\.0|-2\.634|1\.0|0\.0583|0\.102|0\.0|0\.0653|0\.518|122\.036|194754\.0|
|1|memories  dillon francis remix|maroon 5|67\.0|memories dillon francis remix|2019-12-13|pop remix|pop|dance pop|0\.726|0\.815|11\.0|-4\.969|1\.0|0\.0373|0\.0724|0\.00421|0\.357|0\.693|99\.972|162600\.0|
|2|all the time  don diablo remix|zara larsson|70\.0|all the time don diablo remix|2019-07-05|pop remix|pop|dance pop|0\.675|0\.931|1\.0|-3\.432|0\.0|0\.0742|0\.0794|2\.33e-05|0\.11|0\.613|124\.008|176616\.0|
|3|call you mine  keanu silva remix|the chainsmokers|60\.0|call you mine  the remixes|2019-07-19|pop remix|pop|dance pop|0\.718|0\.93|7\.0|-3\.778|1\.0|0\.102|0\.0287|9\.43e-06|0\.204|0\.277|121\.956|169093\.0|
|4|someone you loved  future humans remix|lewis capaldi|69\.0|someone you loved future humans remix|2019-03-05|pop remix|pop|dance pop|0\.65|0\.833|1\.0|-4\.672|1\.0|0\.0359|0\.0803|0\.0|0\.0833|0\.725|123\.976|189052\.0|

---

## Eksplorasi dan Analisis Data
### Pendekatan Analisis
1. **Visualisasi Data**:
   - Membuat distribusi genre musik menggunakan bar chart.
   - Menampilkan korelasi antara energy dan danceability.
2. **Klastering**:
   - Mengelompokkan lagu berdasarkan kesamaan atribut menggunakan algoritma K-Means.
3. **Pembuatan Variabel Baru**:
   - Menambahkan variabel baru seperti "popularitas relatif" berdasarkan metrik tertentu.

### Hasil Analisis
1. **Visualisasi Distribusi Genre**:
   ![Distribusi Genre](gambar/1.JPEG)

2. **Korelasi Antar Kolom Numerik**:
   ![Matrix Korelasi](gambar/CFCORE.png)

4. **Klastering**:
   - Lagu dikelompokkan menjadi 3 klaster utama berdasarkan atribut numerik.

### Visualisasi (isikan dengan hasil visualisasinya)

---

## Rangkuman
### Penyelesaian Masalah
- **Pernyataan Masalah**: Mengidentifikasi pola dan wawasan dalam data genre musik Spotify.
- **Pendekatan**: Pembersihan data, eksplorasi visual, dan klastering K-Means.

### Temuan Menarik
- Genre "Pop" mendominasi daftar lagu, diikuti oleh "Rock".
- Lagu dengan energy tinggi lebih cenderung memiliki danceability tinggi.

### Implikasi Analisis
- Konsumen dapat menggunakan wawasan ini untuk menemukan musik yang sesuai dengan preferensi mereka.
- Spotify dapat memanfaatkan pola ini untuk meningkatkan rekomendasi.

### Keterbatasan
- Analisis ini terbatas pada atribut yang ada dalam dataset.
- Penelitian lebih lanjut dapat mencakup data tambahan seperti lirik lagu atau sentimen pendengar.

---

**Catatan:**
Kode lengkap dapat dijalankan tanpa error dan telah diuji dengan dataset terkait. README ini memberikan pengantar untuk memahami dan mereplikasi analisis kami.

