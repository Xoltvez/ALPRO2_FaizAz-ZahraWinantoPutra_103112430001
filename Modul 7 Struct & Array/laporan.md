<h1 align="center">Laporan Praktikum Modul 7  
<br>Struct & Array</h1>


<p align="center"> Faiz Az-Zahra Winanto Putra - 103112430001 </p>

### Dasar Teori 

**Struct** merupakan tipe data buatan sendiri yang digunakan untuk mengelompokkan sejumlah variabel dengan jenis data berbeda ke dalam satu entitas. Struct sangat berguna untuk mendeskripsikan suatu objek yang memiliki berbagai atribut atau karakteristik.

**Array** adalah sebuah koleksi elemen yang semuanya memiliki tipe data yang sama dan tersimpan dalam satu variabel. Di bahasa Go, ukuran array bersifat tetap dan harus ditentukan sejak awal deklarasi.

### Unguided

#### Soal Latihan Modul 7

##### Soal 1
>##### Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Gunakan tipe bentukan titik untuk menyimpan koordinat, dan tipe bentukan lingkaran untuk menyimpan titik pusat lingkaran dan radiusnya. 
>
>Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat. 
>
>Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".


Contoh :


| No  | Masukan                    | Keluaran                         |
| :-: | -------------------------- | :------------------------------- |
|  1  | 1 1 5<br>8 8 4<br>2 2      | Titik di dalam lingkaran 1       |
|  2  | 1 2 3<br>4 5 6<br>7 8      | Titik di dalam lingkaran 2       |
|  3  | 5 10 15<br>-15 4 20<br>0 0 | Titik di dalam lingkaran 1 dan 2 |


Fungsi untuk menghitung jarak titik (a, b) dan (c, d) dimana rumus jarak adalah:
```
							𝑗𝑎𝑟𝑎𝑘 = √(𝑎 − 𝑐)^2 + (𝑏 − 𝑑)^2
```
dan juga fungsi untuk menentukan posisi sebuah titik sembarang berada di dalam suatu lingkaran atau tidak.

```
function jarak(p, q : titik) -> real
{Mengembalikan jarak antara titik p(x,y) dan titik q(x,y)}

function didalam(c:lingkaran, p:titik) -> boolean
{Mengembalikan true apabila titik p(x,y) berada di dalam lingkaran c yang
memiliki titik pusat (cx,cy) dan radius r}
```

```go
package main
  

import (
    "fmt"
    "math"
)
  
type Titik struct {
    x, y int
}


type Lingkaran struct {
    pusat  Titik
    radius int
}
  

func jarak(p, q Titik) float64 {
    return math.Sqrt(math.Pow(float64(p.x-q.x), 2) + math.Pow(float64(p.y-q.y), 2))
}

  

func didalam(c Lingkaran, p Titik) bool {
    return jarak(c.pusat, p) <= float64(c.radius)
}

  
func posisiTitik(l1, l2 Lingkaran, p Titik) string {
    dalamL1 := didalam(l1, p)
    dalamL2 := didalam(l2, p)
  
    if dalamL1 && dalamL2 {
        return "Titik di dalam lingkaran 1 dan 2"
    } else if dalamL1 {
        return "Titik di dalam lingkaran 1"
    } else if dalamL2 {
        return "Titik di dalam lingkaran 2"
    } else {
        return "Titik di luar lingkaran 1 dan 2"
    }
}

  
func main() {
    var cx1, cy1, r1 int
    var cx2, cy2, r2 int
    var px, py int


    fmt.Scan(&cx1, &cy1, &r1)
    fmt.Scan(&cx2, &cy2, &r2)
    fmt.Scan(&px, &py)


    l1 := Lingkaran{Titik{cx1, cy1}, r1}
    l2 := Lingkaran{Titik{cx2, cy2}, r2}
    p := Titik{px, py}
  

    fmt.Println(posisiTitik(l1, l2, p))

}
```


![[Modul 7 Struct & Array/output/soal1.png]]

Program ini bertujuan untuk menentukan **posisi sebuah titik sembarang** terhadap dua lingkaran menggunakan **struct**. Program menerima input berupa koordinat titik pusat dan radius dari dua lingkaran, serta satu titik sembarang. Output yang dihasilkan berupa posisi titik terhadap lingkaran-lingkaran tersebut.

#### Struct yang digunakan

Struct titik 

```go
type Titik struct {
    x, y int
}
```

Struct `Titik` merepresentasikan koordinat 2 dimensi (x, y). Struct ini digunakan untuk menyimpan posisi titik maupun pusat lingkaran.

Struct Lingkaran

```go
type Lingkaran struct {
	pusat  Titik
	radius int
}
```
 
Struct Lingkaran berisi:
- `pusat`: sebuah `Titik`, menyatakan titik pusat lingkaran.
    
- `radius`: jari-jari lingkaran dalam satuan integer.


#### Fungsi yang digunakan

Fungsi Jarak 

```go
func jarak(p, q Titik) float64 {
    return math.Sqrt(float64((p.x-q.x)*(p.x-q.x) + (p.y-q.y)*(p.y-q.y)))
}
```

Fungsi ini menghitung **jarak Euclidean** antara dua titik `p` dan `q`, menggunakan rumus:

> √((x₂ - x₁)² + (y₂ - y₁)²)

Fungsi Didalam 

```go
func diDalam(c Lingkaran, p Titik) bool {
    return jarak(c.pusat, p) <= float64(c.radius)
}
```

Fungsi ini menentukan apakah **titik `p` berada di dalam lingkaran `c`**. Caranya:

- Menghitung jarak antara `p` dan pusat lingkaran `c`.
    
- Jika jaraknya **kurang dari atau sama dengan** jari-jari, berarti titik `p` berada di dalam lingkaran.

Fungsi PosisiTitik

```go
func posisiTitik(l1, l2 Lingkaran, p Titik) string {
	dalamL1 := didalam(l1, p)
	dalamL2 := didalam(l2, p)

	if dalamL1 && dalamL2 {
		return "Titik di dalam lingkaran 1 dan 2"
	} else if dalamL1 {
		return "Titik di dalam lingkaran 1"
	} else if dalamL2 {
		return "Titik di dalam lingkaran 2"
	} else {
		return "Titik di luar lingkaran 1 dan 2"
	}
}
```

Fungsi ini mengecek **posisi titik `p` terhadap dua lingkaran `l1` dan `l2`**, kemudian mengembalikan string yang menjelaskan posisi tersebut:

- Di dalam keduanya
    
- Hanya di dalam lingkaran 1
    
- Hanya di dalam lingkaran 2
    
- Di luar keduanya
##### Soal 2
>Sebuah array digunakan untuk menampung sekumpulan bilangan bulat. Buatlah program
yang digunakan untuk mengisi array tersebut sebanyak N elemen nilai. Asumsikan array
memiliki kapasitas penyimpanan data sejumlah elemen tertentu. Program dapat
menampilkan beberapa informasi berikut:

a. Menampilkan keseluruhan isi dari array.
b. Menampilkan elemen-elemen array dengan indeks ganjil saja.
c. Menampilkan elemen-elemen array dengan indeks genap saja (asumsi indek ke-0 adalah
genap).
d. Menampilkan elemen-elemen array dengan indeks kelipatan bilangan x. x bisa diperoleh
dari masukan pengguna.
e. Menghapus elemen array pada indeks tertentu, asumsi indeks yang hapus selalu valid.
Tampilkan keseluruhan isi dari arraynya, pastikan data yang dihapus tidak tampil
f. Menampilkan rata-rata dari bilangan yang ada di dalam array.
g. Menampilkan standar deviasi atau simpangan baku dari bilangan yang ada di dalam array
tersebut.
h. Menampilkan frekuensi dari suatu bilangan tertentu di dalam array yang telah diisi
tersebut


```go
package main
  

import (
    "fmt"
    "math"
)
  

func rataRata(arr []int) float64 {
    sum := 0
    for _, val := range arr {
        sum += val
    }
    return float64(sum) / float64(len(arr))
}

  


func standarDeviasi(arr []int) float64 {
    mean := rataRata(arr)
    var variance float64
    for _, val := range arr {
        variance += math.Pow(float64(val)-mean, 2)
    }
    variance /= float64(len(arr))
    return math.Sqrt(variance)
}

  

func frekuensi(arr []int, num int) int {
    count := 0
    for _, val := range arr {
        if val == num {
            count++
        }
    }
    return count
}

  
  
func hapusElemen(arr []int, index int) []int {
    return append(arr[:index], arr[index+1:]...)
}

  
func main() {
    var n, x, index, cari int
    fmt.Print("Masukkan jumlah elemen array: ")
    fmt.Scan(&n)
  
    arr := make([]int, n)
    fmt.Println("Masukkan elemen array:")
    for i := 0; i < n; i++ {
        fmt.Scan(&arr[i])
    }

  

    fmt.Println("Isi array:", arr)
    fmt.Print("Indeks ganjil: ")
    for i := 1; i < len(arr); i += 2 {
        fmt.Print(arr[i], " ")
    }
    fmt.Println()
    fmt.Print("Indeks genap: ")
    
    for i := 0; i < len(arr); i += 2 {
        fmt.Print(arr[i], " ")
    }
    fmt.Println()

    fmt.Print("Masukkan nilai x untuk kelipatan: ")
    fmt.Scan(&x)
    fmt.Print("Indeks kelipatan ", x, ": ")
    
    for i := x; i < len(arr); i += x {
        fmt.Print(arr[i], " ")
    }
    fmt.Println()

  
    fmt.Print("Masukkan indeks yang ingin dihapus: ")
    fmt.Scan(&index)
    arr = hapusElemen(arr, index)
    fmt.Println("Array setelah dihapus:", arr)
    fmt.Printf("Rata-rata: %.2f\n", rataRata(arr))
    fmt.Printf("Standar Deviasi: %.2f\n", standarDeviasi(arr))
    fmt.Print("Masukkan bilangan yang ingin dihitung frekuensinya: ")
    fmt.Scan(&cari)
    fmt.Printf("Frekuensi %d: %d\n", cari, frekuensi(arr, cari))
}
```

![[Modul 7 Struct & Array/output/soal2.png]]

Program ini digunakan untuk membuat sebuah array. Ketika program berjalan, program akan meminta untuk memasukan angka, yaitu untuk menentukan berapa banyak index yang akan ada di dalam array. Bisa dibilang sebagai kapasitas dari array yang akan dibuat. Kemudian, program akan meminta memasukan elemen ke dalam array yang telah terbuat, yaitu menggunakan perulangan. Akan ada inputan yang terus berulang hingga batasnya yaitu nilai yang dimasukan di awal program berjalan. Kemudian program akan bisa menghapus elemen yang ada dalam array, menampilkan nilai rata-rata dari nilai elemen array, menentukan elemen dengan kelipatan index tertentu, menampilkan nilai elemen berdasarkan genap atau ganjil index array, serta mencari frekuensi dari nilai yang diinginkan.


#### Fungsi yang digunakan

#### Fungsi ratarata
```go
func rataRata(arr []int) float64 {
    sum := 0
    for _, val := range arr {
        sum += val
    }
    return float64(sum) / float64(len(arr))
}
```

Menghitung **rata-rata (mean)** dari elemen-elemen dalam array.

##### Cara kerja fungsi rata rata :

- Menjumlahkan semua nilai array (`sum`).
    
- Membagi jumlah tersebut dengan jumlah elemen (`len(arr)`).
    
- Mengembalikan hasil sebagai `float64`.

#### Fungsi standarDeviasi
```go
func standarDeviasi(arr []int) float64 {
    mean := rataRata(arr)
    var variance float64
    for _, val := range arr {
        variance += math.Pow(float64(val)-mean, 2)
    }
    variance /= float64(len(arr))
    return math.Sqrt(variance)
}
```

Menghitung **standar deviasi**, yaitu seberapa menyebar data terhadap rata-ratanya.

##### Cara kerja fungsi standarDeviasi :

- Hitung **rata-rata** terlebih dahulu.
    
- Hitung jumlah kuadrat selisih tiap nilai dengan rata-rata (varian).
    
- Bagi total tersebut dengan panjang array (untuk varian).
    
- Ambil akar dari varian untuk mendapat **standar deviasi**.

#### Fungsi Frekuensi 
```go
func frekuensi(arr []int, num int) int {
    count := 0
    for _, val := range arr {
        if val == num {
            count++
        }
    }
    return count
}
```

Menghitung **berapa kali** angka tertentu (`num`) muncul dalam array.

##### Cara kerja fungsi frekuensi :

- Looping setiap elemen dalam array.
    
- Tambah `count` setiap kali ketemu `val == num`.

#### Frekuensi hapusElemen
```go
func frekuensi(arr []int, num int) int {
    count := 0
    for _, val := range arr {
        if val == num {
            count++
        }
    }
    return count
}
```

Menghapus elemen **berdasarkan index** dari array.

##### Cara kerja fungsi hapusElemen :

- Menggunakan `append` untuk menyambung:
    
    - `arr[:index]` (elemen sebelum index)
        
    - `arr[index+1:]` (elemen setelah index)
        
- Hasilnya adalah array baru tanpa elemen di posisi `index`.


#### Fungsi Main

Alur kerja pada fungsi main :

-**Input** jumlah elemen array dan nilainya dari user.
    
-**Cetak array** dan tampilkan elemen:
    
    - Pada indeks ganjil
        
    - Pada indeks genap
        
-**Input angka `x`**, lalu tampilkan elemen pada **indeks kelipatan `x`**.
    
-**Hapus elemen** pada indeks tertentu.
    
-Hitung dan tampilkan:
    
    - **Rata-rata** elemen array
        
    - **Standar deviasi**
        
    - **Frekuensi** dari angka yang dicari
##### Soal 3
>Sebuah program digunakan untuk menyimpan dan menampilkan nama-nama klub yang memenangkan pertandingan bola pada suatu grup pertandingan. Buatlah program yang digunakan untuk merekap skor pertandingan bola 2 buah klub bola yang berlaga.
>
>Pertama-tama program meminta masukan nama-nama klub yang bertanding, kemudian program meminta masukan skor hasil pertandingan kedua klub tersebut. Yang disimpan dalam array adalah nama-nama klub yang menang saja. 
>
>Proses input skor berhenti ketika skor salah satu atau kedua klub tidak valid (negatif). Di akhir program, tampilkan daftar klub yang memenangkan pertandingan. 
>
>Perhatikan sesi interaksi pada contoh berikut ini (teks bergaris bawah adalah input/read)

```
Klub A : MU

Klub B : Inter

Pertandingan 1 : 2 0 // MU = 2 sedangkan Inter = 0

Pertandingan 2 : 1 2

Pertandingan 3 : 2 2

Pertandingan 4 : 0 1

Pertandingan 5 : 3 2

Pertandingan 6 : 1 0

Pertandingan 7 : 5 2

Pertandingan 8 : 2 3

Pertandingan 9 : -1 2

Hasil 1 : MU

Hasil 2 : Inter

Hasil 3 : Draw

Hasil 4 : Inter

Hasil 5 : MU

Hasil 6 : MU

Hasil 7 : MU

Hasil 8 : Inter

Pertandingan selesai
```


```go
package main 

import "fmt"

func main() {
    var klubA, klubB string
  
    fmt.Print("Klub A: ")
    fmt.Scan(&klubA)

    fmt.Print("Klub B: ")
    fmt.Scan(&klubB)


    var pemenang []string

    pertandingan := 1
  
    for {
        var skorA, skorB int
        fmt.Printf("Pertandingan %d: ", pertandingan)
        fmt.Scan(&skorA, &skorB)
  
        if skorA < 0 || skorB < 0 {
            break
        }
  
        if skorA > skorB {
            pemenang = append(pemenang, klubA)
        } else if skorB > skorA {
            pemenang = append(pemenang, klubB)
        } else {
            pemenang = append(pemenang, "Draw")
        }
        pertandingan++
    }

    for i, hasil := range pemenang {
        fmt.Printf("Hasil %d: %s\n", i+1, hasil)
    }
    
    fmt.Println("Pertandingan selesai") 
}
```

![[Modul 7 Struct & Array/output/soal3.png]]

Program ini digunakan untuk **mencatat hasil pertandingan antara dua klub sepak bola** sebanyak yang diinginkan user, sampai skor negatif dimasukkan sebagai sinyal untuk berhenti. Setelah itu, program akan mencetak hasil pemenang dari setiap pertandingan.

Array yang digunakan 

```go
var pemenang []string
pertandingan := 1
```

- `pemenang` adalah **slice** untuk menyimpan hasil tiap pertandingan (klub pemenang atau "Draw").
    
- `pertandingan` menyimpan **nomor pertandingan** saat ini.

Kemudian ada percabangan yaitu:

```go
 if skorA > skorB {
        pemenang = append(pemenang, klubA)
    } else if skorB > skorA {
        pemenang = append(pemenang, klubB)
    } else {
        pemenang = append(pemenang, "Draw")
    }
```

Disinilah skor akan diperiksa yang kemudian akan menyimpan klub mana yang menang atau draw. Jadi hanya yang menang saja yang akan disimpan.

```go
for i, hasil := range pemenang {
    fmt.Printf("Hasil %d: %s\n", i+1, hasil)
}
```
##### Soal 4
>Sebuah array digunakan untuk menampung sekumpulan karakter, Anda diminta untuk membuat sebuah subprogram untuk melakukan membalikkan urutan isi array dan memeriksa apakah membentuk palindrom.

```go
package main

import "fmt"
  
const NMAX int = 127
  
type tabel [NMAX]rune 
var tab tabel
var m int
  

func isiArray(t *tabel, n *int) {
    *n = 0
    for *n < NMAX {
        var c rune
        fmt.Scanf("%c", &c)
        if c == '.' {
            break
        }
        t[*n] = c
        *n++
    }
}

  
func cetakArray(t tabel, n int) {
    for i := 0; i < n; i++ {
        fmt.Printf("%c ", t[i])
    }
    fmt.Println()
}

  
func balikanArray(t *tabel, n int) {
    var temp rune
    for i := 0; i < n/2; i++ {
        temp = t[i]
        t[i] = t[n-1-i]
        t[n-1-i] = temp
    }
}

  

func palindrom(t tabel, n int) bool {
    for i := 0; i < n/2; i++ {
        if t[i] != t[n-1-i] {
            return false
        }
    }
    return true
}


func main() {
    isiArray(&tab, &m)
  
    fmt.Println("Teks: ")
    cetakArray(tab, m)

    balikanArray(&tab, m)

    fmt.Println("Reverse teks: ")
    cetakArray(tab, m)


    if palindrom(tab, m) {
        fmt.Println("Palindrom : true")
    } else {
        fmt.Println("Palindrom : false")
    }
}
```

![[Modul 7 Struct & Array/output/soal4.png]]

Program ini dibuat menggunakan bahasa pemrograman Go untuk mengolah karakter dalam array. Program menerima input berupa karakter hingga menemukan tanda titik (.), lalu menyimpan karakter tersebut dalam array bertipe `rune`. Setelah itu, program mencetak karakter yang telah dimasukkan, membalik urutannya, dan memeriksa apakah karakter tersebut membentuk palindrom atau tidak. Program ini menggunakan konsep fungsi untuk memisahkan tugas-tugas utama, seperti mengisi array, mencetak array, membalik array, dan memeriksa palindrom.

#### Fungsi yang digunakan :

#### Fungsi isiArray

```go
func isiArray(t *tabel, n *int) {
	*n = 0
	for *n < NMAX {
		var c rune
		fmt.Scanf("%c", &c)
		if c == '.' {
			break
		}
		t[*n] = c
		*n++
	}
}
```

- Membaca karakter satu per satu menggunakan `Scanf`.
    
- Simpan ke array `t` sampai ditemukan karakter `'.'`.
    
- Jumlah karakter yang dibaca disimpan ke `n`.

#### Fungsi cetakArray

```go
func cetakArray(t tabel, n int) {
	for i := 0; i < n; i++ {
		fmt.Printf("%c ", t[i])
	}
	fmt.Println()
}
```

- Menampilkan semua elemen array sebagai karakter.
    
- Dipakai untuk menampilkan teks normal atau teks yang sudah dibalik.

#### Fungsi balikanArray

```go
func balikanArray(t *tabel, n int) {
	var temp rune
	for i := 0; i < n/2; i++ {
		temp = t[i]
		t[i] = t[n-1-i]
		t[n-1-i] = temp
	}
}
```

- Membalik isi array `t` secara in-place (tanpa membuat array baru).
    
- Tukar elemen dari ujung ke tengah.

#### Fungsi palindrom
```go
func palindrom(t tabel, n int) bool {
	for i := 0; i < n/2; i++ {
		if t[i] != t[n-1-i] {
			return false
		}
	}
	return true
}
```

- Mengecek apakah isi array `t` merupakan palindrom.
    
- Jika karakter pertama sama dengan terakhir, kedua sama dengan kedua terakhir, dst., maka true.

##### Kesimpulan :

Program ini bertujuan untuk **membaca sekumpulan karakter** dari input pengguna hingga karakter titik (`.`) dimasukkan, lalu melakukan tiga hal utama:

1. **Menampilkan isi karakter yang dimasukkan.**
    
2. **Membalik urutan karakter tersebut.**
    
3. **Menentukan apakah karakter tersebut membentuk palindrom** (sama dibaca dari depan maupun belakang).