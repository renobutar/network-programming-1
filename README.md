## 1. TCP Connection

Diagram TCP finite state machine merupakan diagram yang menjelaskan alur terjadinya three way handshake pada saat pembuatan koneksi TCP. Starting point berada pada state CLOSED ketika belum ada koneksi.

### Client
1. Client mengirim SYN (SYN SENT)
2. Client menerima SYN dan ACK, kemudian mengirim ACK (CONNECTION ESTABLISHED)
3. Client mengirimkan FIN (FIN WAIT 1)
4. Client menerima ACK (FIN WAIT 2) 
5. Client menerima FIN dan mengirim ACK (TIME WAIT)
6. Terjadi timeout, maka koneksi berakhir (CLOSED)

### Server
1. Server membuat koneksi secara passive open (LISTEN)
2. Server menerima SYN, kemudian mengirim SYN, ACK (SYN RCVD)
3. Server menerima ACK (CONNECTION ESTABLISHED)
4. Server menerima FIN, kemudian mengirimkan ACK (CLOSE WAIT)
5. Server mengirim FIN (LAST ACK)
6. Server mengakhiri koneksi (CLOSED)

## 2. For

### Kode Program
```go
package main
import "fmt"

func main() {
	i := 1
	for i <= 3 {
		fmt.Println(i)
		i = i + 1
	}

	for j := 7; j <= 9; j++ {
		fmt.Println(i)
	}

	for {
		fmt.Println("loop")
		break
	}

	for n := 0; n <= 5; n++ {
		if n%2 == 0 {
			continue
		}
		fmt.Println(n)
	}
}
```
* For merupakan instruksi untuk melakukan perulangan sesuai dengan kondisi yang ditentukan
* Perulangan for dapat berhenti apabila kondisi sudah false, atau jika ada break
* Perulangan for juga dapat di-skip dengan menggunakan continue


### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/for.png)


## If-Else

### Kode Program
```go
package main

import "fmt"

func main() {
	if 7%2 == 0 {
		fmt.Println("7 is even")
	} else {
		fmt.Println("7 is odd")
	}

	if 8%4 == 0 {
		fmt.Println("8 is divisible by 4")
	}

	if num := 9; num < 0 {
		fmt.Println("is negative")
	} else if num < 10 {
		fmt.Println(num, "has 1 digit")
	} else {
		fmt.Println(num, "has multiple digits")
	}
}
```
* If akan dijalankan jika kondisinya true
* Jika kondisi if false, maka akan berlanjut ke else if setelahnya
* Jika semua if kondisinya false, maka yang dijalankan adalah else


### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/if-else.png)


## 3. Array

### Kode Program
```go
package main

import "fmt"

func main() {
	var a [5]int
	fmt.Println("emp:", a)

	a[4] = 100
	fmt.Println("set:", a)
	fmt.Println("get:", a[4])

	fmt.Println("len:", len(a))

	b := [5]int{1, 2, 3, 4, 5}
	fmt.Println("dcl", b)

	var twoD [2][3]int
	for i := 0; i < 2; i++ {
		for j := 0; j < 3; j++ {
			twoD[i][j] = i + j
		}
	}
	fmt.Println("2d:", twoD)
}
```
* Array merupakan sekumpulan variabel yang memiliki tipe data yang sama
* Array mempunyai indeks untuk menentukan nilainya
* Panjang dari suatu array dapat diketahui dengan fungsi ````len(variabelArray)````
* Array bisa berbentuk 2 dimensi atau lebih

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/array.png)


## Function

### Kode Program
```go
package main

import "fmt"

func plus(a int, b int) int {
	return a + b
}

func plusPlus(a, b, c int) int {
	return a + b + c
}

func main() {
	res := plus(1, 2)
	fmt.Println("1+2 =", res)

	res = plusPlus(1, 2, 3)
	fmt.Println("1+2+3 =", res)
}
```
* Function adalah sekumpulan pernyataan yang akan dijalankan jika namanya dipanggil
* Function dapat mengembalikan bermacam-macam tipe data

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/function.png)


## 4. Struct

### Kode Program
```go
package main

import "fmt"

type person struct {
	name string
	age  int
}

func main() {
	fmt.Println(person{"Bob", 20})

	fmt.Println(person{name: "Alice", age: 30})

	fmt.Println(person{name: "Fred"})

	fmt.Println(&person{name: "Ann", age: 40})

	s := person{name: "Sean", age: 50}
	fmt.Println(s.name)

	sp := &s
	fmt.Println(sp.age)

	sp.age = 51
	fmt.Println(sp.age)
}
```
* Struct adalah instruksi untuk membuat tipe data bentukan
* Sebuah struct bisa mempunyai berbagai variabel yang tipe datanya berbeda
* Jika pada saat pemanggilan struct terdapat variabel yang tidak didefinisikan nilainya, maka nilainya menjadi 0 atau nil

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/struct.png)


## Method

### Kode Program
```go
package main

import "fmt"

type rect struct {
	width, height int
}

func (r *rect) area() int {
	return r.width * r.height
}

func (r rect) perim() int {
	return 2*r.width + 2*r.height
}

func main() {
	r := rect{width: 10, height: 5}

	fmt.Println("area:", r.area())
	fmt.Println("perim:", r.perim())

	rp := &r
	fmt.Println("area:", rp.area())
	fmt.Println("perim:", rp.perim())
}
```
* Method adalah fungsi yang memiliki akses ke properti struct
* Perbedaannya dengan fungsi, pada saat deklarasi method ditentukan struct dari method tersebut
* Untuk memanggilnya juga harus diawali dengan variabel struct terlebih dahulu

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/method.png)


## 5. Multiple Return Value

### Kode Program
```go
package main

import "fmt"

func vals() (int, int) {
	return 3, 7
}

func main() {
	a, b := vals()
	fmt.Println(a)
	fmt.Println(b)

	_, c := vals()
	fmt.Println(c)
}
```
* Pada bahasa Go, fungsi dapat mengembalikan lebih dari 1 nilai

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/multiple-return-value.png)


## Command Line

### Kode Program
```go
package main

import (
	"flag"
	"fmt"
)

func main() {
	wordPtr := flag.String("word", "foo", "a string")

	numbPtr := flag.Int("numb", 42, "an int")
	boolPtr := flag.Bool("fork", false, "a bool")

	var svar string
	flag.StringVar(&svar, "svar", "bar", "a string var")

	flag.Parse()

	fmt.Println("word:", *wordPtr)
	fmt.Println("numb:", *numbPtr)
	fmt.Println("fork", *boolPtr)
	fmt.Println("svar:", svar)
	fmt.Println("tail:", flag.Args())
}
```

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/command-line.png)


## 6. Simple Web Application

### Kode Program
```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprint(w, "Hello, you've requested: %s\n", r.URL.Path)
	})

	http.ListenAndServe(":8000", nil)
}
```

* Go bisa digunakan untuk membuat aplikasi web
* HandleFunc berfungsi untuk menentukan route dan menentukan konten web ketika alamat diakses
* ListenAndServe berfungsi menentukan port dan menjalankan aplikasi pada port yang ditentukan

### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/web-application.png)



## 7. Simple Web Application using Config (Viper)

### Kode Program
````go
package main

import (
	"fmt"
    "html"
    "github.com/spf13/viper"
    "net/http"
)

func main() {
	// Set lokasi file config
	viper.SetConfigFile("./config/env.json")
	
	// Tampilkan error jika file config tidak ditemukan
	if err := viper.ReadInConfig(); err != nil {
		fmt.Println("Error reading config file, %s", err)
	}
	
	// Set route dan konten ketika web diakses
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello, you've requested: %q", html.EscapeString(r.URL.Path))
	})

	// Jalankan server di port yang sudah di-set config
	http.ListenAndServe(":" + viper.GetString("server.port"), nil)
}
````

Untuk membuat config dengan library viper, pertama-tama harus menginstal library tersebut pada Go dengan cara menuliskan perintah berikut pada terminal
````
go get -u github.com/spf13/viper
````
Jika sudah terinstal, import library viper pada file .go kita
````go
import (
    "github.com/spf13/viper"
)
````
Setelah di-import, buat file config dengan format .json
````json
{
    "appName": "Web Application",

    "server": {
        "port": 8000
    }
}
````
Definisikan lokasi file config yang sudah dibuat dengan perintah ````viper.SetConfigFile````
````go
viper.SetConfigFile("./config/env.json")
````
Untuk mengambil nilai dari file config, gunakan perintah ````viper.GetString````
````go
viper.GetString("server.port")
````


### Hasil Program
![for](https://raw.githubusercontent.com/adityaeka26/network-programming-1/master/Screenshot/web-application-viper.png)