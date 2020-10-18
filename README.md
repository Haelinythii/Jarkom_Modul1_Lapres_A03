# Jarkom_Modul1_Praktikum_A03

## **Soal 1**
**1. Sebutkan webserver yang digunakan pada "testing.mekanis.me"!**

Untuk melihat webservernya, pertama kita harus mencari request http yang dikirimkan kepada kita, kemudian mem follow TCP stream nya. Webserver dapat dilihat dibagian server: ..., seperti gambar yang ada dibawah

Display filter yang digunakan adalah ```http.host == "testing.mekanis.me"```

![gambar display filter no 1](/images/no1Filter.png)

![gambar TCP Stream no 1](/images/no1TCPStream.png)

Bisa dilihat bahwa testing.mekanis.me menggunakan webserver nginx/1.14.1 (Ubuntu).

## **Soal 2**
**2. Simpan gambar "Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg"!**

Untuk menyimpan gambar "Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg", pertama, pada display filter kita gunakan

```http.request.method == GET```

![2_1](https://user-images.githubusercontent.com/61625353/96361137-6c2d6380-114d-11eb-8cbf-c7a6674b1053.png)

untuk menampilkan data yang dikirimkan ke kita. Kemudian kita cari file gambar yang diinginkan.

Selain itu, kita juga bisa menggunakan Export Object. Pada text filter masukkan nama file [Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436],
Kemudian save.

![2_2](https://user-images.githubusercontent.com/61625353/96361146-7fd8ca00-114d-11eb-8648-c6a52e9f93df.png)

Berikut adalah gambar yang dimaksud

Tim_Kunjungan_Kerja_BAKN_DPR_RI_ke_Sukabumi141436.jpg

![2_3](https://user-images.githubusercontent.com/61625353/96361418-abf54a80-114f-11eb-8fee-d1d22723e4ca.jpg)


## **Soal 3**
**3. Cari username dan password ketika login di "ppid.dpr.go.id"!**

Untuk mencari user dan password, kita bisa mencari dengan request http dengan method POST. Namun karena kita hanya ingin mendapat yang login di "ppid.dpr.go.id", kita harus menambahkan http host nya juga.

Sehingga, display filternya menjadi ```http.host == "ppid.dpr.go.id" && http.request.method == POST```

![gambar display filter no 3](/images/no3Filter.png)

Bisa dilihat pada gambar yang dikotaki, bahwa username yang dimasukkan adalah "10pemuda" dan passwordnya "guncanngdunia"

## **Soal 4**
**4. Temukan paket dari web-web yang menggunakan basic authentication method!**

Untuk menemukan paket dari web-web yang menggunakan basic authentication method, digunakan display filter berikut

```http.authbasic```

maka akan keluar web-web yang menggunakan basic authentication method, seperti gambar berikut

![4_1](https://user-images.githubusercontent.com/61625353/96361384-718bad80-114f-11eb-9bd8-5ee602a0da80.png)

## **Soal 5**
**5. Ikuti perintah di aku.pengen.pw! Username dan password bisa didapatkan dari file .pcapng!**

Untuk mencari username dan passwordnya, kita bisa mendapatkan packet http yang dikirim/diterima oleh "aku.pengen.pw"

Display filter yang digunakan adalah ```http.host == "aku.pengen.pw"```

![gambar display filter no 5](/images/no5Filter.png)

Bisa dilihat pada gambar diatas, bahwa pada bagian Authorization kita bisa mendapatkan username dan password nya dengan mengexpand Authorization. Karena yang dipakai adalah auth basic, maka username dan password bisa langsung terlihat, yaitu ```"kakakgamtenk"``` dan ```"hartatahtabermuda"```

![gambar web no 5](/images/no5Web.png)

Setelah mengakses web "aku.pengen.pw", maka akan diminta user dan passwordnya. Jika sudah, maka akan ada instruksi dimana diminta menuliskan urutan kabel T658B yaitu putih oren, oren, putih hijau, biru, putih biru, hijau, putih coklat, coklat.

## **Soal 6**
**6. Seseorang menyimpan file zip melalui FTP dengan nama "Answer.zip". Simpan dan Buka file "Open This.pdf" di Answer.zip. Untuk mendapatkan password zipnya, temukan dalam file zipkey.txt (passwordnya adalah isi dari file txt tersebut).**

Untuk menjawab sol nomor 6, langkahya adalah gunakan display filter berikut :

```ftp-data.command contains Answer.zip```

kemudian 

```tp-data.command contains zipkey.txt```

Key nya adalah hey997400323051

File yang dimaksud adalah berikut

![6_1](https://user-images.githubusercontent.com/61625353/96361943-13ad9480-1154-11eb-8e62-2690afee4ae9.png)


## **Soal 7**
**7. Ada 500 file zip yang disimpan ke FTP Server dengan nama 1.zip, 2.zip, ..., 500.zip. Salah satunya berisi pdf yang berisi puisi. Simpan dan Buka file pdf tersebut.Your Super Mega Ultra Rare Hint = nama pdf-nya "Yes.pdf"**

Display filter yang digunakan adalah ```ftp-data``` untuk memfilter hanya data dari ftp saja yang keluar dan cari dengan hex value 59 65 73 2e 70 64 66 (hex value dari Yes.pdf)

![gambar display filter no 7](/images/no7Filter.png)

Ternyata file zip yang dimaksud adalah "473.zip". Untuk meyimpan file zip tersebut, kita bisa memfollow TCP stream nya, lalu mengganti save as raw, kemudian save dikomputer kita sendiri.

![gambar hasil no 7](/images/no7Hasil.png)

Gambar diatas adalah hasil jika kita membuka file pdf yang ada didalam "473.zip"

Cara lain dari yang diatas adalah dengan menggunakan display filter ```ftp-data contains Yes.pdf``` dan melakukan yang sama ketika sudah mendapat packet yang dimaksud.

## **Soal 8**
**8. Cari objek apa saja yang didownload (RETR) dari koneksi FTP dengan Microsoft FTP Service!**

Untuk mencari objek yang didownload (RETR) dari koneksi FTP dengan Microsoft FTP Service, digunakan display filter

```ftp.request.command == RETR```

Terdapat 2 paket yang keluar, dicheck follow tcp stream ternyata hanya yang RETR readme yang menggunakan Microsoft FTP Service.

![8_1](https://user-images.githubusercontent.com/61625353/96362112-2aa0b680-1155-11eb-97a2-761206d292e2.png)

![8_2](https://user-images.githubusercontent.com/61625353/96362128-4a37df00-1155-11eb-8ec2-7ceaa99dcc14.png)

Atau juga bisa dengan menggunakan 

```ftp.request.command == RETR && ip.addr == 198.246.117.106``` 

Karena kita sudah tau yang mana Microsoft FTP Service dari mengcek diatas.

![8_3](https://user-images.githubusercontent.com/61625353/96362152-7c494100-1155-11eb-89dc-ce5a12243c9d.png)

## **Soal 9**
**9. Cari username dan password ketika login FTP pada localhost!**

Untuk mencari login user dan password, kita bisa memfilter request command dari FTP yaitu USER dan PASS

Display filter yang digunakan adalah ```ftp.request.command == USER || ftp.request.command == PASS```

![gambar display filter no 9](/images/no9Filter.png)

Bisa dilihat pada gambar diatas, bahwa username yang dimasukkan adalah "dhana" dan passwordnya "dhana123"

## **Soal 10**
**10. Cari file .pdf di wireshark lalu download dan buka file tersebut! clue: "25 50 44 46"**

Soal nomor 10 dapat dikerjakan dengan mencari file menggunakan hex value nya.

![10_1](https://user-images.githubusercontent.com/61625353/96362211-ecf05d80-1155-11eb-8fe0-1950b3ebec82.png)

![10_2](https://user-images.githubusercontent.com/61625353/96362230-042f4b00-1156-11eb-81f6-3b3a66d8864d.png)

Berikut adalah file yang dimaksud

![10_3](https://user-images.githubusercontent.com/61625353/96362241-1e692900-1156-11eb-9be3-afb359de29af.png)

## **Soal 11**
**11. Filter sehingga wireshark hanya mengambil paket yang mengandung port 21!**

Untuk hanya mengambil paket yang mengandung port 21, capture filter yang perlu di masukkan adalah ```port 21```

![gambar filter no 11](/images/no11Filter.png)

![gambar hasil no 11](/images/no11Hasil.png)

## **Soal 12**
**12. Filter sehingga wireshark hanya mengambil paket yang berasal dari port 80!**

Agar wireshark hanya mengambil paket yang berasal dari port 80, maka digunakan capture filter :

```src port 80```

![12__1](https://user-images.githubusercontent.com/61625353/96362301-83248380-1156-11eb-92d3-a1622ff583dd.png)

Hasil capture filter adalah sebagai berikut :

![12__2](https://user-images.githubusercontent.com/61625353/96362298-7d2ea280-1156-11eb-8629-855959b9b2aa.png)

menampilkan hanya paket - paket yang berasal dari port 80.

## **Soal 13**
**13. Filter sehingga wireshark hanya menampilkan paket yang menuju port 443!**

Untuk hanya menampilkan paket yang menuju port 443, capture filter yang perlu di masukkan adalah ```dst port 443```

![gambar filter no 13](/images/no13Filter.png)

![gambar hasil no 13](/images/no13Hasil.png)

## **Soal 14**
**14. Filter sehingga wireshark hanya mengambil paket yang berasal dari ip kalian!**

Agar wireshark hanya mengambil paket yang berasal dari ip kita masing - masing, digunakan capture filter berikut :

```src host 192.168.1.8```

![12__1](https://user-images.githubusercontent.com/61625353/96362391-1362c880-1157-11eb-96c6-204348bdbc41.png)

Maka, wireshark akan mengambil paket dari ip kita seperti berikut :

![12__2](https://user-images.githubusercontent.com/61625353/96362385-0f36ab00-1157-11eb-8197-c6d0ed5d8a5c.png)



## **Soal 15**
**15. Filter sehingga wireshark hanya mengambil paket yang tujuannya ke monta.if.its.ac.id!**

Untuk hanya mengambil paket yang tujuannya ke monta.if.its.ac.id, capture filter yang perlu di masukkan adalah ```dst host monta.if.its.ac.id```

![gambar filter no 15](/images/no15Filter.png)

![gambar hasil no 15](/images/no15Hasil.png)
