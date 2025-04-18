## Tugas Kelompok 4 [Pekan 10]

**Anggota Kelompok dan Peran:**
- Muhammad Ayash Az dzikri 10231060 - Network Engineer
- Cintya Widhi Astuti 10231026 - Security & Documentation Specialist 
- Riqqah Khalda Karina 10231082 - Network Architect
- Verina Rahma Dinah 10231090 - Network Services Specialist


### Deliverable (Format Markdown):
- **Dokumen Desain Jaringan, berisi**: 
    - Diagram topologi fisik dan logis (gambar yang diunggah dalam markdown dengan penjelasan mende
    - Tabel pengalamatan IP (subnet, VLAN ID, gateway, range, dsb). 
    - Daftar perangkat yang dibutuhkan (router, switch, server, dsb). 
    - Rencana penerapan VLAN (VLAN ID, nama, tujuan). 
    - **WAJIB**: Awal implementasi dalam Packet Tracer dengan screenshot topologi dasar (disertai penjelasan detail untuk setiap gambar).

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

***Diagram topologi fisik***

<img src = topologi.png >

Topologi jaringan ini menggunakan jenis topologi gabungan antara topologi star (bintang) dan extended star (bintang bertingkat). Di tingkat paling dasar, setiap departemen menggunakan topologi star, yaitu semua komputer dalam satu ruangan atau divisi terhubung ke satu switch Layer 2, yaitu Cisco 2960. Switch ini mengatur lalu lintas data lokal antar perangkat dalam departemen tersebut.

Setiap Switch 2960 di departemen kemudian terhubung ke Main Switch, yaitu Switch 3560, yang berfungsi sebagai switch Layer 3. Dengan ini, terbentuk topologi extended star, di mana semua koneksi dari masing-masing switch departemen dikumpulkan dan dikelola di satu pusat.

***Struktur & Lokasi Perangkat:***
**GEDUNG A**

Main Router A adalah router utama yang menghubungkan Gedung A dengan jaringan luar dan Gedung B. Router ini mendukung OSPF untuk komunikasi antar gedung, NAT untuk akses ke internet, serta ACL untuk mengatur keamanan jaringan. Router ini terhubung langsung ke Main Switch 3560 A.

Main Switch 3560 A bertindak sebagai pusat manajemen VLAN dan pengatur lalu lintas antar departemen. Semua Switch 2960 dari departemen-departemen di Gedung A terhubung ke switch ini.

Departemen IT memiliki 2 unit Switch 2960, masing-masing terhubung ke 20 komputer, total 40 PC. Kedua switch ini terhubung langsung ke Main Switch 3560 A.

Departemen Keuangan menggunakan 2 unit Switch 2960 untuk menghubungkan 25 PC, juga langsung terhubung ke Main Switch 3560 A.

Departemen SDM memiliki 1 Switch 2960 untuk 20 PC dan langsung terkoneksi ke Main Switch.

Server Farm menggunakan 1 Switch 2960 yang menghubungkan 10 server, seperti Web Server, DNS, DHCP, File Server, dan lainnya. Switch ini juga tersambung ke Main Switch agar seluruh jaringan dapat mengakses layanan dari server tersebut.

**GEDUNG B**

Main Router B memiliki fungsi yang sama dengan Main Router A. Router ini mengatur komunikasi antar gedung dengan OSPF, menyediakan NAT untuk internet, dan ACL untuk keamanan. Router ini terhubung ke Main Switch 3560 B serta terkoneksi ke Main Router A untuk komunikasi dua arah antar gedung.

Main Switch 3560 B adalah pusat penghubung di Gedung B. Switch ini menyambungkan semua Switch 2960 dari departemen-departemen dan mengatur lalu lintas VLAN di dalam gedung.

Departemen Marketing memiliki 2 Switch 2960, masing-masing terhubung ke 15 komputer, total 30 PC. Kedua switch ini tersambung ke Main Switch 3560 B.

Departemen Operasional juga memiliki 2 Switch 2960 untuk 35 komputer. Keduanya juga terhubung langsung ke Main Switch 3560 B.

Dalam jaringan ini, komunikasi antar perangkat bergantung pada lokasi perangkat tersebut berada.

Jika dua komputer berada dalam satu departemen yang sama, misalnya antar komputer di Departemen IT, maka data akan mengalir cukup melalui Switch Cisco 2960 yang ada di departemen itu. Artinya, pertukaran data terjadi secara langsung tanpa perlu melewati perangkat jaringan lain di luar departemen.

Jika sebuah komputer ingin mengakses server yang ada di Server Farm (masih dalam satu gedung), data akan dikirim terlebih dahulu ke Switch Cisco 2960 di departemen, lalu diteruskan ke Main Switch Cisco 3560 di gedung tersebut. Setelah itu, Main Switch akan mengarahkan data ke Switch 2960 di Server Farm, sehingga data sampai ke server tujuan.

Jika sebuah komputer di Gedung B ingin berkomunikasi dengan perangkat di Gedung A, maka alur komunikasinya akan lebih panjang. Data dari komputer akan dikirim ke Switch 2960 di departemen, lalu ke Main Switch Cisco 3560 B, kemudian diteruskan ke Main Router B. Dari sana, data dikirim ke Main Router A di Gedung A melalui koneksi WAN. Setelah itu, data diteruskan ke Main Switch Cisco 3560 A, dan kemudian sampai ke perangkat tujuan di Gedung A, baik itu komputer lain atau server.

Semua proses ini berlangsung sangat cepat dan diatur oleh perangkat jaringan seperti router dan switch, dengan dukungan pengaturan seperti VLAN, OSPF, dan ACL untuk memastikan jalur data tepat sasaran dan aman.


***Tabel pengalamatan IP (subnet, VLAN ID, gateway, range, dsb).***

 | Departemen    | Subnet IP         | VLAN ID | Network Address   | Gateway         | Usable IP Range                     | Jumlah Host | Broadcast Address   |
|---------------|-------------------|---------|--------------------|------------------|--------------------------------------|--------------|----------------------|
| IT            | 192.168.10.0/26   | 10      | 192.168.10.0       | 192.168.10.1     | 192.168.10.1 – 192.168.10.62         | 62           | 192.168.10.63        |
| Keuangan      | 192.168.20.0/26   | 20      | 192.168.20.0       | 192.168.20.1     | 192.168.20.1 – 192.168.20.62         | 62           | 192.168.20.63        |
| SDM           | 192.168.30.0/27   | 30      | 192.168.30.0       | 192.168.30.1     | 192.168.30.1 – 192.168.30.30         | 30           | 192.168.30.31        |
| Server Farm   | 192.168.40.0/28   | 40      | 192.168.40.0       | 192.168.40.1     | 192.168.40.1 – 192.168.40.14         | 14           | 192.168.40.15        |
| Marketing     | 192.168.50.0/26   | 50      | 192.168.50.0       | 192.168.50.1     | 192.168.50.1 – 192.168.50.62         | 62           | 192.168.50.63        |
| Operasional   | 192.168.60.0/26   | 60      | 192.168.60.0       | 192.168.60.1     | 192.168.60.1 – 192.168.60.62         | 62           | 192.168.60.63        |


***Daftar perangkat yang dibutuhkan:***

| Jenis Perangkat         | Jumlah   | Lokasi                                     |
|-------------------------|----------|--------------------------------------------|
| Router                  | 2 unit   | 1 di Gedung A, 1 di Gedung B               |
| Switch Layer 3          | 2 unit   | 1 di Gedung A, 1 di Gedung B               |
| Switch Layer 2 (24 port)| 10 unit   | **Gedung A:**                              |
|                         |          | - IT: 2 unit                               |
|                         |          | - Keuangan: 2 unit                         |
|                         |          | - SDM: 1 unit                              |
|                         |          | - Server Farm: 1 unit (Gigabit/10G)        |
|                         |          | **Gedung B:**                              |
|                         |          | - Marketing: 2 unit                        |
|                         |          | - Operasional: 2 unit                      |
| Server                  | 10 unit  | Gedung A (Server Farm)                     |
| Komputer                | 150 unit | **Gedung A:**                              |
|                         |          | - IT: 40 unit                              |
|                         |          | - Keuangan: 25 unit                        |
|                         |          | - SDM: 20 unit                             |
|                         |          | **Gedung B:**                              |
|                         |          | - Marketing: 30 unit                       |
|                         |          | - Operasional: 35 unit                     |

***Rencana penerapan VLAN:***

| VLAN ID | Nama          | Tujuan                                                                         |
|---------|---------------|--------------------------------------------------------------------------------|
| 10      | VLAN_IT       | Mengisolasi jaringan IT untuk keamanan sistem dan manajemen perangkat jaringan |
| 20      | VLAN_Keuangan | Melindungi data keuangan sensitif dengan isolasi jaringan yang ketat           |
| 30      | VLAN_SDM      | Mengamankan data karyawan dan kebijakan HR dari akses tidak sah                |
| 40      | VLAN_Server   | Mengelompokkan semua server untuk keamanan tinggi dan manajemen terpusat       |
| 50      | VLAN_Marketing| Mendukung kebutuhan bandwidth tinggi untuk kegiatan pemasaran digital          |
| 60      | VLAN_Ops      | Menjamin kestabilan jaringan untuk operasional harian dan sistem produksi      |




