
<h1 align="center">Laporan Praktikum Modul 10  
<br>PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA</h1>


<p align="center"> Faiz Az-Zahra Winanto Putra - 103112430001 </p>

### Dasar Teori 

Pencarian adalah suatu proses yang lazim dilakukan di dalam kehidupan sehari-hari. Contoh penggunaannya dalam kehidupan nyata sangat beragam, misalnya pencarian file di dalam directory komputer, pencarian suatu teks di dalam sebuah dokumen, pencarian buku pada rak buku, dan contoh lainnya. Pertama pada modul ini akan dipelajari salah satu algoritma pencarian nilai terkecil atau terbesar pada sekumpulan data, atau biasa disebut pencarian nilai ekstrim

### Unguided

#### Soal Latihan Modul 10

##### Soal 1
>Sebuah program digunakan untuk mendata berat anak kelinci yang akan dijual ke pasar. Program ini menggunakan array dengan kapasitas 1000 untuk menampung data berat anak kelinci yang akan dijual. 
>
>Masukan terdiri dari sekumpulan bilangan, yang mana bilangan pertama adalah bilangan bulat N yang menyatakan banyaknya anak kelinci yang akan ditimbang beratnya. Selanjutnya N bilangan riil berikutnya adalah berat dari anak kelinci yang akan dijual. 
>
>Keluaran terdiri dari dua buah bilangan riil yang menyatakan berat kelinci terkecil dan terbesar


```go
package main 

import "fmt"
  

type arrKelinci []float64 
func main() {
    var n int
    var kelinci arrKelinci


    fmt.Print("Masukkan jumlah anak kelinci yang ada di array: ")
    fmt.Scan(&n)

  
    if n > 1000 {
        fmt.Println("Kapasitas maksimal adalah 1000 data")
        return
    }

  
    for i := 0; i < n; i++ {
        var berat float64
        fmt.Print("Data ke-", i+1, ": ")
        fmt.Scan(&berat)
        kelinci = append(kelinci, berat)
    }


    max := kelinci[0]
    min := kelinci[0]

   
    for i := 1; i < n; i++ {
        if kelinci[i] > max {
            max = kelinci[i]
        } else if kelinci[i] < min {
            min = kelinci[i]
        }
    }


    fmt.Println("Data Terbesar: ", max)
    fmt.Println("Data Terkecil: ", min)
}
```


![[Modul 10 PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA/output/soal1.png]]

Program di atas digunakan untuk membantu pengguna mengetahui nilai maksimum dan minimum dari sekumpulan berat anak kelinci secara sederhana dan efisien.

Penjelasan:

1. **Deklarasi Tipe Data**  
    Program membuat tipe `arrKelinci` sebagai slice bertipe `float64` untuk menyimpan data berat anak kelinci.
    
2. **Input Jumlah Data**  
    Pengguna diminta memasukkan jumlah anak kelinci. Jika jumlah melebihi 1000, program akan menghentikan proses dan menampilkan peringatan.
    
3. **Input Berat Tiap Kelinci**  
    Program melakukan perulangan sebanyak jumlah data, meminta input berat tiap anak kelinci, lalu menyimpannya ke dalam slice.
    
4. **Proses Pencarian Nilai Maksimum dan Minimum**  
    Dengan membandingkan setiap elemen di slice, program mencari berat terbesar (`max`) dan terkecil (`min`).
    
5. **Output Hasil**  
    Program menampilkan berat anak kelinci terbesar dan terkecil di layar.


##### Soal 2
>Sebuah program digunakan untuk menentukan tarif ikan yang akan dijual ke pasar. Program ini menggunakan array dengan kapasitas 1000 untuk menampung data berat ikan yang akan dijual. 
>
>Masukan terdiri dari dua baris, yang mana baris pertama terdiri dari dua bilangan bulat x dan y. Bilangan x menyatakan banyaknya ikan yang akan dijual, sedangkan y adalah banyaknya ikan yang akan dimasukan ke dalam wadah. Baris kedua terdiri dari sejumlah x bilangan riil yang menyatakan banyaknya ikan yang akan dijual. 
>
>Keluaran terdiri dari dua baris. Baris pertama adalah kumpulan bilangan riil yang menyatakan total berat ikan di setiap wadah (jumlah wadah tergantung pada nilai x dan y, urutan ikan yang dimasukan ke dalam wadah sesuai urutan pada masukan baris ke-2). Baris kedua adalah sebuah bilangan riil yang menyatakan berat rata-rata ikan di setiap wadah


```go
package main

import "fmt"


type arrIkan []float64  

func main() {
    var x, y int
    var ikan arrIkan


    fmt.Print("Masukkan jumlah ikan yang akan dijual (x) dan jumlah ikan per wadah (y): ")
    fmt.Scan(&x, &y)


    if x > 1000 {
        fmt.Println("Kapasitas maksimal adalah 1000 data")
        return
    }

    fmt.Println("Masukkan berat setiap ikan: ")

    for i := 0; i < x; i++ {
        var berat float64
        fmt.Print("Berat ikan ke-", i+1, ": ")
        fmt.Scan(&berat)
        ikan = append(ikan, berat)
    }

  

    var totalWadah []float64
    var totalSemua, total float64
    var jumlahWadah int

  
    for i := 0; i < x; i += y {
        total = 0
        for j := i; j < i+y && j < x; j++ {
            total += ikan[j]
        }

        totalWadah = append(totalWadah, total)
        totalSemua += total
        jumlahWadah++
    }

    fmt.Println("Total berat ikan di setiap wadah:")
    
    for i := 0; i < len(totalWadah); i++ {
        fmt.Printf("%.1f ", totalWadah[i])
    }
    fmt.Println()
    
    rataRata := totalSemua / float64(jumlahWadah)

    fmt.Printf("Rata-rata berat ikan per wadah: %.2f\n", rataRata)
}
```

![[Modul 10 PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA/output/soal2.png]]

Program ini menghitung total dan rata-rata berat ikan per wadah. Pengguna memasukkan jumlah ikan dan jumlah ikan per wadah, lalu berat masing-masing ikan. Program mengelompokkan ikan ke dalam wadah sesuai kapasitas, menghitung total berat tiap wadah, dan menampilkan rata-ratanya.


##### Soal 3
>Pos Pelayanan Terpadu (posyandu) sebagai tempat pelayanan kesehatan perlu mencatat data berat balita (dalam kg). Petugas akan memasukkan data tersebut ke dalam array. Dari data yang diperoleh akan dicari berat balita terkecil, terbesar, dan reratanya. 
>
>Buatlah program dengan spesifikasi subprogram sebagai berikut:

```
type arrBalita [100]float64 

func hitungMinMax(arrBerat arrBalita; bMin, bMax *float64) 
{ /* I.S. Terdefinisi array dinamis arrBerat 
  Proses: Menghitung berat minimum dan maksimum dalam array 
  F.S. Menampilkan berat minimum dan maksimum balita */ 
	... 
} 

function rerata (arrBerat arrBalita) real { 
/* menghitung dan mengembalikan rerata berat balita dalam array */ 
	... 
}
```

```go
package main

import "fmt"


type arrBalita []float64
  

func hitungMinMax(arrBerat arrBalita, bMin, bMax *float64) {
    *bMin = arrBerat[0]
    *bMax = arrBerat[0]

  
    for i := 1; i < len(arrBerat); i++ {
        if arrBerat[i] < *bMin {
            *bMin = arrBerat[i]
        }
        if arrBerat[i] > *bMax {
            *bMax = arrBerat[i]
        }
    }
}
  

func rerata(arrBerat arrBalita) float64 {
    var total float64
    for i := 0; i < len(arrBerat); i++ {
        total += arrBerat[i]
    }
    return total / float64(len(arrBerat))
}

  
func main() {
    var (
        n        int
        array    arrBalita
        berat    float64
        min, max float64
    )

    fmt.Print("Masukan banyak data berat balita : ")
    fmt.Scan(&n)

  
    for i := 0; i < n; i++ {
        fmt.Printf("Masukan berat balita ke-%d: ", i+1)
        fmt.Scan(&berat)
        array = append(array, berat)
    }
  

    hitungMinMax(array, &min, &max)
    avg := rerata(array)


    fmt.Printf("Berat balita minimum: %.2f kg\n", min)
    fmt.Printf("Berat balita maksimum: %.2f kg\n", max)
    fmt.Printf("Rerata berat balita: %.2f kg\n", avg)

}
```

![[Modul 10 PENCARIAN NILAI EKSTRIM PADA HIMPUNAN DATA/output/soal3.png]]

Program ini dibuat menggunakan bahasa Go dan bertujuan untuk **mengolah data berat badan balita**. Program meminta pengguna untuk memasukkan sejumlah data berupa berat badan balita, kemudian menyimpannya dalam sebuah slice bertipe `float64` yang dinamakan `arrBalita`.

Setelah seluruh data dimasukkan, program memanggil dua fungsi:

1. **`hitungMinMax`**  
    Fungsi ini menerima slice data berat dan dua pointer (`bMin` dan `bMax`) untuk menyimpan hasil berat minimum dan maksimum. Fungsi melakukan perulangan untuk membandingkan setiap nilai dan memperbarui nilai minimum dan maksimum.
    
2. **`rerata`**  
    Fungsi ini menghitung total dari semua berat balita dalam slice, kemudian membaginya dengan jumlah data untuk mendapatkan rata-rata berat.
    


