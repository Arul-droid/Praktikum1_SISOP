# Laporan Praktikum1_SISOP

## Soal 1 (Argo Ngawi Jes Ngejes)
pada soal no 1 kami ditugaskan untuk membuat sebuah script AWK untuk menganalisa sebuah gerbong kereta.

### Mendownload file CSV
yang pertama kali yang harus kita lakukan adalah mendownload file csv ke ke dalam directory menggunakan terminal.

Maka dari itu kita perlu membuat sebuah script untuk downloadnya.

```bash
wget -O passenger.csv "https://docs.google.com/spreadsheets/d/1NHmyS6wRO7To7ta-NLOOLHkPS6valvNaX7tawsv1zfE/export?format=csv&gid=0"
```
setelah mendownload file tersebut ke dalam directory soal 1 baru kita bisa memulai membuat script analisanya.

### Memulai script analisa
#### Membuat perintah untuk input

pada soalnya diberikan beberapa subsoal untuk dikerjakan dari a hingga e.

yang dimana nanti cara untuk menjalankan script awknya adalah memberikan input sesuai dengan subsoal yang ada.

seperti:

```bash
awk -f KANJ.sh passenger.csv a   # total penumpang
awk -f KANJ.sh passenger.csv b   # jumlah gerbong
awk -f KANJ.sh passenger.csv c   # penumpang tertua
awk -f KANJ.sh passenger.csv d   # rata-rata usia
awk -f KANJ.sh passenger.csv e   # jumlah business class
```
agar dapat menjalankan script itu kita perlu membuat file .sh nya terlebih dahulu dengan

```bash
nano KANJ.sh
```

kemudian kita isi file tersebut dengan script awk.

pertama kita perlu menulis kode untuk inputnya dengan

```bash
BEGIN {
    FS = ","
    opsi = ARGV[2]
    ARGC = 2
}
```

Ini adalah blok `BEGIN` di awk script. Dijalankan sekali sebelum membaca file CSV.

`FS = ","` Menset pemisah kolom (Field Separator) menjadi koma, karena file CSV dipisahkan dengan koma. Tanpa ini, awk akan pakai spasi sebagai pemisah default.

`opsi = ARGV[2]` Mengambil argumen ketiga dari command line dan menyimpannya ke variabel opsi.

```bash
awk -f KANJ.sh passenger.csv a
```
```bash
Maka:

ARGV[0] = "awk"
ARGV[1] = "passenger.csv"
ARGV[2] = "a"          ← disimpan ke opsi
```

`ARGC = 2`
Membatasi jumlah argumen yang diproses awk menjadi 2 saja (awk dan passenger.csv).
Tanpa ini, awk akan mencoba membuka "a" sebagai file karena mengira itu nama file kedua, lalu error karena file "a" tidak ada.

#### Masuk ke subsoal
##### Soal a
Pada soal a kami ditugaskan untuk menghitung jumlah seluruh penumpang kereta.

dengan contoh output:
```bash
Jumlah seluruh penumpang KANJ adalah ${coutn_passenger} orang
```
untuk itu kita perlu menulis script
```bash
END {
    count = NR - 1
    if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"
}
```
`END` merupakan block kode yang dijalankan setelah semua baris telah dibaca
`count = NR-1` menyimpan semua baris kecuali baris pertama kedalam variabel count
`if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"` akan mengeprint 

```bash
Jumlah seluruh penumpang KANJ adalah 208 orang
```
jika memilih opsi a.

##### soal b
Pada soal b kami ditugaskan untuk menghitung jumlah gerbong kereta.

dengan contoh output:
```bash
Jumlah gerbong penumpang KANJ adalah ${carriege}
```
untuk itu kita perlu menulis script
```bash
NR > 1 {
    # b: hitung gerbong unik
    gsub(/\r/, "")      # hapus karakter windows (penyebab umum)
    gsub(/ /, "", $4)
    gerbong[$4] = 1
}

END {
    else if (opsi == "b") print "Jumlah gerbong penumpang KANJ adalah", length(gerbong)
}
```



`END` merupakan block kode yang dijalankan setelah semua baris telah dibaca
`else if (opsi == "b") print "Jumlah gerbong penumpang KANJ adalah", length(gerbong)` akan mengeprint 

```bash
Jumlah gerbong penumpang KANJ adalah 4
```
jika memilih opsi b.

##### soal c
Pada soal a kami ditugaskan untuk menghitung jumlah seluruh penumpang kereta.

dengan contoh output:
```bash
Jumlah seluruh penumpang KANJ adalah ${coutn_passenger} orang
```
untuk itu kita perlu menulis script
```bash
END {
    count = NR - 1
    if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"
}
```
`END` merupakan block kode yang dijalankan setelah semua baris telah dibaca
`count = NR-1` menyimpan semua baris kecuali baris pertama kedalam variabel count
`if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"` akan mengeprint 

```bash
Jumlah seluruh penumpang KANJ adalah 208 orang
```
jika memilih opsi a.

##### soal d
Pada soal a kami ditugaskan untuk menghitung jumlah seluruh penumpang kereta.

dengan contoh output:
```bash
Jumlah seluruh penumpang KANJ adalah ${coutn_passenger} orang
```
untuk itu kita perlu menulis script
```bash
END {
    count = NR - 1
    if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"
}
```
`END` merupakan block kode yang dijalankan setelah semua baris telah dibaca
`count = NR-1` menyimpan semua baris kecuali baris pertama kedalam variabel count
`if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"` akan mengeprint 

```bash
Jumlah seluruh penumpang KANJ adalah 208 orang
```
jika memilih opsi a.

##### soal e
Pada soal a kami ditugaskan untuk menghitung jumlah seluruh penumpang kereta.

dengan contoh output:
```bash
Jumlah seluruh penumpang KANJ adalah ${coutn_passenger} orang
```
untuk itu kita perlu menulis script
```bash
END {
    count = NR - 1
    if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"
}
```
`END` merupakan block kode yang dijalankan setelah semua baris telah dibaca
`count = NR-1` menyimpan semua baris kecuali baris pertama kedalam variabel count
`if (opsi == "a") print "Jumlah seluruh penumpang KANJ adalah", count, "orang"` akan mengeprint 

```bash
Jumlah seluruh penumpang KANJ adalah 208 orang
```
jika memilih opsi a.

##### jika memilih selain a hingga e


## Soal 2 (Ekspedisi Gunung Kawi)
Script bash untuk parsing koordinat dari file JSON.

## Soal 3 (Kost Slebew)
Script bash untuk manajemen kost berbasis CLI.
