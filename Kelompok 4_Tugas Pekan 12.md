## Tugas Kelompok 4 [Pekan 12]

**Anggota Kelompok dan Peran:**
- Muhammad Ayash Az dzikri 10231060 - Network Engineer
- Cintya Widhi Astuti 10231026 - Security & Documentation Specialist 
- Riqqah Khalda Karina 10231082 - Network Architect
- Verina Rahma Dinah 10231090 - Network Services Specialist

#### **Tugas Kelompok:** 

1. Konfigurasi routing statis pada jaringan intra-gedung.
2. Implementasi routing dinamis (OSPF) untuk koneksi antar-gedung.
3. Simulasi koneksi WAN antar gedung.

### Deliverable (Format Markdown):
- **Laporan Implementasi Tahap 2**, berisi:
- Link file simulasi yang diperbarui.
- **WAJIB**: Dokumentasi konfigurasi CLI lengkap untuk routing statis dan OSPF di semua router:
```markdown
### OSPF Configuration on Router1
```bash
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
...
```

- Screenshot tabel routing pada router utama dengan penjelasan detail.
- Hasil pengujian konektivitas antar-gedung dengan screenshot dan penjelasan.
- Analisis performa routing dinamis vs statis.

**Pendahuluan**

**Latar Belakang**

PT. Nusantara Network merupakan perusahaan teknologi informasi yang sedang berkembang dengan struktur organisasi yang terdiri dari 5 departemen utama yang tersebar di 2 gedung yang berbeda, yaitu kantor pusat (Gedung A) dan kantor cabang (Gedung B). Seiring dengan perkembangan bisnis dan kompleksitas operasional perusahaan, kebutuhan akan infrastruktur jaringan yang mudah dikelola, aman, dan efisien menjadi semakin krusial.

Infrastruktur jaringan yang digunakan saat ini belum sepenuhnya mampu memenuhi kebutuhan tersebut, khususnya dalam hal keamanan data, manajemen traffic, serta kemudahan pengelolaan jaringan secara terpusat. Selain itu, belum adanya pengaturan pembagian akses antar departemen secara optimal menimbulkan potensi celah keamanan dan inefisiensi dalam komunikasi data antar unit kerja. Oleh karena itu, diperlukan perancangan ulang infrastruktur jaringan yang dapat mengakomodasi kebutuhan perusahaan secara menyeluruh.

**Tujuan**

Perancangan jaringan ini bertujuan untuk:
* Membangun jaringan yang aman dan efisien melalui segmentasi VLAN.
* Menyediakan konektivitas antar gedung menggunakan teknologi WAN.
* Mengatur akses internet dengan implementasi NAT.
* Menyediakan layanan DHCP dan DNS untuk pengelolaan IP dan resolusi nama.
* Menerapkan ACL untuk pembatasan akses antar departemen.
* Menggunakan OSPF sebagai routing dinamis antar lokasi.
* Menyediakan sistem monitoring jaringan secara terpusat.

**Ruang Lingkup**

Perancangan ini mencakup seluruh struktur jaringan di kantor pusat dan kantor cabang.Ruang lingkupnya meliputi segmentasi jaringan berdasarkan departemen, konektivitas antar lokasi melalui WAN, konfigurasi layanan internet, pengelolaan alamat IP dan DNS, pengaturan hak akses melalui ACL, serta penerapan routing dinamis.

**Isi Laporan**

### 1. Konfigurasi routing statis pada jaringan intra-gedung.

<img src = Statis.A.jpg >

Switch di Gedung A memiliki beberapa subnet yang terhubung langsung melalui interface VLAN, yaitu VLAN10 hingga VLAN60. Masing-masing subnet yang terdaftar dalam tabel routing memiliki jenis rute C (Connected), yang berarti jaringan tersebut terhubung langsung ke switch. Subnet-subnet yang terhubung langsung adalah 192.168.10.0/26 (VLAN10), 192.168.20.0/26 (VLAN20), 192.168.30.0/27 (VLAN30), 192.168.40.0/28 (VLAN40), 192.168.50.0/26 (VLAN50), dan 192.168.60.0/26 (VLAN60). Baris "Gateway of last resort is not set" menunjukkan bahwa default route belum dikonfigurasi pada switch ini. Artinya, switch di Gedung A hanya bisa mengarahkan lalu lintas jaringan ke jaringan-jaringan yang terdaftar dalam tabel routing lokal tanpa memiliki rute untuk menghubungkan jaringan tersebut ke luar gedung atau jaringan eksternal. Untuk memungkinkan konektivitas antar gedung, perlu dikonfigurasi static route atau gateway default menuju router yang menghubungkan gedung tersebut dengan gedung lain. 

<img src = StatisB.jpg >

Di sisi lain, Gedung B juga menggunakan Switch Layer 3 dengan konfigurasi yang hampir sama. Switch ini memiliki VLAN yang terhubung langsung ke subnet-subnet seperti 192.168.10.0/26 (VLAN10), 192.168.20.0/26 (VLAN20), 192.168.30.0/27 (VLAN30), 192.168.40.0/28 (VLAN40), 192.168.50.0/26 (VLAN50), dan 192.168.60.0/26 (VLAN60). Semua entri ini juga bertanda C (Connected), yang berarti perangkat di setiap subnet dapat saling berkomunikasi secara langsung. Seperti di Gedung A, Gedung B juga tidak memiliki default route atau gateway of last resort yang ditetapkan, sehingga switch ini tidak dapat mengarahkan paket data ke jaringan eksternal atau antar-gedung. Untuk memperluas komunikasi antar gedung atau menghubungkan ke jaringan luar, diperlukan pengaturan static route atau pengaturan gateway default menuju router penghubung antar gedung.

### 2. Implementasi routing dinamis (OSPF) untuk koneksi antar-gedung dan simulasi koneksi WAN antar gedung.

<img src = DinamisA.jpg >

Dalam konfigurasi ini, seorang teknisi jaringan mengatur router untuk berkomunikasi melalui koneksi WAN dengan router lain dan menjalankan protokol OSPF untuk pertukaran rute dinamis. Teknisi memulai dengan masuk ke mode privileged (enable) dan masuk ke mode konfigurasi global (configure terminal). Kemudian, interface GigabitEthernet0/1 dipilih dan diberikan deskripsi to_Router0, yang bertujuan untuk memberikan penanda dokumentasi bahwa interface tersebut terhubung ke Router0. Interface ini kemudian diaktifkan dengan perintah no shutdown, yang memunculkan pesan bahwa status link dan protokol telah berubah menjadi aktif (up).

Selanjutnya, interface tersebut diberi IP address 192.168.100.1 dengan subnet mask 255.255.255.252. Ini adalah pasangan dari konfigurasi pada router sebelumnya, yaitu IP 192.168.100.2, yang membentuk koneksi point-to-point antar kedua router melalui jaringan WAN. Setelah itu, teknisi mengaktifkan routing dinamis dengan menjalankan protokol OSPF melalui perintah router ospf 1. Dua jaringan dimasukkan dalam OSPF area 0:

* 10.10.10.0/30 sebagai jaringan LAN lokal di gedung ini.

*192.168.100.0/30 sebagai jaringan koneksi WAN menuju router lain.

Dengan konfigurasi ini, router akan berpartisipasi dalam pertukaran informasi rute melalui OSPF, memungkinkan router-router lain dalam area yang sama untuk secara otomatis mengetahui dan memperbarui informasi jalur, menciptakan konektivitas dinamis antar gedung yang handal.

<img src = DinamisB.jpg >

Pada konfigurasi tersebut, teknisi jaringan sedang melakukan pengaturan pada sebuah router untuk mengaktifkan koneksi antar-gedung melalui jaringan WAN dan menjalankan protokol routing dinamis OSPF. Proses konfigurasi dimulai dengan masuk ke mode konfigurasi global (configure terminal) setelah sebelumnya masuk ke mode privileged (enable). Kemudian, teknisi jaringan mengakses interface GigabitEthernet0/1, yang diberi deskripsi sebagai koneksi menuju Router2. Interface tersebut diaktifkan menggunakan perintah no shutdown, yang ditandai oleh munculnya pesan status bahwa interface telah berubah menjadi aktif (up).

Setelah interface aktif, diberikan alamat IP 192.168.100.2 dengan subnet mask 255.255.255.252. Subnet ini tergolong sangat kecil (prefix /30), yang umum digunakan untuk koneksi point-to-point antar router dalam jaringan WAN karena hanya menyediakan dua alamat IP yang bisa digunakan. Selanjutnya, teknisi jaringan mengonfigurasi routing dinamis dengan mengaktifkan protokol OSPF (Open Shortest Path First) menggunakan perintah router ospf 1. Dua jaringan kemudian dimasukkan ke dalam proses OSPF area 0:

* Jaringan 10.10.10.0/30, yang kemungkinan besar adalah jaringan lokal atau LAN dalam gedung.

* Jaringan 192.168.100.0/30, yang merupakan koneksi WAN antar router (antar gedung).

Dengan konfigurasi ini, router akan menjalankan OSPF pada kedua jaringan tersebut, memungkinkan pertukaran informasi routing secara otomatis dengan router lain yang juga menjalankan OSPF di area yang sama. Hal ini memastikan konektivitas yang dinamis dan efisien antar gedung melalui jaringan WAN.

### Performa routing statis vs dinamis

| **Aspek**                    | **Routing Statis**                                                                                     | Routing Dinamis OSPF                                                                                     |
|-----------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| Tipe Perangkat           | Diterapkan pada *Switch Layer 3*, fokus pada routing antar VLAN (*intra*-gedung)                      | Diterapkan pada *Router*, fokus pada komunikasi antar-gedung melalui WAN                                     |
| Konfigurasi Jaringan     | Hanya mendukung jaringan internal melalui VLAN (VLAN10–VLAN60), tanpa koneksi ke luar                 | Mendukung pertukaran rute antar gedung melalui jaringan WAN                                                  |
| Kemampuan Adaptasi       | Tidak bisa beradaptasi otomatis terhadap perubahan topologi                                            | Bisa beradaptasi otomatis jika ada perubahan atau kegagalan jalur                                            |
| Manajemen dan Skalabilitas| Lebih rumit jika jaringan berkembang (harus konfigurasi ulang static route satu per satu)             | Lebih mudah dikembangkan karena OSPF otomatis menyebarkan dan memperbarui informasi rute                     |
| Penggunaan Sumber Daya   | Lebih ringan karena hanya menangani rute yang dikonfigurasi manual                                    | Membutuhkan lebih banyak sumber daya karena menghitung jalur optimal secara berkala                          |
| Respon terhadap Gangguan | Tidak ada respon otomatis, perlu campur tangan manual                                                 | Respon otomatis terhadap gangguan jaringan, mencari jalur alternatif                                         |
| Keamanan                 | Lebih aman karena tidak menerima informasi rute dari luar                                             | Perlu pengamanan tambahan untuk mencegah update OSPF yang tidak sah                                          |
| Default Gateway          | Tidak disetel, menyebabkan perangkat tidak bisa mengakses jaringan luar                               | Tidak bermasalah, karena OSPF mendistribusikan informasi jalur otomatis                                      |
| Cakupan Jaringan         | Terbatas pada jaringan lokal (*intra*-gedung)                                                         | Mencakup jaringan lokal dan konektivitas antar-gedung melalui WAN                                            |

 