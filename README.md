# Ijo-Lumut
Final Project Bootcamp Rakamin DS batch 27
## Descriptive Analysis


### A. Tipe data pada tiap-tiap kolom <br>
Terdapat kolom dengan tipe data yang tidak sesuai diantaranya: <br>
- OperatingSystems <br> 
- Browser <br>
- Region <br>
- TrafficType <br>

Cara mengubah tipe data:

```code
df = df.astype({'OperatingSystems': object, 'Browser': object, 'Region': object, 'TrafficType': object})
```

Selanjutnya data tersebut dapat dikategorikan menjadi 3 kategori yaitu: <br>
- Numerikal
- Kategorikal
- Waktu

Cara membuat kategori:
```code
numericals   = ['Administrative', 'Administrative_Duration', 'Informational', 'Informational_Duration', 'ProductRelated', 
              'ProductRelated_Duration', 'BounceRates', 'ExitRates', 'PageValues', 'SpecialDay']
categoricals = ['OperatingSystems', 'Browser', 'Region', 'TrafficType', 'VisitorType', 'Weekend', 'Revenue']
timestamps   = ['Month']
```

### B. Nilai kosong pada tiap-tiap kolom <br>
Dengan menggunakan `df.isna().sum()` kita dapat melihat kolom apa saja yang memiliki nilai kosong dan hasilnya tidak terdapat nilai kosong pada tiap-tiap kolom

### C. Nilai outlier <br>
Positively skewed (Mean > Median):<br>
- Positively skewed: Administrative, Administrative_Duration, Informational, Informational_Duration, Productrelated, ProductRelated_Duration, ExitRates, PageValues, SpecialDay<br> 

Negatively skewed (Median > Mean):<br>
- BounceRates


## Unvariate Analysis
### Outlier
Hampir semua fitur dari dataset ini memiliki outlier
Terdapat beberapa fitur yang memiliki nilai ekstrim seperti pada Administrative_Duration, Informational, Informational_Duration, ProductRelated, ProductRelated_Duration, BounceRates, PageValues dan Browser.

### Distribusi
Semua fitur dalam dataset ini berdistribusi positive skewed karena masih terdapat outlier dalam fitur-fitur tersebut.

### Violin plot
Pada viloin plot di ketahui jika fitur-fitur memiliki ketimpangan nilai karena adanya ouliers

## Multivariate Analysis
### Correlation 
Feature yang memiliki korelasi dengan label:
PageValues: kolerasi positif (0.49)
ExitRates: korelasi negatif (-0.21)
ProductRelated: korelasi positif (0.16); mejadi tipe halaman dengan nilai korelasi paling besar
Catatan lainnya:
1. BounceRates dan ExitRates berkorelasi kuat (0.91), ada kemungkinan redundan
2. Page_type dan Page_type_duration memiliki korelasi positif yang cukup besar. Secara intuitif, semakin banyak halaman tersebut dibuka, maka akan membutuhkan durasi yang lebih lama.

Berdasarkan gambaran korelasi, perlu diperiksa:

1.Feature yang memiliki korelasi dengan feature target (Revenue)
2.Feture lainnya yang memiliki korelasi dengan feature (1)
3.Keterkaitan feature lainnya

### Category plot
Terdapat beberapa pola yang menarik:

1. Feature yang memiliki korelasi dengan feature target (Revenue)

  a. PageValues: terdapat kecenderungan user akan melakukan pembelian pada nilai PageValues yang tinggi.
  b. Exit/Bounce-Rates: terdapat kecenderungan user akan melakukan pembelian saat nilai Exit/Bounce-Rates rendah.
  c.Tidak ada separasi nilai Revenue yang cukup jelas pada scatter plot feature lainnya.

 2.Feature lainnya yang memiliki korelasi dengan feature (1)
   a.Pada scatterplot antara PageValues dan Bounce/Exit-Rates dapat dilihat bahwa user yang melakukan pembelian cenderung berkumpul pada area bawah (nilai PageValues besar, dan nilai Bouce/ExitRates kecil).
    b.Pada nilai SpecialDay 0.0 (jarak SpecialDay dengan waktu kunjungan sangat dekat), nilai PageValues cenderung besar dan user melakukan pembelian.
    
3. Feature lainnya
1. Tidak diperoleh relasi antara type halaman yang mengakibatkan user akan mengunjungi halaman a akibat halaman b atau semisalnya.
2. Tidak ada kecenderungan seseorang akan melakukan pembelian (Revenue = True) atau tidak berdasarkan tipe dan durasi halaman yang berbeda.


###Boxplot
User yang melakukan pembelian (Revenue = True) secara garis besar memiliki:
1.Nilai PageValues yang lebih besar
2.Nilai ExitRates dan BounceRates yang lebih kecil

### Histogram
a. Secara keseluruhan, user yang melakukan pembelian (Revenue = True) memiliki nilai PageValues yang besar.
b. Persentase user yang melakukan pembelian (Revenue = True) mengalami penurunan seiring dengan adanya peningkatan nilai ExitRates.

User yang melakukan pembelian (Revenue = True) cenderung merupakan user dengan session yang memiliki nilai PageValues yang cukup tinggi, dan nilai ExitRates yang cukup rendah. Hal ini mengakibatkan dots yang mewakilkan user tersebut cenderung berkumpul pada bagian kiri-bawah.

### Insight lainnya
Baik user yang hanya mengunjungi halaman ataupun melakukan pembelian lebih banyak dilakukan pada weekday dibandingkan weekend. Hal ini turut dipengaruhi juga oleh banyak hari yang berbeda antara weekday dan weekend.
User yang datang ataupun datang dan melakukan pembelian yang paling banyak adalah Returning Visitor.
Secara keseluruhan, user bertipe Returning_Visitor adalah user yang paling banyak melakukan pembelian.
Returning Visitor sendiri paling banyak berkunjung pada bulan May, disusul pada bulan Nov.
Namun user yang melakukan pembelian paling banyak secara kumulatif (dari ketiga jenis Visitor Type-nya) ada pada bulan November.
Hubungan antara jenis halaman dan durasi kunjungan

1. User yang membuka halaman administrative > 19 kali dalam 1 sesi tidak melakukan pembelian.
2. Semakin sering halaman administrative dibuka, maka durasi yang dibutuhkan cenderung semakin lama.
3. User yang membuka halaman administrative < 7 kali dalam 1 sesi yang memutuskan untuk membeli cenderung mengunjungi halaman dengan total waktu yang relatif lebih sebentar dibandingkan dengan yang tidak melakukan pembelian.

User cenderung menghabiskan waktu lebih lama saat mengunjungi halaman Informational dibandingkan halaman Administrative
User cenderung lebih sering mengunjungi halaman ProductRelated dibandingkan halaman lainnya
Tidak dapat disegmentasi secara langsung apakah user akan melakukan pembelian atau tidak apabila dilihat dari jumlah kunjungan dan durasi pada halaman ProductRelated

## Data Cleansing


## Feature Engineering

### Feature Selection
Fitur yang kurang relevan dan redundan sehingga perlu dihilangkan:
1. OperatingSystem
2. Browser
3. Region
4. TrafficType
5. BounceRates

```code
df_2 = df.drop(['OperatingSystems', 'Browser', 'Region', 'TrafficType', 'BounceRates'], axis=1)
```

Feature OperatingSystem, Browser, Region, TrafficType, TrafficType, BounceRates perlu dihilangkan karena setelah dilakukan hypothesis testing ternyata tidak begitu berpengaruh terhadap Revenue. Sedangkan BounceRates dihilangkan karena memiliki korelasi diatas 0.7 dengan ExitRates sehingga nilainya redundan.

### Feature extraction
Membuat Feature baru yaitu Average Time Page:
1. Average Time Page Administrative
2. Average Time Page Informational
3. Average Time Page ProductRelated

Average Time Page sendiri diambil dari nilai Page Duration/Page Value
```code
df_2['ATP_Administrative'] = df_2['Administrative_Duration']/df_2['Administrative']
df_2['ATP_Informational'] = df_2['Informational_Duration']/df_2['Informational']
df_2['ATP_ProductRelated'] = df_2['ProductRelated_Duration']/df_2['ProductRelated']
```

### Feature Tambahan
Additional Feature yang disarankan untuk membantu membuat performansi model semakin bagus yaitu:
1. Membership duration
2. Favourite category
3. Item bought per month
4. Item bought in price per month
