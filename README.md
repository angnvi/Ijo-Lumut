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
