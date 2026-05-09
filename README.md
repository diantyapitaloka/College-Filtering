## 🍦🍧🍪 College-Filtering 🍪🍧🍦
- Filtering in a data frame is efficiently handled by using the %in% operator for matching. This operator allows you to check if values in a column exist within a specific input vector.
- The input vector serves as a collection of target values you wish to extract. It typically consists of several alliances or group names defined as strings.
- When the operation runs, it returns a logical vector of TRUE and FALSE values. These boolean results determine which rows of the data frame should be retained.
- This method is much cleaner than chaining multiple OR statements together. It streamlines your code and makes it significantly easier for others to read.
- Naming your vector clearly helps document the specific purpose of the filter. It allows future users to understand exactly which group of colleges is being analyzed.
- You apply the logical results to the data frame index to created a subset. This process ensures that only the colleges belonging to your specified alliances remain.
- The vector can be saved as a separate variable to make your filtering process more dynamic. This allows you to update the list of alliances without rewriting the main logic.
- Strings within your vector must match the data frame entries exactly regarding capitalization. Even a small typo or case mismatch will result in that specific row being excluded.
- Using specialized operators like %in% is generally faster than manual loops for large datasets. It leverages optimized internal functions to scan your data frame rapidly.

## 🍦🍧🍪 Code 🍪🍧🍦
- Grafiknya sama dengan subbab "Tren Jumlah Mahasiswa dari Tahun ke Tahun" tapi sudah dengan filter dua fakultas, yaitu "ICT" dan "Ilmu Komunikasi".
- Hal ini dapat terjadi karena ada filtering yang dinyatakan oleh perintah berikut.
- Di sini summarybyfakultas$fakultas %in%c("ICT", "Ilmu Komunikasi") artinya melakukan filter data yang ada di kolom fakultas dari data frame summarybyfakultas.
- Sedangkan perintah lengkap summarybyfakultas[summarybyfakultas$fakultas %in%c("ICT", "Ilmu Komunikasi"),] artinya mengambil data yang sudah terfilter untuk seluruh kolom.

```
library("ggplot2")
library("openxlsx")

#Membaca file mahasiswa.xlsx
mahasiswa <- read.xlsx("https://storage.googleapis.com/dqlab-dataset/mahasiswa.xlsx",sheet = "Sheet 1")

#Menghitung Jumlah Data by Fakultas
summarybyfakultas <- aggregate(x=mahasiswa$JUMLAH, by=list(Kategori=mahasiswa$Fakultas, Tahun=mahasiswa$ANGKATAN), FUN=sum)
summarybyfakultas <- setNames(summarybyfakultas, c("fakultas","tahun", "jumlah_mahasiswa"))
summarybyfakultas

summarybyfakultas$tahun = as.factor(summarybyfakultas$tahun)
summarybyfakultas[summarybyfakultas$fakultas %in% c("ICT", "Ilmu Komunikasi"),]

ggplot(summarybyfakultas[summarybyfakultas$fakultas %in% c("ICT", "Ilmu Komunikasi"),], aes(x=fakultas, y=jumlah_mahasiswa)) + 
  geom_bar(stat = "identity", aes(fill = tahun), width=0.8, position = position_dodge(width=0.8)) + 
  theme_classic() 
```

## 🍦🍧🍪 Result 🍪🍧🍦


![image](https://github.com/diantyapitaloka/College-Filtering/assets/147487436/ea28b451-aab6-4615-b560-1f9d9afe0b6d)


## 🍦🍧🍪 Copyright 🍪🍧🍦
By Diantya Pitaloka
