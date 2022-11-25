# Ijo-Lumut
Final Project Bootcamp Rakamin DS batch 27
## Descriptive Analysis

A. Terdapat kolom dengan tipe data yang tidak sesuai diantaranya <br>
- OperatingSystems <br> 
- Browser <br>
- Region <br>
- TrafficType <br>

Nilai 
''code
df = df.astype({'OperatingSystems': object, 'Browser': object, 'Region': object, 'TrafficType': object})
''

B. Tidak terdapat nilai kosong pada tiap-tiap kolom <br>

C. Terdapat nilai outlier di beberapa kolom seperti di kolom Informational, Informational_Duration, Page Values, Special Day
