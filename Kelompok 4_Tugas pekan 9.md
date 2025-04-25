### Tugas Kelompok 4 [Pekan 9]

1. Pembentukan kelompok dan pembagian peran.
2. Analisa kebutuhan PT. Nusantara Network.
3. Brainstorming desain jaringan awal.

### Deliverable (Format Markdown):
- **Dokumen Perencanaan Proyek**, berisi:
  - Daftar anggota kelompok dan peran masing-masing.
  - Analisis kebutuhan jaringan dari studi kasus.
  - Timeline rencana kerja untuk 7 pekan.
  - Sketsa awal desain jaringan (gambar yang diunggah dalam markdown dengan penjelasan detail).

**PT. Nusantara Network - Pekan 9**

**Anggota Kelompok dan Peran:**
- Muhammad Ayash Az dzikri 10231060 - Network Engineer
- Cintya Widhi Astuti 10231026 - Security & Documentation Specialist 
- Riqqah Khalda Karina 10231082 - Network Architect
- Verina Rahma Dina 10231090 - Network Services Specialist

Daftar Isi
1. [Pendahuluan](#pendahuluan)
2. [Isi Laporan](#isi-laporan)
3. [Konfigurasi Perangkat](#konfigurasi-perangkat)
4. dst…

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

Analisis kebutuhan jaringan dari studi kasus.
Dalam studi kasus ini, dilakukan perkiraan terhadap komponen jaringan serta kebutuhan yang diperlukan untuk Gedung A dan Gedung B. Perusahaan memiliki dua gedung operasional, di mana masing-masing gedung terdiri dari beberapa departemen dengan kebutuhan jaringan yang spesifik.

**Kantor Pusat (Gedung A):**

* Departemen IT (40 unit komputer)
* Departemen Keuangan (25 unit komputer)
* Departemen Sumber Daya Manusia (20 unit komputer)
* Server Farm (10 unit server untuk berbagai layanan jaringan)

**Kantor Cabang (Gedung B):**

* Departemen Marketing (30 unit komputer)
* Departemen Operasional (35 unit komputer)

    **Perangkat Jaringan Fisik yang diperlukan**

    1. Router
        * Digunakan sebagai main router di masing-masing gedung.
        * Diperlukan 1 unit router untuk setiap gedung (total 2 router).
        * Setiap router harus mendukung fitur OSPF, NAT, ACL, dan koneksi WAN.

    2. Switch Layer 3
        * Berfungsi sebagai main switch untuk manajemen VLAN dan routing internal antar VLAN.
        * Diperlukan 1 unit switch Layer 3 untuk setiap gedung (total 2 switch).

    3. Switch Layer 2
        * Digunakan untuk koneksi perangkat-perangkat dalam departemen.
        * Gedung A:
           -  Departemen IT: 2 switch (24 port)
           -  Departemen Keuangan: 1 switch (24 port)
           -  Departemen SDM: 1 switch (24 port)
           - Server Farm: 1 switch (24 port, Gigabit/10G untuk server)
        * Gedung B:
           - Departemen Marketing: 2 switch (24 port)
           - Departemen Operasional: 2 switch (24 port)
           - Total: 9 unit switch Layer 2, diletakkan sesuai dengan masing-masing departemen.
    4. Server
        * Digunakan untuk menjalankan berbagai layanan jaringan internal.
        * 10 unit server dibutuhkan di Gedung A, dengan fungsi yang berbeda-beda, seperti:
           - DHCP Server
           - DNS Server
           - File Server
           - Database Server
           - Mail Server
           - Web Server
           - Monitoring Server
           - Backup Server
           - Authentication Server
           - Virtualization Server (jika menggunakan VM)
        
    **Segmentasi VLAN, Routing, dan Pengalamatan IP**

    Untuk memastikan keamanan, efisiensi manajemen traffic, dan kemudahan pengelolaan jaringan, setiap departemen di Kantor Pusat (Gedung A) dan Kantor Cabang (Gedung B) akan ditempatkan dalam Virtual LAN (VLAN) yang terpisah. VLAN ini memungkinkan isolasi lalu lintas jaringan antar departemen sekaligus meminimalkan risiko akses yang tidak sah.

    Setiap VLAN akan diberi subnet IP yang unik sesuai jumlah perangkat di masing-masing departemen dengan ruang cadangan untuk ekspansi. Untuk mendukung alokasi alamat IP secara otomatis, akan diterapkan layanan DHCP, baik secara terpusat dengan penggunaan DHCP relay agent di setiap VLAN, atau terdistribusi per lokasi tergantung desain jaringan. Agar setiap VLAN dapat saling berkomunikasi secara terbatas dan sesuai kebijakan, serta terhubung ke layanan pusat seperti server farm atau akses internet, digunakan routing antar VLAN (inter-VLAN routing). Hal ini dilakukan melalui Layer 3 switch atau router yang mendukung VLAN-aware routing.

    Berikut contoh skema segmentasi VLAN dan subnet IP:

    | Departemen  | Gedung  | Jumlah Perangkat |VLAN ID |  Subnet IP        |
    | :---------- | :------:| ----------------:| ------:| -----------------:|
    |  IT         |   A     |         40       |  10    |  192.168.10.0/26  |
    |  Keuangan   |   A     |         25       |  20    |  192.168.20.0/26  | 
    |  SDM        |   A     |         20       |  30    |  192.168.30/27    |  
    | Server Farm |   A     |         10       |  40    |  192.168.40.0/28  |
    | Marketing   |   B     |         30       |  50    |  192.168.50.0/26  |
    | Operasional |   B     |         35       |  60    |  192.168.60/26    |


    **Keamanan Jaringan, Akses Internet, dan Layanan DNS**

    1. Access Control List (ACL):
        ACL diterapkan pada perangkat Layer 3 seperti switch atau router untuk mengatur dan membatasi komunikasi antar VLAN sesuai kebijakan keamanan. Sebagai contoh, hanya VLAN IT yang diizinkan mengakses server farm, sementara akses ke VLAN Keuangan dibatasi agar tidak dapat diakses oleh departemen lain, sehingga data sensitif tetap terlindungi. Dengan begitu, lalu lintas internal jaringan dapat dikelola secara lebih aman dan efisien.

    2. Firewall:
        Firewall ditempatkan di perbatasan jaringan (edge) untuk melakukan filtering trafik secara lebih mendalam. Firewall ini mampu menyaring data berdasarkan alamat IP, port, dan protokol tertentu, serta mendeteksi lalu lintas yang mencurigakan dari luar jaringan. Penggunaan firewall ini merupakan lapisan tambahan keamanan yang melengkapi fungsi ACL di dalam jaringan internal.

    3. Network Address Translation (NAT):
        NAT digunakan agar seluruh perangkat dalam jaringan internal yang menggunakan alamat IP privat dapat mengakses internet melalui satu atau beberapa public IP dari ISP. Proses NAT ini dilakukan pada perangkat gateway, seperti router atau firewall, sehingga penggunaan IP publik menjadi lebih efisien dan alamat IP internal tetap tersembunyi dari jaringan luar.

    4. Domain Name System (DNS):
        Layanan DNS internal digunakan untuk mempermudah komunikasi antar perangkat dalam jaringan lokal dengan menggunakan nama host, bukan alamat IP. Untuk mengakses layanan di luar jaringan, DNS internal akan meneruskan permintaan ke server DNS eksternal seperti milik Google (8.8.8.8), Cloudflare (1.1.1.1), atau DNS dari ISP. Dengan mekanisme ini, proses resolusi nama menjadi lebih cepat dan terintegrasi.

    **Timeline rencana kerja untuk 7 pekan:**

    | Pekan     | Waktu Pengumpulan   | Deliverable                          |Peran Anggota                                      |
    | :---------| :--------------:    | ------------------------------------:| ----------------------------------------------------:|
    | **9**     | Minggu 13 April 2025|Dokumen perencanaan proyek            | Riqqah Khalda Karina 10231082 - Network Architect    |  
    | **10**    | Jumaat 25 April 2025|Desain Topologi & Skema Pengalamatan  | Riqqah Khalda Karina 10231082 - Network Architect    |   
    | **11**    | Jumaat 2 Mei 2025   |Implementasi Topologi Dasar & VLAN    | Muhammad Ayash Az dzikri 10231060 - Network Engineer |   
    | **12**    | Jumaat 9 Mei 2025   |Implementasi Routing & WAN            | Muhammad Ayash Az dzikri 10231060 - Network Engineer |
    | **13**    | Jumaat 16 Mei 2025  |Implementasi Layanan Jaringan         | Verina Rahma Dina 10231090 - Network Services        |
    | **14**    | Jumaat 23 Mei 2025  |Implementasi Keamanan & Pengujian     | Cintya Widhi Astuti 10231026 - Security & Documentation Specialist |
    | **15**    | Jumaat 30 Mei 2025  |Finalisasi Dokumentasi & Presentasi   | Cintya Widhi Astuti 10231026 - Security & Documentation Specialist |
 
    **Sketsa awal desain jaringan**

    <img src = GedungA.jpeg >

    Gedung A memiliki struktur jaringan yang lebih kompleks karena mencakup lebih banyak departemen dan dilengkapi Server Farm.
    Detail strukturnya:
    
    - **Departemen IT**

        Komputer di Departemen IT terhubung ke dua switch yang masing-masing tersambung ke Main Router. Ini menunjukkan adanya kemungkinan penggunaan load balancing atau redundansi untuk meningkatkan ketersediaan jaringan. Departemen IT biasanya memiliki hak akses yang lebih luas, termasuk akses ke server farm.

    - **Departemen Keuangan**

         Departemen Keuangan memiliki komputer yang tersambung ke switch khusus lalu menuju router utama. VLAN digunakan untuk membatasi akses hanya pada perangkat yang berwenang, sehingga melindungi informasi keuangan yang sensitif.

    - **Departemen SDM**

        Komputer di Departemen SDM dihubungkan ke switch tersendiri yang selanjutnya menuju Main Router. Sama seperti departemen lain, VLAN diterapkan untuk memberikan segmentasi logis demi keamanan dan efisiensi lalu lintas jaringan.

    - **Server Farm**

        Server farm terdiri dari beberapa server yang terhubung melalui switch lalu ke router utama. Server-server ini menyediakan berbagai layanan seperti DHCP, DNS internal, file sharing, dan aplikasi internal lainnya. Akses ke server farm biasanya dibatasi melalui pengaturan ACL agar hanya departemen tertentu yang dapat mengaksesnya, seperti IT.

    <img src = GedungB.jpeg >

    Diagram ini memperlihatkan struktur jaringan di Gedung B yang terdiri dari dua departemen utama: Departemen SDM dan Departemen Keuangan. Masing-masing departemen memiliki perangkat jaringan tersendiri, namun tetap terhubung melalui satu perangkat Main Router.
    Detail Strukturnya:

    - **Departemen SDM** 
        Komputer pada Departemen SDM terhubung ke sebuah switch yang kemudian disambungkan ke Main Router Gedung B. Penggunaan switch ini menunjukkan bahwa jaringan telah dipisahkan dalam VLAN tersendiri untuk keperluan isolasi lalu lintas data antar departemen.

    - **Departemen Keuangan**

        Komputer Departemen Keuangan juga terhubung ke switch tersendiri yang disambungkan ke Main Router. Pemisahan ini bertujuan untuk memberikan keamanan jaringan serta mempermudah manajemen akses antar departemen.

   -  **Penjelasan Router dan Switch pada Gedung A dan B**

        Router yang digunakan di Gedung A dan Gedung B atau Main Router berfungsi sebagai penghubung utama antar VLAN, antar gedung melalui jalur WAN, dan sebagai gateway menuju internet. Kedua router ini juga dapat mengatur routing dinamis menggunakan protokol seperti OSPF agar pertukaran informasi rute antar jaringan VLAN dari berbagai departemen bisa berlangsung otomatis dan efisien. Selain itu, router ini menangani implementasi NAT (Network Address Translation) agar perangkat internal dapat mengakses internet dengan satu alamat publik.

        Switch yang digunakan dalam jaringan ini terdiri dari dua jenis, yaitu switch Layer 2 dan switch Layer 3. Switch Layer 2 berfungsi untuk menghubungkan perangkat-perangkat dalam satu VLAN, bekerja pada Data Link Layer, dan melakukan switching berdasarkan alamat MAC. Jenis switch ini biasanya digunakan di tingkat departemen, seperti untuk koneksi antar komputer di Departemen SDM atau Keuangan.

        Sementara itu, switch Layer 3 memiliki kemampuan routing antar VLAN karena bekerja sampai di Network Layer. Switch ini bisa menggantikan peran router dalam melakukan inter-VLAN routing, sehingga mempercepat proses komunikasi antar departemen dalam gedung yang sama tanpa harus melewati router terlebih dahulu. Switch Layer 3 biasanya digunakan di area pusat jaringan atau bisa disebut sebagai Main Switch, seperti di Gedung A yang memiliki server farm dan banyak VLAN.
