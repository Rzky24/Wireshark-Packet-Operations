# Wireshark-Packet-Operations
Di ruangan ini, kita akan membahas dasar-dasar analisis paket dengan Wireshark dan menyelidiki kejadian yang menarik perhatian pada tingkat paket. Perlu dicatat bahwa ini adalah ruangan kedua dari tiga ruangan Wireshark, dan disarankan untuk mengunjungi ruangan pertama (Wireshark: Dasar-Dasar ) untuk berlatih dan menyegarkan kembali keterampilan Wireshark Anda sebelum memulai ruangan ini.

Tujuan pembelajaran
Selidiki tangkapan lalu lintas jaringan
Lihat statistik termasuk ringkasan dan detail protokol.
Mengungkap dan menerapkan prinsip-prinsip penyaringan paket.
Terapkan filter protokol
Terapkan pemfilteran lanjutan

Lingkungan
Sebuah VM yang menyertakan Wireshark dan beberapa tangkapan paket terhubung ke ruangan ini. Anda dapat memulai VM dengan mengklik Start Virtual Machinetombol di bawah. Mesin Virtual akan dimulai dalam tampilan terpisah. Jika Anda tidak melihat VM dalam tampilan terpisah, Anda dapat mengklik tombol biru Show Split Viewdi kanan atas halaman ruangan ini untuk menampilkannya. Buka Exercise.pcapng file di Desktop dan ikuti langkah-langkahnya.

Catatan: Jangan berinteraksi langsung dengan domain dan alamat IP apa pun di ruangan ini. Domain dan alamat IP disertakan hanya untuk tujuan referensi.

Statistik | Ringkasan
Statistik
Menu ini menyediakan berbagai opsi statistik yang siap untuk dianalisis guna membantu pengguna melihat gambaran besar dalam hal cakupan lalu lintas, protokol yang tersedia, titik akhir dan percakapan, serta beberapa detail spesifik protokol seperti DHCP , DNS , dan HTTP /2. Bagi seorang analis keamanan, sangat penting untuk mengetahui cara memanfaatkan informasi statistik. Bagian ini memberikan ringkasan singkat dari pcap yang telah diproses , yang akan membantu analis membuat hipotesis untuk investigasi. Anda dapat menggunakan  menu "Statistik" untuk melihat semua opsi yang tersedia. Sekarang jalankan VM yang diberikan , buka Wireshark, muat file "Exercise.pcapng", dan ikuti panduan langkah demi langkah.

Alamat yang Terpecahkan
Opsi ini membantu analis mengidentifikasi alamat IP dan nama DNS yang tersedia dalam file tangkapan dengan menyediakan daftar alamat yang telah diresolusi dan nama host-nya. Perhatikan bahwa informasi nama host diambil dari jawaban DNS dalam file tangkapan. Analis dapat dengan cepat mengidentifikasi sumber daya yang diakses dengan menggunakan menu ini. Dengan demikian, mereka dapat menemukan sumber daya yang diakses dan mengevaluasinya sesuai dengan peristiwa yang diminati. Anda dapat menggunakan  menu "Statistik --> Alamat yang Diresolusi"  untuk melihat semua alamat yang telah diresolusi oleh Wireshark.

<img width="1463" height="803" alt="image" src="https://github.com/user-attachments/assets/9b96e03f-c75b-41ea-843a-71300b8242b5" />

Hierarki Protokol
Opsi ini menguraikan semua protokol yang tersedia dari file tangkapan dan membantu analis melihat protokol dalam tampilan pohon berdasarkan penghitung paket dan persentase. Dengan demikian, analis dapat melihat penggunaan keseluruhan port dan layanan serta fokus pada kejadian yang diminati. Aturan emas yang disebutkan di ruangan sebelumnya berlaku di bagian ini; Anda dapat mengklik kanan dan memfilter kejadian yang diminati. Anda dapat menggunakan  "Statistik --> Hierarki Protokol". <img width="1463" height="648" alt="image" src="https://github.com/user-attachments/assets/687a0c42-6975-4fb9-a05e-c5aef3a1bb9e" />

Percakapan
Percakapan mewakili lalu lintas antara dua titik akhir tertentu. Opsi ini menyediakan daftar percakapan dalam lima format dasar; ethernet, IPv4, IPv6, TCP , dan UDP . Dengan demikian, analis dapat mengidentifikasi semua percakapan dan titik akhir kontak untuk peristiwa yang diminati. Anda dapat menggunakan menu "Statistik --> Percakapan" untuk melihat informasi ini.

Titik akhir
Opsi titik akhir (endpoints) mirip dengan opsi percakapan (conversations). Satu-satunya perbedaan adalah opsi ini menyediakan informasi unik untuk satu bidang informasi (Ethernet, IPv4, IPv6, TCP , dan UDP ). Dengan demikian, analis dapat mengidentifikasi titik akhir unik dalam file tangkapan dan menggunakannya untuk peristiwa yang diminati. Anda dapat menggunakan menu "Statistik --> Titik Akhir" untuk melihat informasi ini.

Wireshark juga mendukung resolusi alamat MAC ke format yang mudah dibaca manusia menggunakan nama pabrikan yang ditetapkan oleh IEEE. Perhatikan bahwa konversi ini dilakukan melalui tiga byte pertama dari alamat MAC dan hanya berfungsi untuk pabrikan yang dikenal. Saat Anda meninjau titik akhir ethernet, Anda dapat mengaktifkan opsi ini dengan tombol "Resolusi nama" di sudut kiri bawah jendela titik akhir. <img width="1463" height="784" alt="image" src="https://github.com/user-attachments/assets/d272b7bd-b117-4b50-8a85-52f188d3fdfb" />

Resolusi nama tidak hanya terbatas pada alamat MAC. Wireshark juga menyediakan opsi resolusi nama IP dan port. Namun, opsi ini tidak diaktifkan secara default. Jika Anda ingin menggunakan fungsi ini, Anda perlu mengaktifkannya melalui menu "Edit --> Preferensi --> Resolusi Nama" . Setelah Anda mengaktifkan resolusi nama IP dan port, Anda akan melihat alamat IP dan nama port yang telah diresolusi di panel daftar paket dan juga dapat melihat nama yang telah diresolusi di menu "Percakapan" dan "Titik Akhir".

Tampilan menu titik akhir dengan resolusi nama:<img width="1463" height="415" alt="image" src="https://github.com/user-attachments/assets/f778f162-506e-4355-82d6-44808534df48" />

Selain resolusi nama, Wireshark juga menyediakan pemetaan geolokasi IP yang membantu analis mengidentifikasi alamat sumber dan tujuan peta. Namun fitur ini tidak diaktifkan secara default dan membutuhkan data tambahan seperti basis data GeoIP. Saat ini, Wireshark mendukung basis data MaxMind, dan versi terbaru Wireshark sudah dikonfigurasi dengan resolver basis data MaxMind. Namun, Anda tetap memerlukan file basis data MaxMind dan memberikan jalur basis data ke Wireshark dengan menggunakan menu "Edit --> Preferensi --> Resolusi Nama --> Direktori basis data MaxMind". Setelah Anda mengunduh dan menunjukkan jalurnya, Wireshark akan secara otomatis memberikan informasi GeoIP di bawah detail protokol IP untuk alamat IP yang cocok.<img width="842" height="528" alt="image" src="https://github.com/user-attachments/assets/477af2bd-2032-4123-b2da-c476f82b5ea0" />

Tampilan titik akhir dan GeoIP
<img width="1463" height="493" alt="image" src="https://github.com/user-attachments/assets/f8295bb7-705d-44c7-86aa-ff986d7d51ff" />
Catatan: Anda memerlukan koneksi internet aktif untuk melihat peta GeoIP. Komputer di laboratorium tidak memiliki koneksi internet aktif!

Jawablah pertanyaan-pertanyaan di bawah ini.

Selidiki alamat yang telah diresolusi. Berapakah alamat IP dari nama host yang diawali dengan "bbc"?  199.232.24.81
cara nya buaka file exercise.pcapng - lihat halaman utama wireshark - statistic - pilih resolved addresses - bagian Host - klik bbc- muncul hasil  199.232.24.81

Berapakah jumlah percakapan IPv4 ? 435
statistic - pilih coversations - lihat ipv4 - hasil 435

Berapa banyak byte (k) yang ditransfer dari alamat MAC "Micro-St"?
statistic - endpoint - lihat di Micro-St- hasil - 7474

Berapakah jumlah alamat IP yang terkait dengan "Kansas City"? 4
statistic - endpoint - lihat di IPv4 -Kansas City - lihat collum rx packet - 4

Alamat IP mana yang terkait dengan Organisasi AS "Blicnet"? 188.246.82.7
statistic - endpoint - lihat di colom AS "Blicnet" - hasil 188.246.82.7

Statistik | Detail Protokol
IPv4 dan IPv6
Sampai di sini, hampir semua opsi memberikan informasi yang berisi kedua versi alamat IP. Menu statistik memiliki dua opsi untuk mempersempit statistik pada paket yang berisi versi IP tertentu. Dengan demikian, analis dapat mengidentifikasi dan mencantumkan semua kejadian yang terkait dengan versi IP tertentu dalam satu jendela dan menggunakannya untuk kejadian yang diminati. Anda dapat menggunakan menu "Statistik --> Statistik IPvX" untuk melihat informasi ini. <img width="1239" height="1200" alt="image" src="https://github.com/user-attachments/assets/9ebd7da2-c340-4a0c-8484-5cff0f87e601" />
<img width="1463" height="879" alt="image" src="https://github.com/user-attachments/assets/04e53822-ec01-49f0-b253-460023db1722" />
DNS
Opsi ini menguraikan semua paket DNS dari file tangkapan dan membantu analis melihat temuan dalam tampilan pohon berdasarkan penghitung paket dan persentase protokol DNS . Dengan demikian, analis dapat melihat penggunaan keseluruhan layanan DNS , termasuk rcode, opcode, class, tipe kueri, statistik layanan dan kueri, dan menggunakannya untuk peristiwa yang diminati. Anda dapat menggunakan  menu "Statistik --> DNS "  untuk melihat informasi ini.<img width="1239" height="1200" alt="image" src="https://github.com/user-attachments/assets/49282367-5571-48ea-8d91-37cd2ab5d9e8" />

HTTP
Opsi ini menguraikan semua paket HTTP dari file tangkapan dan membantu analis melihat temuan dalam tampilan pohon berdasarkan penghitung paket dan persentase protokol HTTP . Dengan demikian, analis dapat melihat penggunaan keseluruhan layanan HTTP , termasuk kode permintaan dan respons serta permintaan asli. Anda dapat menggunakan  menu "Statistik --> HTTP " untuk melihat informasi ini.<img width="1320" height="1200" alt="image" src="https://github.com/user-attachments/assets/60708cfa-498d-49b5-9b87-48f8ebaa8a0e" />

Jawablah pertanyaan-pertanyaan di bawah ini.

Apa alamat tujuan IPv4 yang paling sering digunakan? 10.100.1.33
statistic - converstations - ipv4 - lihat collom B - yaitu alamat yang sering di gunakan - 10.100.1.33

Berapakah waktu respons permintaan layanan maksimum untuk paket DNS? 0.467897
statistic - dns - lihat di respons permintaan / request respons - hasil 

Berapakah jumlah Permintaan HTTP yang dilakukan oleh "rad[.]msn[.]com?" ? 39 
statistic - http - lihat bagian rad.msn - hasil - 39 

Penyaringan Paket | Prinsip-prinsip
Penyaringan Paket
Di ruangan sebelumnya ( Wireshark: Dasar-Dasarnya ), kita telah membahas penyaringan paket dan cara menyaring paket tanpa menggunakan kueri. Di ruangan ini, kita akan menggunakan kueri untuk menyaring paket. Seperti yang disebutkan sebelumnya, ada dua jenis filter di Wireshark. Meskipun keduanya menggunakan sintaks yang serupa, keduanya digunakan untuk tujuan yang berbeda. Mari kita ingat perbedaan antara kedua kategori ini.

Filter Tampilan	
Jenis filter ini digunakan untuk menyelidiki paket dengan mengurangi jumlah paket yang terlihat, dan dapat diubah selama proses pengambilan data. 

Catatan:  Anda tidak dapat menggunakan ekspresi filter tampilan untuk menangkap lalu lintas dan sebaliknya.

Kasus penggunaan tipikal adalah menangkap semuanya dan memfilter paket sesuai dengan kejadian yang diminati. Hanya profesional berpengalaman yang menggunakan filter penangkapan dan memantau lalu lintas. Inilah mengapa Wireshark mendukung lebih banyak jenis protokol dalam filter tampilan. Pastikan Anda benar-benar mempelajari cara menggunakan filter penangkapan sebelum menggunakannya di lingkungan nyata. Ingat, Anda tidak dapat menangkap kejadian yang diminati jika filter penangkapan Anda tidak sesuai dengan pola lalu lintas spesifik yang Anda cari.

Sintaks Filter Tangkap
Filter ini menggunakan offset byte, nilai heksadesimal, dan mask dengan operator boolean, dan tujuan filter ini tidak mudah dipahami/diprediksi pada pandangan pertama. Sintaks dasarnya dijelaskan di bawah ini:

Cakupan:  host, jaringan, port, dan rentang port.
Arah:  sumber, tujuan, sumber atau tujuan, sumber dan tujuan,
Protokol:  ether, wlan, ip, ip6, arp , rarp, tcp dan udp .
Contoh filter untuk menangkap lalu lintas port 80: tcp port 80
Anda dapat membaca lebih lanjut tentang sintaks filter tangkapan di  sini  dan  di sini . Referensi cepat tersedia di bawah menu "Tangkapan --> Filter Tangkapan" .<img width="1082" height="465" alt="image" src="https://github.com/user-attachments/assets/bd99fba5-d734-49ff-abd8-f79d8bd96cd9" />

Sintaks Filter Tampilan
Ini adalah fitur Wireshark yang paling ampuh. Fitur ini mendukung 3000 protokol dan memungkinkan pencarian tingkat paket berdasarkan rincian protokol. " Referensi Filter Tampilan " resmi menyediakan semua rincian protokol yang didukung untuk pemfilteran.

Contoh filter untuk menangkap lalu lintas port 80: tcp.port == 80
Wireshark memiliki opsi bawaan (Display Filter Expression) yang menyimpan semua struktur protokol yang didukung untuk membantu analis membuat filter tampilan. Kita akan membahas menu "Display Filter Expression" nanti. Sekarang mari kita pahami dasar-dasar operasi filter tampilan. Referensi cepat tersedia di bawah menu "Analyse --> Display Filters" .<img width="1082" height="457" alt="image" src="https://github.com/user-attachments/assets/a8117e75-e483-4765-91c5-2b71da99c601" />

Operator Perbandingan
Anda dapat membuat filter tampilan dengan menggunakan berbagai operator perbandingan untuk menemukan peristiwa yang diminati. Operator utama ditunjukkan pada tabel di bawah ini.

Bahasa inggris	Mirip C	Keterangan	Contoh
persamaan	==	Setara	
ip.src == 10.10.10.100

ne	!=	Tidak sama	
ip.src != 10.10.10.100

gt	>	Lebih besar dari	
ip.ttl > 250

lt	<	Kurang dari	
ip.ttl < 10

ge	>=	Lebih besar dari atau sama dengan	
ip.ttl >= 0xFA

le	<=	Kurang dari atau sama dengan	
ip.ttl <= 0xA

Catatan:  Wireshark mendukung nilai desimal dan heksadesimal dalam pemfilteran. Anda dapat menggunakan format apa pun yang Anda inginkan sesuai dengan pencarian yang akan Anda lakukan.

Ekspresi Logika
Wireshark mendukung sintaks boolean. Anda juga dapat membuat filter tampilan dengan menggunakan operator logika.

Bahasa inggris  	Mirip C	Keterangan  	Contoh
Dan	&&	Logika DAN	
(ip.src == 10.10.10.100) AND (ip.src == 10.10.10.111)

atau	||	OR Logika	
(ip.src == 10.10.10.100) OR (ip.src == 10.10.10.111)

bukan	!	Logika TIDAK	
!(ip.src == 10.10.10.222)

Catatan:  Penggunaan ini !=value sudah usang; menggunakannya dapat memberikan hasil yang tidak konsisten. Penggunaan !(value) gaya ini disarankan untuk hasil yang lebih konsisten.

Toolbar Filter Paket
Toolbar filter adalah tempat Anda membuat dan menerapkan filter tampilan. Ini adalah toolbar cerdas yang membantu Anda membuat filter tampilan yang valid dengan mudah. ​​Sebelum mulai memfilter paket, berikut beberapa tips:

Filter paket didefinisikan dalam huruf kecil.
Filter paket memiliki fitur pelengkapan otomatis untuk menguraikan detail protokol, dan setiap detail diwakili oleh sebuah "titik".
Filter paket memiliki representasi tiga warna yang dijelaskan di bawah ini.

Hijau	Filter yang valid
Merah	Filter tidak valid
Kuning	Filter peringatan. Filter ini berfungsi, tetapi tidak dapat diandalkan, dan disarankan untuk menggantinya dengan filter yang valid.
<img width="1463" height="361" alt="image" src="https://github.com/user-attachments/assets/91535337-b410-4abe-99fb-d5079a2bfc43" />

Fitur toolbar filter ditampilkan di bawah ini.
<img width="1463" height="477" alt="image" src="https://github.com/user-attachments/assets/150995f7-1efa-4488-9ade-009e8c0888d2" />
Kita telah membahas banyak prinsip dan sintaks. Mari kita praktikkan dan mulai memfilter paket pada tugas berikutnya.

Penyaringan Paket | Filter Protokol
Filter Protokol
Seperti yang disebutkan pada tugas sebelumnya, Wireshark mendukung 3000 protokol dan memungkinkan investigasi tingkat paket dengan memfilter bidang protokol. Tugas ini menunjukkan pembuatan dan penggunaan filter terhadap berbagai bidang protokol. 

Filter IP
Filter IP membantu analis menyaring lalu lintas berdasarkan informasi tingkat IP dari paket (lapisan jaringan model OSI). Ini adalah salah satu filter yang paling umum digunakan di Wireshark. Filter ini menyaring informasi tingkat jaringan seperti alamat IP, versi, waktu hidup (time to live), jenis layanan, flag, dan nilai checksum.

Filter umum ditunjukkan pada tabel yang diberikan.

Menyaring	Keterangan
ip

Tampilkan semua paket IP.
ip.addr == 10.10.10.111

Tampilkan semua paket yang berisi alamat IP 10.10.10.111.
ip.addr == 10.10.10.0/24

Tampilkan semua paket yang berisi alamat IP dari subnet 10.10.10.0/24.
ip.src == 10.10.10.111

Tampilkan semua paket yang berasal dari 10.10.10.111
ip.dst == 10.10.10.111

Tampilkan semua paket yang dikirim ke 10.10.10.111
ip.addr  vs  ip.src/ip.dst	Catatan:  ip.addr menyaring lalu lintas tanpa mempertimbangkan arah paket. ip.src/ip.dst menyaring paket dengan mempertimbangkan arah paket.<img width="1555" height="1089" alt="image" src="https://github.com/user-attachments/assets/8db838f1-70c2-4cc5-96f8-9531e752f520" />

Filter TCP dan UDP
Filter TCP membantu analis menyaring lalu lintas berdasarkan informasi tingkat protokol dari paket (lapisan Transport dari model OSI). Filter ini menyaring informasi tingkat protokol transport seperti port sumber dan tujuan, nomor urutan, nomor pengakuan, ukuran jendela, stempel waktu, flag, panjang, dan kesalahan protokol.

Menyaring	Keterangan	Menyaring	Ekspresi
tcp.port == 80

Tampilkan semua paket TCP dengan port 80 	
udp.port == 53

Tampilkan semua paket UDP dengan port 53
tcp.srcport == 1234

Tampilkan semua paket TCP yang berasal dari port 1234	
udp.srcport == 1234

Tampilkan semua paket UDP yang berasal dari port 1234
tcp.dstport == 80

Tampilkan semua paket TCP yang dikirim ke port 80	
udp.dstport == 5353

Tampilkan semua paket UDP yang dikirim ke port 5353
<img width="1555" height="1089" alt="image" src="https://github.com/user-attachments/assets/0917d02b-466e-4abc-8e8c-f882d9978dfe" />

Filter Protokol Tingkat Aplikasi | HTTP dan DNS
Filter protokol tingkat aplikasi membantu analis menyaring lalu lintas sesuai dengan informasi tingkat protokol aplikasi dari paket (lapisan aplikasi model OSI). Filter ini menyaring informasi spesifik aplikasi, seperti muatan dan data terkait, tergantung pada jenis protokolnya.

Menyaring	Keterangan	Menyaring	Keterangan
http

Tampilkan semua paket HTTP	
dns

Tampilkan semua paket DNS
http.response.code == 200

Tampilkan semua paket dengan kode respons HTTP "200"	
dns.flags.response == 0

Tampilkan semua permintaan DNS
http.request.method == "GET"

Tampilkan semua permintaan HTTP GET	
dns.flags.response == 1

Tampilkan semua respons DNS
http.request.method == "POST"

Tampilkan semua permintaan HTTP POST	
dns.qry.type == 1

Tampilkan semua catatan DNS "A"
<img width="1555" height="1089" alt="image" src="https://github.com/user-attachments/assets/11ebfc4d-e38a-436b-8e01-b9b0cb3011f5" />

Tampilkan Ekspresi Filter
Seperti yang disebutkan sebelumnya, Wireshark memiliki opsi bawaan (Display Filter Expression) yang menyimpan semua struktur protokol yang didukung untuk membantu analis membuat filter tampilan. Ketika seorang analis tidak dapat mengingat filter yang dibutuhkan untuk protokol tertentu atau tidak yakin tentang nilai yang dapat ditetapkan untuk suatu filter, menu Display Filter Expressions menyediakan panduan pembuat filter tampilan yang mudah digunakan. Menu ini tersedia di bawah menu  "Analyse --> Display Filter Expression"  .

Tidak mungkin menghafal semua detail filter tampilan untuk setiap protokol. Setiap protokol dapat memiliki bidang yang berbeda dan dapat menerima berbagai jenis nilai. Menu "Ekspresi Filter Tampilan" menunjukkan semua bidang protokol, jenis nilai yang diterima (bilangan bulat atau string), dan nilai yang telah ditentukan sebelumnya (jika ada). Perlu diingat bahwa dibutuhkan waktu dan latihan untuk menguasai pembuatan filter dan mempelajari bidang filter protokol.

<img width="862" height="746" alt="image" src="https://github.com/user-attachments/assets/985a85df-290d-4dc9-aaad-0550d476378c" />

Catatan: Wireshark: dasar-dasar  memperkenalkan "Aturan Pewarnaan" (Tugas-2). Sekarang Anda tahu cara membuat filter tampilan dan memfilter peristiwa yang diminati. Anda dapat menggunakan  menu "Tampilan --> Aturan Pewarnaan"  untuk menetapkan warna guna menyoroti hasil filter tampilan Anda.

Jawablah pertanyaan-pertanyaan di bawah ini.

Berapakah jumlah paket IP?
81420
Di filter halaman wire shark , cukup ketik 'ip' untuk memfilter berdasarkan paket IP

Berapakah jumlah paket dengan "nilai TTL kurang dari 10"?
66
Di filter wireshark , cukup ketik  ip.ttl<10 ( jangan memakai spacy ) - lihat displayed gambar halaman utama wire shark pojok kanan bawah - hasil 66

Berapakah jumlah paket yang menggunakan "port TCP 4444"? 
632
Di filter wireshark , cukup ketik  tcp.port == 4444  - lihat displayed gambar halaman utama wire shark pojok kanan bawah - 632

Berapakah jumlah permintaan "HTTP GET" yang dikirim ke port "80"?
527
Di filter wireshark , cukup ketik  http.request.method == "GET"  && tcp.port== 80 - lihat displayed gambar halaman utama wire shark pojok kanan bawah -hasil 527

Berapakah jumlah kueri DNS tipe A?
51
Di filter wireshark , cukup ketik - dns.a  - lihat displayed gambar halaman utama wire shark pojok kanan bawah -hasil - 51

Penyaringan Lanjutan
Penyaringan Lanjutan
Sejauh ini, Anda telah mempelajari dasar-dasar operasi penyaringan paket. Sekarang saatnya untuk fokus pada detail paket spesifik untuk peristiwa yang diminati. Selain operator dan ekspresi yang dibahas di ruangan sebelumnya, Wireshark memiliki operator dan fungsi tingkat lanjut. Opsi penyaringan tingkat lanjut ini membantu analis melakukan analisis mendalam terhadap suatu peristiwa yang diminati.


Filter: "berisi"
Menyaring	berisi
Jenis	Operator Perbandingan
Keterangan	Cari nilai di dalam paket. Fungsi ini peka terhadap huruf besar dan kecil serta menyediakan fungsionalitas serupa dengan opsi "Cari" dengan memfokuskan pada bidang tertentu.
Contoh	Temukan semua server " Apache ".
Alur kerja	Cantumkan semua paket HTTP di mana kolom "server" pada paket tersebut berisi kata kunci " Apache ".
Penggunaan	
http.server contains "Apache"<img width="1064" height="715" alt="image" src="https://github.com/user-attachments/assets/5a0fc97a-d9b2-44a8-af81-3d4c4b7ca577" />

Filter: "kecocokan"
Menyaring	pertandingan
Jenis	Operator Perbandingan
Keterangan	Mencari pola dalam ekspresi reguler. Pencarian ini tidak peka terhadap huruf besar/kecil, dan kueri yang kompleks memiliki margin kesalahan.
Contoh	Temukan semua halaman .php dan .html.
Alur kerja	Cantumkan semua  paket HTTP  di mana kolom "host" paket tersebut cocok dengan kata kunci ".php" atau ".html".
Penggunaan	
http.host matches "\.(php|html)"<img width="1074" height="718" alt="image" src="https://github.com/user-attachments/assets/93df04b6-cc3a-4c3b-8421-14813850967d" />

Filter: "masuk"
Menyaring	di dalam
Jenis	 Keanggotaan Tetap
Keterangan	Mencari nilai atau kolom di dalam cakupan/rentang tertentu.
Contoh	Temukan semua paket yang menggunakan port 80, 443, atau 8080.
Alur kerja	Cantumkan semua paket TCP yang kolom "port" pada paket tersebut memiliki nilai 80, 443, atau 8080.
Penggunaan	
tcp.port in {80 443 8080} <img width="1142" height="768" alt="image" src="https://github.com/user-attachments/assets/3c515c5d-8230-4493-ba6b-a8f8faa37960" />

Filter: "atas"
Menyaring	atas
Jenis	Fungsi
Keterangan	Mengubah nilai string menjadi huruf besar.
Contoh	Temukan semua server "APACHE".
Alur kerja	Ubah semua   kolom "server" pada paket HTTP menjadi huruf besar dan daftarkan paket yang berisi kata kunci "APACHE".
Penggunaan	
upper(http.server) contains "APACHE"<img width="1123" height="752" alt="image" src="https://github.com/user-attachments/assets/3065bc35-fe4c-4bf4-9148-7b019c7a2ed6" />

Filter: "lebih rendah"
Menyaring	lebih rendah
Jenis	Fungsi
Keterangan	Mengubah nilai string menjadi huruf kecil.
Contoh	Temukan semua server " apache ".
Alur kerja	Ubah semua   informasi field "server" pada paket HTTP menjadi huruf kecil dan daftarkan paket yang berisi kata kunci " apache ".
Penggunaan	
lower(http.server) contains "apache" <img width="1160" height="776" alt="image" src="https://github.com/user-attachments/assets/53d06c74-84bf-4ada-9d76-b732a6b8f311" />

Filter: "string"
Menyaring	rangkaian
Jenis	Fungsi
Keterangan	Mengonversi nilai non-string menjadi string.
Contoh	Temukan semua bingkai dengan angka ganjil.
Alur kerja	Konversikan semua kolom "nomor frame" ke nilai string, dan daftar frame yang diakhiri dengan nilai ganjil.
Penggunaan	
string(frame.number) matches "[13579]$"<img width="1160" height="775" alt="image" src="https://github.com/user-attachments/assets/83df8ae0-b124-4110-8fc7-29381e1f9c22" />

Bookmark dan Tombol Penyaringan
Kita telah membahas berbagai jenis opsi pemfilteran, operator, dan fungsi. Sekarang saatnya membuat filter dan menyimpannya sebagai bookmark dan tombol untuk digunakan nanti. Seperti yang disebutkan pada tugas sebelumnya, toolbar filter memiliki bagian bookmark filter untuk menyimpan filter yang dibuat pengguna, yang membantu analis menggunakan kembali filter favorit/kompleks hanya dengan beberapa klik. Mirip dengan bookmark, Anda dapat membuat tombol filter yang siap digunakan hanya dengan satu klik. 

Membuat dan menggunakan bookmark <img width="958" height="759" alt="image" src="https://github.com/user-attachments/assets/7519669a-5923-4681-bb50-be4027573a3a" />

Membuat dan menggunakan tombol filter tampilan:
<img width="1233" height="851" alt="image" src="https://github.com/user-attachments/assets/dc51a370-9e64-454b-b25d-5dadef0f4171" />

Profil
Wireshark adalah alat multifungsi yang membantu analis melakukan analisis paket secara mendalam. Seperti yang telah kita bahas di ruang diskusi, beberapa preferensi perlu dikonfigurasi untuk menganalisis peristiwa spesifik yang diminati. Mengubah konfigurasi untuk setiap kasus investigasi cukup merepotkan, karena membutuhkan serangkaian aturan pewarnaan dan tombol filter yang berbeda. Di sinilah profil Wireshark berperan. Anda dapat membuat beberapa profil untuk kasus investigasi yang berbeda dan menggunakannya sesuai kebutuhan. Anda dapat menggunakan menu "Edit --> Configuration Profiles" atau bagian "pojok kanan bawah bilah status --> Profile" untuk membuat, memodifikasi, dan mengubah konfigurasi profil.

Jawablah pertanyaan-pertanyaan di bawah ini.

Temukan semua server Microsoft IIS. Berapa jumlah paket yang tidak berasal dari "port 80"?
21

Temukan semua server Microsoft IIS. Berapa jumlah paket yang memiliki "versi 7.5"?
71

Berapakah jumlah total paket yang menggunakan port 3333, 4444, atau 9999?
2235

Berapakah jumlah paket dengan "angka TTL genap"?
77289

Ubah profil menjadi "Kontrol Checksum". Berapa jumlah paket "Checksum TCP Buruk"?
34185

Gunakan tombol filter yang ada untuk memfilter lalu lintas. Berapa jumlah paket yang ditampilkan?
261

Kesimpulan
Selamat!

Anda baru saja menyelesaikan ruangan "Wireshark: Operasi Paket". Di ruangan ini, kita telah membahas statistik, filter, operator, dan fungsi Wireshark.

Ingin mempelajari lebih lanjut? Kami mengundang Anda untuk menyelesaikan  ruang Wireshark: Analisis Lalu Lintas  untuk meningkatkan keterampilan Wireshark Anda dengan menyelidiki aktivitas lalu lintas yang mencurigakan. 
