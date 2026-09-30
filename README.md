[README.md](https://github.com/user-attachments/files/32849491/README.md)
# Bangladesh Crime Clustering

Clustering wilayah kejadian kejahatan di Bangladesh dengan K-Means berdasarkan fitur cuaca, demografi, dan fasilitas publik. Dikerjakan oleh Samuel Christopher.

## Isi Repositori

```
.
├── README.md
├── requirements.txt
├── Bangladesh_Crime.ipynb
└── Bangladesh_Crime_Dataset_B.csv
```

File CSV harus berada di folder yang sama dengan notebook karena dibaca dengan path relatif.

## Dataset

`Bangladesh_Crime_Dataset_B.csv`: 6.574 baris, 26 kolom. Kolom utama mencakup waktu kejadian (bulan, minggu, hari, bagian hari), lokasi (distrik, divisi), cuaca (`precip`, `visibility`, `heatindex`), demografi (populasi, kepadatan, literasi), fasilitas (sekolah, kolese, kantor polisi, taman, dan lain-lain), serta jenis kejahatan (`crime`).

## Alur Notebook

1. **EDA dan cleaning**: standarisasi nama hari, hapus baris dengan `total_population` tidak positif, isi nilai kosong (modus untuk kategorikal, median untuk numerik), plot distribusi kejahatan, hari, dan heat index.
2. **Modeling**: 19 fitur numerik di-scale dengan `StandardScaler`, lalu K-Means diuji untuk k = 2 sampai 10 dengan elbow method dan silhouette score. Notebook memilih k = 3.
3. **Visualisasi**: proyeksi PCA 2 dimensi.
4. **Profil cluster**:
   - Cluster 0: area padat dan urban, infrastruktur banyak.
   - Cluster 1: area semi-urban, heat index tertinggi, literasi lebih rendah.
   - Cluster 2: area berkepadatan rendah dan lebih sejuk.

## Keterbatasan

- `KMeans` pada tahap tuning tidak diberi `random_state`, sehingga kurva elbow dan silhouette bisa sedikit berbeda tiap run.
- Kolom `crime` hanya dipakai di EDA dan tidak masuk ke clustering. Cluster menggambarkan karakteristik wilayah, bukan jenis kejahatan.
- Pemilihan k = 3 adalah keputusan yang perlu dicek ulang lewat kurva elbow dan silhouette masing-masing run.
