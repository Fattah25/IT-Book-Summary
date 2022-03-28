# Packet Traveling

[link referensi](https://www.practicalnetworking.net/series/packet-traveling/packet-traveling/)

Ketika data meninggalkan komputer kita, itu dikelompokkan menjadi potongan-potongan kecil yang disebut ***Packets*/Paket**. Paket ini pada dasarnya adalah amplop kecil yang membawa data melintasi Internet. [Lebih jelasnya di sini](Introduction-to-Networking.md#packet-and-routers)

OSI Model
=========

*Open Systems Interconnect model* (OSI Model) menjelaskan semua fungsi
individual yang diperlukan agar Internet dapat berfungsi.

Ini adalah sebuah perangkat yang memiliki tujuh fungsi *independen* yang digabungkan untuk mencapai tujuan akhir komunikasi **Komputer ke Komputer**.

Model OSI dibagi menjadi tujuh lapisan yang berbeda, yang masing-masing memenuhi fungsi yang sangata spesifik. Ketika digabungkan bersama, setiap fungsi berkontribusi memungkinkan komunikasi data komputer ke komputer (antar komputer).

| Application  | 7   |
| ------------ | --- |
| Presentation | 6   |
| Session      | 5   |
| Transport    | 4   |
| Network      | 3   |
| Data Link    | 2   |
| Physical     | 1   |

OSI Layer 1 - Physical
----------------------

Lapisan fisik (*physical layer*) model OSI bertanggung jawab untuk transfer bit-1 dan 0 yang membentuk semua kode komputer.

Lapisan ini mewakili media fisik yang mengatasi lalu lintas antara dua node. Contohnya adalah kabel **Ethernet** atau kabel serial kita. Tapi jangan terlalu terpaku pada kata “Fisik” - lapisan ini diberi nama pada tahun 1970-an, jauh sebelum komunikasi nirkabel dalam jaringan (*networking*) menjadi sebuah konsep. Dengan demikian WiFi, meskipun tidak memiliki fisik dan kehadiran nyata, juga dianggap sebagai **Layer 1 protocol**.

Sederhananya, **Layer 1 adalah segala sesuatu yang membawa 1 dan 0 antara dua
node.**

Format sebenarnya dari data pada “kabel” dapat bervariasi dengan setiap medium (perantara). Dalam kasus *Ethernet*, bit ditransfer dalam bentuk pulsa listrik (*electric pulses*)*.* Dalam kasus WiFi, bit ditransfer dalam bentuk gelombang radio. Dalam kasus *Fiber Optic*, bit ditransfer dalam bentuk pulsa cahaya (*light pulses*).

\<simpan gambar\>

Selain kabel fisik, *Repeater* dan *Hub* juga beroperasi pada lapisan ini.

sebuah *Repeater* sederhananya mengulangi sinyal dari satu medium ke medium lainnya, memungkinkan serangkaian kabel dirangkai bersama-sama dan meningkatkan
jangkauan sinyal yang dapat menempuh melebihi batasan kabel tunggal. Ini biasanya digunakan dalam penyebaran (*deployment*) WiFi skala besar, di mana satu jaringan WiFi “*repeated* / diulang” di beberapa titik akses untuk mencakup jangkauan yang lebih luas.

*Hub* hanyalah *Repeater* multi-port. Jika empat perangkat terhubung ke satu *Hub*, apapun yang dikirim oleh satu perangkat akan diulang ke tiga perangkat lainnya.

 

OSI Layer 2 - Data Link
-----------------------

*Data Link layer* dari OSI model bertanggung jawab untuk berinteraksi dengan *Physical Layer*. Secara efektif, Layer 2 bertanggung jawab untuk menempatkan 1 dan 0 pada kabel, dan mengambil 1 dan 0 dari kabel.

*Network Interface Card* (NIC) tempat kita menyambungkan kabel *Ethernet* menangani fungsionalitas Layer 2. Ini menerima sinyal dari kabel, dan mengirimkan sinyal ke kabel.

NIC WiFi kita bekerja dengan cara yang sama, menerima dan mentransmisikan gelombang radio yang kemudian ditafsirkan sebagai rangkaian 1 dan 0.

**Layer 2 kemudian akan mengelompokkan 1 dan 0 kedalam potongan yang dikenal sebagai Frames.**

Ada sistem pengalamatan (*addressing*) yang ada di Layer 2 yang dikenal sebagai *Media Access Control address* , atau MAC *address*. MAC *address* secara unik mengidentifikasi setiap NIC individual. Setiap NIC telah dikonfigurasi sebelumnya dengan alamat MAC oleh produsen; pada kenyataanya, terkadang disebut sebagai *Burned In Address* (BIA).

\<tambahkan gambar\>

Selain NIC kita, *Switch* juga beroperasi pada lapisan ini. **Tanggung jawab utama Switch adalah untuk memfasilitasi komunikasi dalam Jaringan** (lihat di sini).

Fungsi menyeluruh dari *Data Link layer* adalah untuk mengirimkan paket dari satu NIC ke NIC lainnya. Atau dengan kata lain, peran Layer 2 adalah mengirimkan paket dari *hop ke hop*.

OSI Layer 3-Network
-------------------

*Network layer* OSI model bertanggung jawab atas pengiriman paket dari ujung ke ujung (*end to end*).

Ini dilakukan dengan menggunakan skema pengalamatan lain yang secara logis dapat
mengidentifikasi setiap node yang terhubung ke Internet. Skema pengalamatan ini dikenal sebagai *Internet Protocol address*, atau **IP Address**.

Hal ini dianggap logis karena alamat IP bukan merupakan identifikasi permanen dari sebuah komputer. Berbeda dengan alamat MAC yang dianggap sebagai alamat fisik, alamat IP tidak dipasang ke perangkat keras komputer mana pun oleh pabrikan (*manufacturer*)*.*

\<letakkan gambar\>

*Router* (jamak) adalah perangkat jaringan (*Network devices*) yang beroperasi pada Layer 3 OSI model. Peran utama *Router* adalah memfasilitasi komunikasi antar jaringan. Dengan demikian, *Router* menciptakan batas antara dua jaringan. Untuk berkomunikasi dengan perangkat apa pun yang tidak secara langsung di jaringan kita, *router* harus digunakan.

OSI Model - Layer 2 vs. Layer 3
-------------------------------

Interaksi dan perbedaan antara Layer 2 dan Layer 3 sangat penting untuk dipahami bagaimana data mengalir antara dua komputer. Misalnya, jika kita sudah memiliki skema pengalamatan L2 yang unik di setiap NIC (seperti MAC address), mengapa kita memerlukan skema pengalamatan lain di L3 (seperti IP address)? Atau sebaliknya?

Jawabannya adalah bahwa kedua skema pengalamatan menyelesaikan fungsi yang berbeda:

- **Layer 2** menggunakan **MAC address** dan berperan untuk pengiriman paket dari **hop ke hop**.

- **Layer 3** menggunakan **IP address** dan berperan untuk pengiriman paket dari **end to end** (ujung ke ujung).

Saat komputer memiliki data untuk dikirim, komputer akan mengenkapsulasinya dalam *IP header* yang akan menyertakan informasi seperti IP *address* Sumber (*resource*) dan Tujuan (*destination*) dari dua komunikasi “**ends**/ujung“.

IP Header dan Data kemudian dienkapsulasi lebih lanjut dalam MAC *address header*, yang mana akan menyertakan informasi seperti MAC *address* Sumber (*source*) dan Tujuan (*destination*) dari “hop” di jalur saat ini (*path*) menuju tujuan akhir.

Berikut adalah ilustrasi untuk mengarahkan titik ini ke *home*:

\<gif ada di sini\>

Perhatikan di antara setiap *Router*, MAC *address header* dihapus dan dibuat ulang untuk mebawanya ke hop berikutnya. IP Header yang dihasilkan oleh komputer pertama hanya dihapus oleh komputer terakhir, oleh karena itu IP *header* menangani pengiriman “*end to end*”, dan masing-masing dari empat MAC *header* berbeda yang terlibat dalam animasi ini menangani pengiriman “*hop to hop*”.

OSI Layer 4 - Transport
-----------------------

*Transport layer* dari OSI model berperan untuk membedakan arus\* *jaringan* (network stream\*).

Di waktu tertentu pada komputer pengguna mungkin ada *browser* Internet yang terbuka, saat musik sedang *streamed* (diputar dengan koneksi internet), saat aplikasi *messenger* atau chat sedang berjalan. Masing-masing aplikasi ini mengirim dan menerima data dari Internet, dan semua data itu tiba dalam bentuk 1 dan 0 ke NIC komputer tersebut.

Sesuatu harus ada untuk membedakan mana 1 dan 0 milik *messenger* atau *browser* atau musik *streaming*. “Sesuatu” itu adalah Layer 4:

\<gambar di sini\>

**Layer 4 mengerjakan ini dengan menggunakan skema pengalamatan (addressing
scheme) yang dikenal sebagai Port Numbers.**

Secara khusus, ada dua metode untuk membedakan *network streams*. Mereka dikenal sebagai *Transmission Control Protocol* (TCP), atau *User Datagram Protocol* (UDP).

Baik TCP maupun UDP memiliki 65.536 *port numbers* (masing-masing), dan *stream* aplikasi yang unik diidentifikasi oleh *port* Sumber (*source*) dan Tujuan (*destination*) (dikombinasikan dengan IP *address* Sumber dan Tujuan).

TCP dan UDP menggunakan strategi yang berbeda dalam cara aliran data (*data stream**) ditransfer, dan perbedaan serta cara kerjanya menarik dan signifikan, yang mungkin akan dibahas di lain tempat.

Untuk meringkasnya, jika Layer 2 bertanggung jawab untuk pengiriman *hop to hop*, dan Layer 3 bertanggung jawab untuk pengiriman *end to end*, dapat dikatakan bahwa Layer 4 bertanggung jawab untuk pengiriman *service to service*.

OSI Layer 5, 6, and 7
---------------------

*Session*, *Presentation*, dan *Application layer* dari OSI model menangani langkah terakhir sebelum data yang ditransfer melalui jaringan (difasilitasi oleh lapisan 1-4) ditampilkan kepada pengguna akhir.

Dari perspektif murni Rekayasa Jaringan (*Network Engineering*), perbedaan antara Layer 5, 6, dan 7 tidak terlalu signifikan. Bahkan, ada model komunikasi Internet populer lainnya yang dikenal sebagai TCP/IP model, yang mengelompokkan ketiga lapisan ini kedalam satu cakupan Layer.

Perbedaan akan menjadi lebih signifikan jika kita terlibat dalam Rekayasa Perangkat Lunak (*Software Engineering*).

Encapsulation and Decapsulation
-------------------------------

Item terakhir yang perlu kita diskusikan sebelum kita beralih dari OSI Model adalah Enkapsulasi **(Encapsulation) dan Dekapsulasi (Decapsulation)**. Istilah-istilah ini mengacu pada **bagaimana data dipindahkan melalui Layers dari atas ke bawah saat dan dari bawah ke atas saat menerima**.

Saat data diserahkan dari *layer to layer*, setiap *layer* menambahkan informasi yang diperlukan untuk mencapai tujuannya sebelum datagram lengkap diubah menjadi 1 dan 0 dan dikirim melalui kabel. Sebagai contoh:

- Layer 4 akan menambahkan TCP *header* yang akan menyertakan *port* Sumber dan Tujuan.

- Layer 3 akan menambahkan IP *header* yang akan menyertakan IP *address* Sumber dan Tujuan.

- Layer 2 akan menambahkan *Ethernet header* yang akan menyertakan MAC *address* Sumber dan Tujuan.

Di sisi penerima, setiap *layer* menghapus *header* dari data dan meneruskannya kembali ke tumpukkan (*stack*) *Application layer*. Berikut adalah seluruh proses dalam tindakan:

\<taruh gif di sini\>

Perhatikan bahwa ini hanya sebuah contoh. *Header* yang akan ditambahkan akan tergantung pada protokol komunikasi yang mendasarinya. Misalnya, UDP *header* mungkin ditambahkan di Layer 4 sebagai gantinya, atau header IPv6 mungkin ditambahkan di Layer 3.

Apa pun itu, penting untuk dipahami bahwa saat data dikirim melalui kabel, data akan diteruskan ke tumpukan (*stack*) dan setiap *layer* menambahkan *header*-nya sendiri untuk membantunya mencapai tujuannya. Di sisi penerima, *header* dilepas satu per satu, *layer* demi *layer*, saat data dikirim kembali ke *Application layer*. 

Key Players
===========

Internet adalah perpaduan menarik dari banyak elemen berbeda yang semuanya bekerja bersama untuk menciptakan jaringan-jaringan di seluruh dunia yang memungkinkan miliaran perangkat yang berbeda untuk berkomunikasi.

Daftar ini jauh dari lengkap, tetapi akan mencakup “pemain dan kru” utama yang perlu kita ketahui untuk memahami bagaiaman sebuah paket (*packet*) berjalan melalui Internet.

Host
----

Istilah **host** adalah istilah umum yang menyiratkan segala jenis perangkat akhir (*end-device*) di Internet. Perangkat apa pun yang mungkin merupakan inisiasi *traffic* asli atau tujuan akhir *traffic* dapat dianggap sebagai host.

Contoh sederhananya adalah komputer atau laptop kita. Namun di zaman modern ini, ada lebih banyak lagi: ponsel, smart TV, jam tangan pintar, mobil tertentu, dan bahkan beberapa lemari es!

\<image here\>

Host menjalankan perangkat lunak (*software*) dan aplikasi untuk berinteraksi dengan *end user*, dan itu juga pada titik tertentu perlu menempatkan bit pada kabel. Dengan demikian, dikatakan bahwa Host beroperasi di semua tujuh *layer* OSI model.

Dalam komunikasi internet atau lalu lintas jaringan yang khas, dua host dalam komunikasi sering diberi label sebagai Klien (*client*) atau *Server*.

**Klien adalah entitas yang memulai permintaan** dan sedang mencari untuk memperoleh informasi atau data atau layanan. Sedangkan **Server adalah entitas yang menerima permintaan** dan memiliki informasi, data, atau layanan yang diinginkan oleh klien.

Perlu diperhatikan bahwa istilah ini relatif terhadap jenis komunikasi tertentu.

Misalnya, saat laptop kita menjelajahi halaman web, laptop kita bertindak sebagai Klien dan *Web Server* bertindak sebagai Server. Tetapi ketika *Web Server* yang sama itu kemudian mengunduh pembaruan perangkat lunak, maka *Web Server* tersebut bertindak sebagai Klien dan berkomunikasi dengan *Update Server*.

Network
-------

Jaringan / *Network* hanyalah dua atau lebih perangkat yang terhubung - biasanya dikelompokkan bersama berdasarkan tujuan atau lokasi fisik yang serupa. Sebuah jaringan dapat mengambil banyak bentuk yang berbeda, misalnya:

- Sekelompok PC di ruang kelas semuanya berada dalam ruang fisik yang sama dan semuanya akan tergabung dalam satu jaringan / *Network*.

- Setiap jaringan rumah tipikal akan mencakup beberapa laptop, ponsel, atau printer yang semuanya terikat ke alamat fisik yang sama. Oleh karena itu, semua tergolong jaringan yang sama.

- Sebuah kedai kopi yang memiliki WiFi akan memungkinkan setiap pelanggannya terhubung ke Jaringan WiFi yang sama.

- Perusahaan besar mungkin menggunakan banyak jaringan, sering kali memisahkannya berdasarkan peran pekerjaan. Misalnya, satu jaringan untuk semua akuntannya dan jaringan lain untuk semua insinyurnya.

Bergantung pada tujuan setiap jaringan, perangkat di dalamnya kemudian akan berkomunikasi dengan perangkat lain di jaringan yang sama atau perangkat lain di
jaringan yang berbeda.

Setiap kali salah satu *Key Players* yang dibahas dalam sisa seri artikel ini terhubung satu sama lain, kita memiliki jaringan. Faktanya, seluruh **Internet** tidak lebih dari serangkaian jaringan yang saling terhubung *(Inter-connected networks*)*.*

Switch
------

*Switch* adalah *network device* yang tujuan utamanya adalah untuk memfasilitasi komunikasi dalam jaringan.

*Switch* beroperasi pada Layer 2 OSI *model*, yang berarti *switch* hanya memeriksa ke setiap *data-gram* hingga *header* Layer 2. *Header* Layer 2 berisi informasi yang memungkinkan pengiriman *hop to hop*, seperti MAC *address* Sumber dan Tujuan.

\<gambar ada di sini\>

Satu *Switch* beroperasi dengan mempertahankan apa yang dikenal sebagai **MAC Address table**. Ini adalah tabel yang memetakan MAC *address* perangkat yang dicolokkan ke setiap *switch port*. *Switch* tipikal memiliki banyak port, dari 24 hingga 48, hingga 96, atau lebih.

MAC Address Table diisi dengan melihat bidang MAC *address* Sumber dari setiap
*frame* yang diterima.

Untuk meneruskan *frame*, *Switch* akan mencari MAC *address* Tujuan (*destination*) di Tabel MAC *address*-nya untuk menentukan port yang akan digunakan.

Jika *Switch* menemui *frame* yang tidak diketahui lokasi MAC *address* Tujuannya, Switch hanya akan menduplikasi dan membanjiri *frame* keluar dari setiap port *switch* (Kecuali port yang menerimanya).

Router
------

*Router* adalah *network device* yang tujuan utamanya adalah untuk memfasilitasi komunikasi antar jaringan. Setiap *interface* pada *router* menciptakan batas jaringan (*network boundary*).

Router beroperasi pada Layer 3 OSI Model, yang berarti mereka hanya melihat ke setiap datagram hingga Layer 3 *header*. Layer 3 *header* berisi informasi yang memungkinkan pengiriman *end to end*, seperti IP *address* Sumber dan Tujuan (*destination*).

\<gambar di sini\>

Pada gambar di atas, perhatikan bahwa *router* di sebelah kiri (R1) dan *router* di sebelah kanan (R2) membuat tiga jaringan terpisah (11.11.11.x, 22.22.22.x, dan 33.33.33.x). *Interface* R1 kanan dan *interface* R2 kiri keduanya berada di jaringan yang sama.

Satu-satunya cara bagi **Klien di jaringan 11.11.11.x untuk berbicara adalah dengan meneruskan paket ke R1, yang pada gilirannya akan meneruskan paket ke R2 yang kemudian akhirnya akan meneruskan paket ke Server**.

*Router *menyelesaikan semua ini dengan mempertahankan apa yang dikenal sebagai Tabel Perutean (*Routing Table*). Ini adalah tabel yang berisi jalur-jalur (*paths*) ke semua jaringan yang dapat dijangkau oleh *Router*. Jalur ini kadang-kadang dikenal sebagai *Rutes*, dan setiap entri berisi IP *Network* dan *interface* atau IP *address* dari *router* berikutnya di jalur tujuan / target.

Ada beberapa cara *Router* dapat mempelajari jaringan dan mengisi Tabel Perutean-nya. Kita akan melihat beberapa cara tersebut dalam artikel selanjutnya dalam seri ini.

Perlu diingat, dari sudut pandang setiap *router*, *Route Table* adalah peta dari setiap jaringan yang ada. Jika *router* menerima paket yang ditujukan ke jaringan yang tidak diketahuinya, maka sejauh menyangkut *router* tersebut, jaringan tersebut tidak boleh ada. Oleh karena itu, saat *router* menerima paket yang ditujukan ke jaringan yang tidak ada dalam Tabel peruteannya, paket tersebut akan dibuang.

Address Resolution Protocol (ARP)
---------------------------------

Sebelumnya kita telah membahas bahwa MAC *address* adalah skema pengalamatan
Layer 2. Kita juga membahas bahwa IP *address* adalah skema pengalamtan Layar 3.

\<gambar di sini\>

Yang menjembatani kedua skema / protokol pengalamatan (*addressing*) ini adalah *Address Resolution Protocol* (ARP).

Biasanya, ketika dua host berkomunikasi, mereka sudah mengetahui IP *address* masing-masing. Mereka mengetahui IP *address* satu sama lain dari berbagai metode: terkadang diberikan secara manual oleh *user*, terkadang oleh protokol lain (seringkali DNS). Namun metode sebenarnya yang digunakan tidak relevan (setidaknya untuk seri artikel ini).

Namun, yang pasti tidak diketahui adalah MAC *address-* nya. Host akan menggunakan ARP untuk menemukan MAC *address* yang sesuai. Dengan kata lain, ARP akan menggunakan IP *address* yang diketahui, dan menemukan MAC *address* yang
tidak diketahui. Pemetaan yang ditemukan kemudian ditambahkan dan disimpan dalam ARP Tabel, yang merupakan pemetaan IP *address* ke MAC *address* yang berkorelasi.

Bagaimana L2 dan L3 dijembatani bersama, dan peran ARP dalam proses akan di jelaskan di sini  menggunakan ilustrasi berikut: 

\<gambar di sini\>

Pada gambar di atas, ada tiga jaringan: jaringan ungu, jaringan abu-abu, dan jaringan merah. Kita akan menggunakan diagram ini untuk menggambarkan dua contoh ARP: Pertama ketika sebuah host berkomunikasi ke host lain di jaringan yang sama (*Client to Purple server*). Dan Kedua ketika sebuah host berbicara dengan host lain di jaringan yang berbeda (*Client to Red server*).

Ketika Klien perlu berbicara dengan Server Ungu, ia kana mengetahui IP *address* Server Ungu, dan dari sanalah akan ditentukan bahwa Server Ungu ada di jaringan lokal (LAN). Ketika Klien mencoba untuk berbicara dengan host di jaringan yang sama, Klien akan mengedarkan ARP *request* untuk MAC *address* host.

ARP akan memungkinkan Klien untuk menyelesaikan Layer 2 *header* seperti
berikut:

\<gambar di sini\>

Saat Klien perlu berbicara dengan Server Merah, Klien akan mengetahui IP *address* Server Merah, dan dari situ Klien akan mengetahui bahwa server Merah ada di jaringan asing. Dengan demikian, paket (*packet*) harus dikirimkan ke router terdekat - atau dikenal sebagai *Default Gateway*.

Klien umumnya sudah dikonfigurasi dengan *Default Gateway* - yang dapat kita ketahui dari gambar adalah R1. Ketika Klien mencoba untuk berkomunikasi dengan host di jaringan asing, Klien akan menyebarkan ARP *request* untuk MAC *address Gateway Default*.

Ini akan memungkinkan Klien untuk mengisi Layer 3 *header* dan Layer 2 sebagai
berikut:

\<di sini gambar\>

Untuk meringkas operasi ARP:

- Saat Klien berkomunikasi dengan host di jaringan yang sama, Klien akan
  (melakukan) ARP untuk MAC *address host*.

- Saat Klien berkomunikasi dengan host di jaringan yang berbeda, Klien akan
  ARP untuk MAC *address Gateaway Default*.

Ingat, pengiriman paket selalu menjadi tugas Layer 2, dan tujuan utama Layer 2
adalah mendapatkan paket dari *hop to hop*. Sebaliknya, Layer 3, yang berkaitan
dengan pengiriman *end to end* tidak dapat menempatkan paket pada kabel dan
mengirimkannya ke NIC host lain. Peran ARP adalah untk membantu klien membuat L2
*header* yang tepat, berdasarkan L3 *header*, untuk mendapatkan paket dari satu
*hop to hop* berikutnya.

Perlu juga dicatat bahwa setiap perangkat yang bermaksud meneruskan paket berdasarkan IP *address* (L3), juga harus memiliki kemampuan untuk mengirimkan paket ke hop berikutnya (L2). Dengan demikian, perangkat apa pun yang menggunakan IP *address* juga harus menggunakan ARP untuk mengirimkan paket menggunakan MAC *address*. Akibatnya, semua Layer 3 *devices* harus memelihara
***ARP Table***.

## Summary

Pada artikel ini, kita membahas tujuan utama dari lapisan yagn berbeda dari model OSI. Secara khusus:

- OSI Layer 1 adalah media fisik (*physical medium*) yang membawa 1 dan 0 melintasi kabel / *wire*.

- OSI Layer 2 bertanggung jawab atas pengiriman *hop to hop* dan menggunakan MAC *address*.

- OSI Layer 3 bertanggung jawab untuk pengiriman *end to end* dan menggunakan IP *address*.

- OSI Layer 4 bertanggung jawab atas pengiriman *service to service* dan menggunakan *Port Numbers*.

Kita juga membahas beberapa *Key Players* yang terlibat dalam memindahkan paket melalui Internet:

- Swithces memfasilitasi komunikasi *dalam* jaringan dan beroperasi di Layer 2

- Routers memfasilitasi komunikasi *antar* jaringan dan beroperasi di Layer 3 

- ARP menggunakan IP *address* yang diketahui untuk memecahkan  MAC *address* yang tidak diketahui.

Kita juga membahas tiga tabel berbeda yang digunakan untuk menyimpan pemetaan (*mapping*) yang berbeda:

- Switch menggunakan MAC *Address Table* yang merupakan pemetaan / *mapping* *Witchports* ke MAC *address* yang terhubung.

- Router menggunakan *Routing Table* / Tabel perutean yang merupakan pemetaan jaringan yang diketahui (*known Networks*) ke *interface* atau alamat *hop* berikutnya (*next-hop addresses*).

- Semua L3 *devices* menggunakan ARP *Table* yang merupakan pemetaan / *mapping* IP *Address* ke MAC *address*.



# Host to Host Communication
