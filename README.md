Sure! Here's the translation into Bahasa Indonesia, including the images as requested.

---

# Analisis Data Eksplorasi pada Dataset Pokemon Unite
Usaha pertama saya dalam EDA pada Statistik Pokemon Unite, yang mencakup

0. Memuat Data  
1. Informasi Dasar  
2. Duplikat atau Nilai Unik  
3. Visualisasi Nilai Unik  
4. Menemukan Nilai Null  
5. Mengganti Nilai Null (Jika Ditemukan)  
6. Mengganti Nilai Null (Jika Ditemukan)  
7. Mengetahui jenis data dari dataset untuk mempermudah proses  
8. Memfilter Data  
9. Membuat Box Plot  
10. Korelasi  

## 0. Memuat Data  
![image](https://github.com/user-attachments/assets/4fb880f7-b1cd-4be5-b11e-14bbf7cad966)  
Dengan Python, kita bisa mengimpor pustaka seperti Pandas untuk memuat Dataset, Seaborn, dan matplotlib untuk memvisualisasikan data.

Untuk memuat dataset saya menggunakan:  
```py
df = pd.read_csv("FILE DIRECTORY")
```
Untuk menemukan direktori file, kita bisa menempatkan file CSV di folder yang sama dengan kode atau kita bisa mengklik file CSV dan klik Salin Jalur.  
![image](https://github.com/user-attachments/assets/2508b422-98ad-48d7-a0dd-0d41aabb4cea)

Kode Anda harus terlihat seperti ini:  
```py
df = pd.read_csv("C:\Users\PC\Documents\PokemonUniteData.csv")
df
```

Dan outputnya harus terlihat seperti ini.  
![image](https://github.com/user-attachments/assets/9d45db83-5846-4c4f-97d9-db40e0dd537d)  

## 1. Informasi Dasar  
Setelah memuat dataset, kita perlu melihat informasi tentang dataset tersebut.  
Dengan menggunakan:  
```py
df.info()
```
Kita bisa melihat informasi tentang dataset, seperti jenis data, jumlah non-null, dan nama kolom.  
![image](https://github.com/user-attachments/assets/f0e65c39-5094-41a0-946a-da88ab8f221f)  

## 2. Duplikat atau Nilai Unik  
Setelah menganalisis informasi tentang dataset, kita akan mencoba mencari apakah ada duplikat atau nilai yang hilang.  
```py
df_duplicate = df.duplicated().sum()

df_unique = df.nunique()

print("Jumlah duplikat yang ditemukan dalam data :", df_duplicate, "\n")
print(df_unique)
```

Dengan `.duplicated()` kita bisa melihat apakah data tersebut duplikat atau tidak melalui output boolean. False untuk data yang tidak duplikat, dan True untuk data yang duplikat. Setelah itu, kita menggunakan `.sum()` untuk menjumlahkan semua False/True dan melihat berapa banyak data yang terduplikasi.

Beralih ke `.nunique()`, ini menghitung berapa banyak string, int, float unik yang ada di kolom.  

Jika dilakukan dengan benar, outputnya harus terlihat seperti ini.  
![image](https://github.com/user-attachments/assets/4d5a7b47-0973-4226-90d4-ca977d56cf58)  

Dari sini, kita bisa berasumsi bahwa tidak ada data yang terduplikasi dan kita juga bisa melihat beberapa data unik untuk setiap kolom.  

## 3. Visualisasi Nilai Unik  
Sekarang untuk bagian Visualisasi, kita akan menggunakan matplotlib sebagai plt.  
```py
plt.figure(figsize=(10, 6))
df_unique.drop(["Name", "Description"]).plot(kind='bar', color='skyblue')
plt.title("Jumlah Nilai Unik di Setiap Kolom")
plt.ylabel("Jumlah Nilai Unik")
plt.xticks(rotation=45)
plt.show()
```

`figure()` Mengatur ukuran kanvas untuk visualisasi.

`drop(["Name", "Description"])` Menghapus kolom yang tidak perlu dari dataset.

`title()` Menambahkan judul di bagian atas tengah visualisasi.

`ylabel()` Menandai sumbu y dari grafik.

`xlabel()` Menandai sumbu x dari grafik.

`xticks(rotation=45)` Memutar label sumbu x sebesar 45 derajat agar sesuai.

`show()` Menampilkan visualisasi akhir.  
![image](https://github.com/user-attachments/assets/4f161895-ff18-4bc1-858a-f29b20445eee)  

## 4. Menemukan Nilai Null  
Menemukan nilai yang hilang atau Null dari dataset adalah wajib untuk EDA karena kita perlu data yang jelas dan utuh tanpa nilai yang hilang.  
```py
df_null = df.isnull().sum()
print("Jumlah Nilai yang Hilang ditemukan dalam data")
df_null
```

`isnull()` menentukan apakah data hilang atau kosong.  
`sum()` menjumlahkan seluruh array, baris, atau daftar.  
![image](https://github.com/user-attachments/assets/3efc0c6b-eef1-4551-9402-00240f9f98cb)  

Seperti yang kita lihat di sini, tidak ada Data yang Hilang, kita bisa berasumsi bahwa data kita utuh sepenuhnya dan kita bisa melewati ke Nomor 7.  

## 7. Mengetahui jenis data dari dataset untuk mempermudah proses  
Sebelum kita membuat visualisasi, kita perlu mengetahui jenis data apa yang tersedia di dataset. Kita bisa mengetahuinya dengan menggunakan `dtypes`.  
```py
df.dtypes
```
![image](https://github.com/user-attachments/assets/7a99bd70-1e5c-4ea2-9db8-f29b6e7755e1)  

## 8. Memfilter Data  
Bagian ini diperlukan untuk memfilter data yang tidak perlu yang akan menghalangi visualisasi.  

Kita akan mulai memfilternya berdasarkan UsageDifficulty.  
```py
df_usagedifficulty_Novice = df[df['UsageDifficulty'] == "Masukkan Kesulitan"]
print("Jumlah Pokemon yang memiliki Kesulitan Penggunaan Masukkan Kesulitan :", len(df_usagedifficulty_Novice))
df_usagedifficulty_Novice.head()
```
Karena hanya ada 3 Kesulitan Penggunaan yang tersedia yaitu Novice, Intermediate, dan Expert. Kita bisa mengganti "Masukkan Kesulitan" dengan Kesulitan yang disebutkan sebelumnya.  
![image](https://github.com/user-attachments/assets/fcf0b76b-2522-41e5-af9c-0344665f6368)  

Berikut adalah contoh output dari dataset yang telah difilter berdasarkan Kesulitan Penggunaan Novice.  

Sebelum kita masuk ke bagian visualisasi, kita perlu menambahkan kolom baru. Ini adalah total statistik.  
```py
df['Total Stats'] = df[['Offense', 'Endurance', 'Mobility', 'Scoring', 'Support']].sum(axis=1)
df.head()
```

Jadi kita menjumlahkan Offense, Endurance, Mobility, Scoring, dan Support dan menggunakan `axis=1` untuk kolom baru di sisi kanan dataset.

Dataset baru harus terlihat seperti ini.  
![image](https://github.com/user-attachments/assets/285126dd-4c01-4fd7-be00-2a4c4eda1d60)  

Contoh lain memfilter berdasarkan kolom Range atau Melee.  
```py
df_melee = df[df['Ranged_or_Melee'] == "Melee"]
df_ranged = df[df['Ranged_or_Melee'] == "Ranged"]
```  

## 9. Membuat Box Plot  
Sekarang masuk ke visualisasi.  
```py
plt.figure(figsize=(10, 6))
sns.boxplot(x='UsageDifficulty', y='Total Stats', data=df)
plt.title('Perbandingan Total Stats berdasarkan Kesulitan Penggunaan')
plt.xlabel('Kesulitan Penggunaan')
plt.ylabel('Total Stats')
plt.show()
```

`figure(figsize=(10, 6))`: Mengatur ukuran kanvas menjadi 10x6 untuk visualisasi.

`sns.boxplot(x='UsageDifficulty', y='Total Stats', data=df)`: Membuat boxplot yang membandingkan 'Total Stats' di berbagai kategori 'Kesulitan Penggunaan' menggunakan dataset `df`.

`title('Perbandingan Total Stats berdasarkan Kesulitan Penggunaan')`: Menambahkan judul di bagian atas tengah visualisasi.

`xlabel('Kesulitan Penggunaan')`: Menandai sumbu x sebagai 'Kesulitan Penggunaan'.

`ylabel('Total Stats')`: Menandai sumbu y sebagai 'Total Stats'.

`show()`: Menampilkan produk akhir dari visualisasi.  
![image](https://github.com/user-attachments/assets/483214ff-8ec9-40d7-9ffd-b643a8e120fa)  

## 10. Korelasi  
Sekarang ke langkah terakhir, untuk melihat apakah ada korelasi antara data.  
```py
correlation_matrix = df[['Offense', 'Endurance', 'Mobility', 'Scoring', 'Support', 'Total Stats']].corr()

plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', linewidths=0.5)

plt.title('Matriks Korelasi')
```

`df[['Offense', 'Endurance', 'Mobility', 'Scoring', 'Support

', 'Total Stats']].corr()`: Menghitung matriks korelasi untuk kolom yang dipilih.

`figure(figsize=(10, 8))`: Mengatur ukuran kanvas menjadi 10x8 untuk visualisasi.

`sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', linewidths=0.5)`: Membuat heatmap dari matriks korelasi dengan anotasi dan menggunakan skema warna 'coolwarm'. Lebar garis diatur menjadi 0,5 untuk memisahkan sel.

`title('Matriks Korelasi')`: Menambahkan judul di bagian atas tengah visualisasi.  
![image](https://github.com/user-attachments/assets/18efa5e8-5ce5-449f-96fe-73d01ae07773)  

Korelasi Tinggi (dekat dengan 1 atau -1): Menunjukkan Korelasi yang kuat (positif atau negatif) antara dua variabel.  

Korelasi Rendah (dekat dengan 0): Menunjukkan sedikit atau tidak ada Korelasi antara variabel.  

--- 
