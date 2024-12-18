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
Setelah pembersihan, data final mencakup 12 kolom utama yang siap untuk dianalisis lebih lanjut. Berikut adalah cuplikan data:
```python
# Cuplikan Data
print(df.head())
```

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

