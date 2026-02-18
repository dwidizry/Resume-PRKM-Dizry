# Resume-PRKM-Dizry
# Dasar Pemrograman Robot dan Kontrol Motor
## Peran mikrokontroler dalam robot
* Mikrokontroler adalah sistem saraf waktu nyata robot—mengumpulkan data sensor, menjalankan loop kontrol dan pemeriksaan keamanan, serta memerintah aktuator dengan pengaturan waktu deterministik dan latensi minimal, sambil berinteraksi dengan komputasi tingkat tinggi untuk perencanaan dan persepsi. Mereka menerima sinyal masukan dari sensor (mata dan telinga robot). Mikrokontroler memiliki program yang memberi tahu apa yang harus dilakukan dengan sinyal masukan tersebut. Sinyal keluaran dari mikrokontroler diberikan ke motor (roda, kaki, dll.) atau lampu atau aktuator lainnya dan membuat robot berjalan atau bergerak.

## Struktur program (setup() & loop())
* Bagian setup() merupakan bagian yang hanya dijalankan satu kali saja yaitu pada saat program pertama dijalankan. Bagian ini berfungsi sebagai pedefinisian suatu perangkat, seperti pedefinisian pin,komunikasi,SPI dan lain-lain. Contoh:

  void setup()

{

      pinMode(13,OUTPUT); // mengset pin 13 di board arduino sebagai output

} 

* Bagian loop() merupakan bagian yang akan terus dijalankan dan akan melakukan instruksi-instruksi/program yang ada di dalam loop() secara berurutan. Contoh:

 void loop()
{
     digitalWrite(13, HIGH); // nyalakan pin 13
     delay(1000);   // delay selama 1000 ms
     digitalWrite(13, LOW); // matikan pin 13
     delay(1000);   /// delay selama 1000 ms
} 

## Digital & Analog I/O
* Sinyal digital bersifat biner, artinya sinyal tersebut hanya dapat memiliki salah satu dari dua keadaan yang mungkin: hidup atau mati, yang direpresentasikan secara numerik sebagai 1 atau 0. Representasi biner ini membuat sinyal digital bersifat diskrit, berbeda dengan sifat kontinu sinyal analog.

* Dalam aplikasi industri, sinyal digital merepresentasikan kondisi sederhana dan jelas seperti ada atau tidaknya suatu objek, keadaan katup terbuka atau tertutup, atau status motor hidup atau mati. Sinyal-sinyal ini mudah diproses dan diinterpretasikan oleh sistem kontrol, yang dapat dengan cepat mengambil keputusan berdasarkan input biner. Modul I/O digital dirancang untuk menangani sinyal biner ini, mengubahnya menjadi format yang dapat digunakan sistem kontrol untuk tujuan pemantauan dan pengendalian.

* Sinyal analog adalah sinyal kontinu yang bervariasi seiring waktu dan dapat mengambil nilai apa pun dalam rentang tertentu. Tidak seperti sinyal digital, yang bersifat diskrit dan biner, sinyal analog merepresentasikan informasi dalam bentuk yang berbanding lurus dengan besaran fisik yang diukur.

* Dalam aplikasi industri, sinyal analog merepresentasikan parameter suhu, tekanan, laju aliran, dan level. Sinyal-sinyal ini biasanya diukur dalam volt (V) atau miliampere (mA). Misalnya, sensor suhu mungkin mengeluarkan tegangan yang bervariasi secara kontinu dengan suhu, atau pengukur aliran mungkin menghasilkan sinyal arus yang proporsional dengan laju aliran. Modul I/O analog menangani sinyal kontinu ini, mengubahnya menjadi data digital yang dapat diproses oleh sistem kontrol. Konversi ini sangat penting untuk pemantauan dan pengendalian proses industri yang akurat.

## PWM dan kecepatan motor
* PWM adalah teknik yang berarti modulasi lebar pulsa. Gelombang PWM adalah gelombang pulsa yang dikendalikan oleh teknik ini. Jika induktansi catu daya switching dibandingkan dengan jantung hewan, maka gelombang PWM dari tegangan switching dapat dibandingkan dengan detak jantung hewan.

* Secara umum, jika kita ingin mengontrol kecepatan motor DC, kita dapat menyesuaikan tegangan di terminal motor bergetar. Kecepatan motor sebanding dengan tegangan input - Semakin tinggi tegangan, semakin cepat kecepatan. Oleh karena itu, meningkatkan tegangan akan meningkatkan kecepatan. Saat Anda memberikan tegangan yang stabil, motor akan berputar pada kecepatan tertentu. Namun, metode ini memiliki kerugian yang jelas: tidak dapat mencapai kontrol kecepatan tanpa langkah motor.

* Kontrol kecepatan tanpa langkah berarti bahwa kecepatan motor halus dari kecepatan tinggi ke kecepatan rendah lainnya, atau dari kecepatan rendah ke kecepatan tinggi. Ini adalah proses menyesuaikan kecepatan secara bertahap menjadi lebih cepat atau lebih lambat).

* Misalnya, Anda mungkin ingin menyesuaikan kecepatan motor dari 100% hingga 70%, atau dari 70% hingga 50%, kontrol yang tepat seperti itu tidak dapat dicapai jika tegangan langsung diterapkan.

## Dead zone & offset
* Dalam sistem kontrol robot dan perangkat input seperti joystick, Dead Zone dan Offset merupakan dua parameter teknis krusial yang digunakan untuk menjamin presisi dan stabilitas kendali. Dead Zone atau zona mati adalah area ambang batas di sekitar titik pusat di mana pergerakan fisik joystick tidak akan terdaftar sebagai input oleh mikrokontroler. Fungsi utamanya adalah untuk mengatasi sensitivitas berlebih atau fenomena drift pada komponen yang sudah aus, sehingga robot atau karakter tidak bergerak sendiri saat stick berada di posisi netral. Pengaturan ini biasanya terbagi menjadi Minimum Deadzone, yang menentukan seberapa jauh tuas harus digerakkan untuk mulai merespons, dan Maximum Deadzone, yang menentukan titik di mana input dianggap mencapai nilai maksimum.

* Sementara itu, Offset berperan sebagai parameter penyesuaian untuk memindahkan atau mengompensasi titik pusat respons tersebut. Dalam konteks kontroler, offset digunakan untuk menggeser posisi dead zone agar selaras dengan posisi netral fisik tuas yang mungkin sudah tidak presisi (tidak tepat di tengah secara elektrik). Dengan mengombinasikan keduanya, pengembang dapat memastikan bahwa rentang kendali mekanis yang diberikan oleh operator diterjemahkan secara akurat menjadi instruksi digital, menghasilkan pergerakan robot yang lebih halus, terukur, dan bebas dari gangguan input tak disengaja.

## Kinematika robot (Differential / Mecanum)
* Kinematika Penggerak Mecanum adalah alat yang berguna untuk mengkonversi antara satu Objek Kecepatan Sasis dengan Objek Kecepatan Roda Penggerak Mecanum lainnya, yang berisi kecepatan untuk masing-masing dari empat roda pada penggerak mecanum. Kelas ini Kinematika Penggerak Mecanum menerima empat argumen konstruktor, dengan setiap argumen berupa lokasi roda relatif terhadap pusat robot (sebagai Translation2d). Urutan argumennya adalah depan kiri, depan kanan, belakang kiri, dan belakang kanan. Lokasi roda harus relatif terhadap pusat robot. Nilai x positif menunjukkan pergerakan ke arah depan robot, sedangkan nilai y positif menunjukkan pergerakan ke arah kiri robot.

* Kinematika adalah penerapan geometri untuk mengendalikan berbagai mekanisme robot. Persamaan kinematika digunakan untuk mengendalikan mekanisme dengan memberikan masukan spesifik untuk mencapai keluaran yang diinginkan.

* Banyak persamaan kinematika di sini diambil dari Controls Engineering in the FIRST Robotics Competition (buku) dan Mobile Robot Kinematics for FTC (makalah) , yang berisi penurunan rumus yang relevan. Meskipun hanya persamaan kinematika tank (penggerak diferensial) dan mecanum yang ditampilkan di sini, sumber-sumber ini juga berisi penurunan rumus untuk mekanisme lain seperti swerve dan odometri roda mati. Tank, atau penggerak diferensial, adalah sistem penggerak yang terdiri dari dua set roda di kedua sisi robot yang digerakkan secara independen.

## Mapping joystick (maju, mundur, belok)
* Robot beroda adalah sebuah robot yang dapat berjalan dengan menggunakan roda. Robot ini umumnya memiliki gerak maju, mundur, berhenti, belok kanan dan belok kiri. Robot ini dibuat dengan menggunakan mikrocontroller sebagai alat pengontrolnya. Robot tidak dapat melakukan aksinya jika tidak dikendalikan oleh manusia.

* Pada penelitian ini diusulkan Sistem Remote Control Robot Beroda Menggunakan Teknologi Leap Motion. Remote kontrol akan dibuat dengan menggunakan leap motion. Leap motion digunakan untuk mendeteksi posisi titik-titik koordinat (XYZ) tulang-tulang pada tangan dan jari (Metacarpal, Proximal Phalanx, Intermediate Phalanx, Distal Phalanx dan Palm). Data koordinat tersebut akan digunakan untuk membentuk fitur. Fitur yang telah dibentuk akan diambil nilai rata-ratanya. Nilai rata-rata fitur tersebut akan dijadikan sebagai nilai untuk menentukan range atau area, dimana ada 5 range atau area (nilai range forward, backward, stop, right dan left). Setiap nilai uji coba akan dicocokkan dengan nilai range yang ada untuk menjalankan robot beroda. Sistem ini diharapkan dapat mengontrol robot beroda dengan instruksi maju, mundur, berhenti, belok kanan, dan belok kiri. Adapun untuk mengukur keberhasilan dari sistem ini akan dilakukan uji coba dengan mengukur tingkat akurasinya.

* Tab Perangkat USB pada Driver Station digunakan untuk mengatur dan mengkonfigurasi joystick agar dapat digunakan dengan robot. Menekan tombol pada joystick akan menyebabkan entri joystick tersebut di tabel menyala hijau. Memilih joystick akan menampilkan nilai sumbu, tombol, dan POV yang dapat digunakan untuk menentukan pemetaan antara fitur fisik joystick dan nomor sumbu atau tombol. Tab Perangkat USB juga menetapkan indeks joystick untuk setiap joystick. Untuk mengubah urutan joystick, cukup klik dan seret. Perangkat lunak Driver Station akan mencoba mempertahankan urutan perangkat di antara setiap penggunaan. Sebaiknya catat urutan perangkat Anda dan periksa setiap kali Anda memulai perangkat lunak Driver Station untuk memastikan urutannya sudah benar.

* Saat Driver Station dalam mode nonaktif, ia secara rutin mencari perubahan status pada perangkat joystick. Perangkat yang dicabut akan dihapus dari daftar dan perangkat baru akan dibuka dan ditambahkan. Saat tidak terhubung ke FMS, mencabut joystick akan memaksa Driver Station ke mode nonaktif. Untuk mulai menggunakan joystick lagi: colokkan joystick, periksa apakah joystick muncul di tempat yang tepat, lalu aktifkan kembali robot. Saat Driver Station dalam mode aktif, ia tidak akan memindai perangkat baru. Ini adalah operasi yang memakan waktu dan pembaruan sinyal dari perangkat yang terhubung harus diprioritaskan.
