# Tugas 2 IF3110 Pengembangan Aplikasi Berbasis Web

Melakukan *upgrade* Website ojek online pada Tugas 1 dengan mengaplikasikan **arsitektur web service REST dan SOAP**.



## Anggota Tim

1. Andika Kusuma (13515033)
2. Vincent Endrahadi (13515117)
3. Mico (13515126)

## Tools

1. WebApp : Java + Java Server Page
2. Web Service : SOAP and Java
3. Identity Service : Java Servlet
4. Database : MySQL

### Arsitektur Umum Server
![Gambar Arsitektur Umum](arsitektur_umum.png)




## Skenario dan Penjelasan

### Login

![](ss/login.jpg)

Pengguna dapat melakukan login sebagai user. Login akan membadingkan username dan password. Setelah dicek dan benar maka akan ditambahkan token dan expiry time dari token yang dibuat ke database user. Pada page ini telah ada proses otentikasi apakah ada pengguna yang login atau belum. Jika ada maka tampilan page akan menampilkan profile atau order.
Identitas pengguna akan ditangani oleh servlet.


### Register 

![](ss/register.jpg)

Pengguna dapat mendaftarkan diri sebagai user agar dapat menggunakan aplikasi ini. Satu user akan memiliki satu akun yang dapat digunakan sebagai penumpang maupun sebagai driver. User disediakan opsi untuk memilih apakah dia mau menjadi driver atau tidak saat registrasi. Anda harus melakukan validasi bahwa email dan username yang sama tidak boleh digunakan untuk dua kali mendaftar. **Validasi email dan username dilakukan menggunakan AJAX**.
Jika data yang dimasukkan telah benar, maka data akan ditangani oleh servlet dan nantinya akan dimasukkan ke 2 database yang terpisah. Pada database account, username, password, token, dan expiry time yang akan di INSERT.
Sedangkan pada database service, nama, email dan data lainnya akan di INSERT. 

### Profile
![](ss/profile.jpg)

Pada halaman ini, ditampilkan username, nama lengkap, email, dan nomor HP. Selain itu, ditampilkan keterangan apakah pengguna merupakan driver atau bukan. Jika pengguna merupakan driver, ditampilkan tulisan Driver diikuti rating dan jumlah vote seperti terlihat pada gambar. Jika pengguna bukan driver, ditampilkan tulisan Non-Driver, tanpa diikuti rating. Pada bagian kanan atas, terdapat tombol edit, jika pengguna menekan tombol tersebut, pengguna dibawa ke halaman Edit-Profile melalui servlet.

Pada bagian bawah, terdapat Preferred Location, yang berisi daftar lokasi yang dilayani pengguna jika berperan sebagai driver. Bagian ini ditampilkan jika pengguna merupakan driver. Pada bagian kanan atas, terdapat tombol edit, jika pengguna menekan tombol tersebut, pengguna dibawa ke halaman Edit-Preferred-Location melalui servlet.


### Edit-Profile
![](ss/editprofile.jpg)

Pada halaman ini, pengguna dapat mengedit nama yang ditampilkan, nomor telepon, foto, dan status driver.
Status driver berupa tombol Yes/No yang dapat diklik oleh pengguna untuk mengganti. Tombol Yes/No dapat berupa sekedar tulisan Yes dan No yang berubah saat ditekan. Pada saat tombol Yes/No ditekan, page tidak boleh refresh. Tulisan Yes dan No harus berbeda warna.
Pada bagian bawah halaman, terdapat tombol Back dan Save. Jika tombol Back ditekan, pengguna kembali ke halaman Profile. Jika tombol tersebut ditekan, nama dan nomor telepon pengguna akan diganti sesuai input field. Setelah tombol save ditekan, pengguna dibawa ke halaman Profile setelah data diproses ke soap yang dihandler oleh servlet.

### Edit-Preferred-Location
![](ss/editloc1.jpg)

![](ss/editloc2.jpg)

Pada Edit-Preferred-Location, ditampilkan lokasi-lokasi yang dapat dicapai jika menjadi driver. Pada tiap baris lokasi, ada tombol Delete. Jika tombol tersebut ditekan, akan tampil konfirmasi untuk delete, menggunakan Javascript. Setelah Delete, lokasi yang didelete akan hilang. Selain itu, pada tiap baris juga ada tombol edit location. Jika tombol ini ditekan maka akan tampil textbox untuk mengganti lokasi.

Pada bagian Add New Location, terdapat sebuah text area dan sebuah tombol Add. Pada text area, pengguna dapat mengisikan lokasi untuk ditambahkan. Ketika tombol Add ditekan, alamat tersebut ditambahkan pada preferred location pengguna.

Jika tombol Back ditekan, pengguna dibawa kembali ke halaman Profile.

Catatan: Format alamat dibebaskan kepada mahasiswa.

### Order-Ojek
![](ss/order.jpg)

Order-Ojek merupakan halaman utama yang ditampilkan ketika user telah login. Pada halaman Order-Ojek, terdapat sebuah form yang dapat diisi pengguna untuk melakukan order.

Perlu diperhatikan, tulisan di atas tombol logout memiliki format "Hi, username!". Selanjutnya, terdapat menu bar yang menampilkan 3 menu utama seperti pada gambar. Menu yang sedang dibuka diberikan warna background yang berbeda sebagai penanda halaman apa yang sedang dibuka pengguna.

Setelah pengguna mengisi field-field pada form order dan menekan tombol order, pengguna akan dibawa ke halaman Select-Driver melalui servlet yang akan menghandler pengambilan data dari database dengan protokol SOAP. Perlu diperhatikan bahwa seluruh field wajib diisi, kecuali field "Preferred Driver". Pada field Preferred Driver, terdapat Placeholder "(optional)"



### Select Driver
![](ss/order2.jpg)

Pada halaman ini, ditampilkan driver-driver yang tersedia dan dapat mengambil order. Driver yang dapat mengambil order adalah pengguna yang menjadi driver, dan memiliki alamat asal *atau* alamat tujuan pada "Preferred Location"-nya.

Halaman ini terdiri atas dua bagian, yaitu "Preferred Driver" dan "Other Drivers". Bagian "Preferred Driver" akan terisi dengan driver-driver dengan nama yang diisikan pengguna pada field "Preferred Driver" saat melakukan order. Jika pengguna tidak mengisikan field "Preferred Driver" atau tidak ada driver dengan nama yang diisikan pada field "Preferred Driver", bagian Preferred Driver akan kosong.

Pada bagian "Other Drivers", ditampilkan seluruh driver yang dapat mengambil order tersebut.

Perlu diperhatikan, pada setiap driver, terdapat foto, nama, dan rating driver tersebut. Rating dituliskan dengan format: Rating rata-rata (jumlah orang yang memberikan rating).

Setelah memilih driver dan menekan tombol Confirm, pengguna dibawa ke halaman Complete-Order melalui servlet yang akan menghandler pengambilan data dari database dengan protokol SOAP.


### Complete Order
![](ss/order3.jpg)

Pada halaman Complete-Order, akan ditampilkan informasi driver dan order, serta opsi untuk memberikan rating dan komentar. Setelah pengguna submit rating dan komentar untuk driver, pengguna dibawa ke halaman Order-Ojek melalui servlet yang akan menghandler pengambilan/pengiriman data dari database dengan protokol SOAP.

Rating untuk driver berupa integer antara 1 sampai 5 (inklusif). Implementasi rating dibebaskan pada peserta.

### History
![](ss/history1.jpg)

![](ss/history2.jpg)

Pada halaman history, terdapat dua tab, yaitu History Penumpang dan History Driver. History Penumpang menampilkan daftar order yang pernah diambil pengguna sebagai penumpang, dan History Driver menampilkan daftar order yang pernah diambil pengguna sebagai driver.

Pada tiap entri pada history, terdapat tombol hide. Jika tombol hide ditekan, history yang bersangkutan tidak akan ditampilkan, tapi tidak dihapus.



## Pembagian Tugas

REST :

Generate token : 13515033, 13515117  
Validasi token : 13515033, 13515117  
Fungsionalitas Login : 13515126  
Fungsionalitas Register : 13515033  
Fungsionalitas Logout : 13515033  


SOAP :  

Fungsionalitas Token Validator : 13515033, 13515117  
Fungsionalitas Generate Token: 13515033, 13515117  
Show Profile : 13515033  
Order : 13515126  
Show History : 13515117  
Edit Profile : 13515033  
Edit Preffered Location : 13515033  
Register : 13515126  


Web app (JSP) :  

Login : 13515126  
Register : 13515126  
Profile : 13515033  
Order : 13515126  
History : 13515117  
Edit Profile : 13515033  
Preffered Location : 13515033  

## Penjelasan 

### Basis Data

Basis data pada sistem, basis data pada sistem kami dibagi dua yaitu untuk webservice dan identity service
Basisdata untuk identity service hanya berupa tabel users dengan kolom id, uname, password, access_token, expiry time
Sedangkan pada database web service terdiri dari tabel users, preffered location dan orders.

### Konsep Shared Session

Konsep shared session menggunakan REST dengan bantuan session/cookies serta access token. Setiap kali pengguna login akan digenerate token khusus untuk pengguna itu sendiri. Token tersebut memiliki batas waktu ekspirasinya. Access token ini sendiri akan disimpan pada cookies maupun session di browser para user. Setiap user ingin mengakses database (web service) maka web service akan mengirimkan token ke REST untuk divalidasi.

### Pembangkitan token dan expiry time

Pembangkitan token dilakukan setiap user tersebut login. Jika user yang sedang login melakukan log out, maka token yang disimpan akan dihapus. Expiry Time diset selama 5 menit. Expiry time akan diperpanjang setiap kali user melakukan kegiatan di dalam website tersebut (tidak melakukan logout).


### Kelebihan dan Kekurangan

Kelebihan :
1. Adanya Security dengan sistem validasi token sehingga data-data user lebih terjamin. Selain itu juga dengan adanya sistem expiry token, user yang memakai program ini di komputer publik lebih kecil kemungkinannya terjadi penyalahgunaan terhadap account user jika lupa di logout.
2. Karena menggunakan hampir semua pengerjaan menggunakan basis java, kecepatan daari program lebih meningkat karena tidak seperti php yaang sistem interpreted, java harus dicompile terlebih dahulu sehingga ketika penggunaan pertama kali membutuhkan waktu tambahan karena proses kompilasi. Namun setelah proses kompilasi tersebu selesai, untuk kedepannya tidak perlu lagi d compile sehingga aplikasi berjalan lebih cepat. 
3. Aplikasi lebih scalable.

Kelemahan :
1. Waktu yang dibutuhkan dalam request response lebih lama karena tidak sepert tugas sebelumnya yang semua data request dan response bisa langusng diproses tanpa penanganan pada servlet. Lalu karena database di pisah juga sedikit menambah waktu response karena beberapa fungsi membutuhkan join antara 2 tabel yang harus diakses dengan cara yang berebda (REST dan SOAP)
2. Karena bahasa yang dipakai hampir semuanya dalam basis java, adanya sedikit kesalahan akan langsung di notice dan program tidak dapat berjalan. Tidak seperti php yang dapat menabaikan beebrapa error dan program tetap berjalan
3. Aplikasi tergantung kepada server REST dan SOAP, sehingga tidak dapat berjalan tanpa keduanya.

## About

Asisten IF3110 2017

Ade | Johan | Kristianto | Micky | Michael | Rangga | Raudi | Robert | Sashi 

Dosen : Yudistira Dwi Wardhana | Riza Satria Perdana | Muhammad Zuhri Catur Candra