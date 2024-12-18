# ProyekAkhirAnalisisBigData
**Proyek Akhir Analisis Big Data** adalah luaran mata kuliah yang diampu oleh **Bapak Yuda Munarko, S.Kom., M.Sc.** Proyek ini bertujuan menganalisis data Spotify untuk memahami pola genre musik melalui klastering, visualisasi, dan eksplorasi data. Luaran ini bermanfaat untuk penyedia konten, konsumen, dan pengembang fitur berbasis data.

# Spotify Genre Analysis

## Tim Kami
1. **Marsela Margareta** - NIM: 202110370311247 (Kelas: Analisis Big Data A)  
2. **Uswatun Chasanah** - NIM: 202110370311274 (Kelas: Analisis Big Data A)  
3. **Akhtar Azizi Farid** - NIM: 202110370311281 (Kelas: Analisis Big Data C)  

---

## Pendahuluan
### Pernyataan Masalah
Musik adalah bagian integral dari kehidupan manusia. Spotify, sebagai salah satu platform streaming musik terbesar di dunia, menyediakan berbagai data tentang genre musik, yang dapat dimanfaatkan untuk mendapatkan wawasan yang menarik. Namun, banyak data ini belum diolah secara optimal untuk menjawab pertanyaan seperti:
- Apa saja genre musik yang paling populer?
- Bagaimana distribusi genre berdasarkan berbagai metrik, seperti durasi atau energy?

Analisis ini penting untuk memahami preferensi pendengar musik, yang berguna bagi pengembang konten, penyusun playlist, maupun konsumen umum.

### Rencana Penyelesaian Masalah
1. **Dataset**: Data diperoleh dari [link ini](https://www.dropbox.com/sh/qj0ueimxot3ltbf/AACzMOHv7sZCJsj3ErjtOG7ya?dl=1). Dataset ini mencakup berbagai informasi tentang lagu, seperti genre, durasi, energy, dan atribut lain yang relevan.
2. **Metodologi**: Kami akan membersihkan data, mengeksplorasi metrik penting, dan menggunakan teknik seperti visualisasi data dan klastering untuk memahami pola dalam genre musik.
3. **Teknik Analisis**: Menggunakan eksplorasi data deskriptif, klastering dengan K-Means, serta visualisasi mendalam menggunakan Matplotlib dan Seaborn.

### Manfaat Analisis
Hasil analisis ini akan membantu:
- Konsumen dalam menemukan genre yang sesuai dengan preferensi mereka.
- Spotify untuk mengembangkan fitur-fitur yang lebih relevan berdasarkan data analitik.
- Penyedia konten untuk menyusun strategi distribusi musik.

---

## Memuat Package yang Diperlukan
```python
# Memuat package yang diperlukan
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import MinMaxScaler, StandardScaler
from sklearn.cluster import KMeans

# Menonaktifkan pesan peringatan
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
- **Jumlah Variabel**: Dataset awal memiliki 15 kolom.
- **Kekhasan Dataset**: Data berisi beberapa nilai kosong (missing values) yang perlu diimputasi dan beberapa atribut numerik yang memerlukan normalisasi.
  
### Langkah Pembersihan Data
1. **Mengimpor Data**:
   Dataset diimpor menggunakan Pandas.
2. **Penanganan Missing Values**:
   Missing values diisi menggunakan strategi mean/mode dengan `SimpleImputer`.
3. **Normalisasi Data**:
   Data numerik dinormalisasi menggunakan `MinMaxScaler`.

### Dataset Setelah Dibersihkan
Setelah pembersihan, data final mencakup 12 kolom utama yang siap untuk dianalisis lebih lanjut. Berikut adalah cuplikan data:|index|track\_id|track\_name|track\_artist|track\_popularity|track\_album\_id|track\_album\_name|track\_album\_release\_date|playlist\_name|playlist\_id|playlist\_genre|playlist\_subgenre|danceability|energy|key|loudness|mode|speechiness|acousticness|instrumentalness|liveness|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|6f807x0ima9a1j3VPbc7VN|i dont care with justin bieber  loud luxury remix|ed sheeran|66\.0|2oCs0DGTsRO98Gh5ZSl2Cx|I Don't Care \(with Justin Bieber\) \[Loud Luxury Remix\]|2019-06-14|Pop Remix|37i9dQZF1DXcZDD7cfEKhW|pop|dance pop|0\.748|0\.916|6\.0|-2\.634|1\.0|0\.0583|0\.102|0\.0|0\.0653|
|1|0r7CVbZTWZgbTCYdfa2P31|memories  dillon francis remix|maroon 5|67\.0|63rPSO264uRjW1X5E6cWv6|Memories \(Dillon Francis Remix\)|2019-12-13|Pop Remix|37i9dQZF1DXcZDD7cfEKhW|pop|dance pop|0\.726|0\.815|11\.0|-4\.969|1\.0|0\.0373|0\.0724|0\.00421|0\.357|
|2|1z1Hg7Vb0AhHDiEmnDE79l|all the time  don diablo remix|zara larsson|70\.0|1HoSmj2eLcsrR0vE9gThr4|All the Time \(Don Diablo Remix\)|2019-07-05|Pop Remix|37i9dQZF1DXcZDD7cfEKhW|pop|dance pop|0\.675|0\.931|1\.0|-3\.432|0\.0|0\.0742|0\.0794|2\.33e-05|0\.11|
|3|75FpbthrwQmzHlBJLuGdC7|call you mine  keanu silva remix|the chainsmokers|60\.0|1nqYsOef1yKKuGOVchbsk6|Call You Mine - The Remixes|2019-07-19|Pop Remix|37i9dQZF1DXcZDD7cfEKhW|pop|dance pop|0\.718|0\.93|7\.0|-3\.778|1\.0|0\.102|0\.0287|9\.43e-06|0\.204|
|4|1e8PAfcKUYoKkxPhrHqw4x|someone you loved  future humans remix|lewis capaldi|69\.0|7m7vv9wlQ4i0LFuJiE2zsQ|Someone You Loved \(Future Humans Remix\)|2019-03-05|Pop Remix|37i9dQZF1DXcZDD7cfEKhW|pop|dance pop|0\.65|0\.833|1\.0|-4\.672|1\.0|0\.0359|0\.0803|0\.0|0\.0833|

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
   - Genre musik yang paling dominan adalah "Pop" dan "Rock".

2. **Korelasi Energy-Danceability**:
   - Energy tinggi cenderung berkorelasi positif dengan danceability.

3. **Klastering**:
   - Lagu dikelompokkan menjadi 3 klaster utama berdasarkan atribut numerik.

### Visualisasi
```python
# Contoh Plot
plt.figure(figsize=(10, 6))
sns.barplot(x='genre', y='count', data=genre_distribution)
plt.title('Distribusi Genre Musik')
plt.xlabel('Genre')
plt.ylabel('Jumlah Lagu')
plt.show()
```

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

