## Tugas Kelompok 4 [Pekan 11]

**Anggota Kelompok dan Peran:**
- Muhammad Ayash Az dzikri 10231060 - Network Engineer
- Cintya Widhi Astuti 10231026 - Security & Documentation Specialist 
- Riqqah Khalda Karina 10231082 - Network Architect
- Verina Rahma Dinah 10231090 - Network Services Specialist

#### **Tugas Kelompok:** 

Pembangunan topologi dasar di Cisco Packet Tracer/GNS3. 
Konfigurasi VLAN dan trunking. 
Implementasi routing antar-VLAN. 

#### **Deliverable (Format Markdown):** 

Laporan Implementasi Tahap 1
Link file simulasi (.pkt atau sejenisnya) yang dapat diunduh. 
Screenshot topologi yang telah diimplementasikan dengan penjelasan detail.
WAJIB: Dokumentasi konfigurasi CLI lengkap untuk semua switch dan router, mencakup: 

```markdown 
### Switch Configuration 
```bash 
# Konfigurasi VLAN pada Switch1 
Switch> enable 
Switch# configure terminal 
Switch(config)# vlan 10 
Switch(config-vlan)# name IT_DEPARTMENT 
... 
``` 
Hasil pengujian konektivitas antar-VLAN dengan screenshot dan penjelasan.
Kendala yang dihadapi dan solusinya.

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

#### Topologi 

<img src = topologi11.jpg >

### Gedung A

#### 1. Konfigurasi Switch Departemen IT 1

**Vlan Switch Departemen IT 1**
```
Switch>en
Switch#conf t
Switch(config)#vlan 10
Switch(config-vlan)#name VLAN_IT
Switch(config-vlan)#interface range fa0/1 - 20
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
Switch(config-if-range)#spanning-tree portfast
```
**Dokumentasi Vlan Departemen IT 1**

<img src = IT1.jpg >

<img src = hasilIT1.jpg >

**Penjelasan Vlan Departemen IT 1**

Konfigurasi VLAN yang diberikan bertujuan untuk mengelompokkan perangkat-perangkat yang digunakan oleh Departemen IT ke dalam satu jaringan virtual yang terpisah, yaitu VLAN 10. Langkah pertama adalah masuk ke mode konfigurasi switch, lalu membuat VLAN 10 dan memberinya nama VLAN_IT agar mudah dikenali sebagai jaringan khusus departemen IT. Setelah itu, port FastEthernet dari 0/1 hingga 0/20 dikonfigurasi dalam mode akses (access mode), yang berarti setiap port tersebut hanya akan terhubung ke satu VLAN. Semua port dalam rentang ini kemudian diasosiasikan ke VLAN 10, sehingga perangkat yang terhubung ke port tersebut berada dalam satu segmen jaringan yang sama. Selain itu, diaktifkan juga fitur spanning-tree portfast yang memungkinkan port langsung aktif (forwarding) tanpa menunggu proses konvergensi Spanning Tree Protocol, sehingga perangkat dapat segera terkoneksi ke jaringan begitu dinyalakan. Konfigurasi ini bermanfaat untuk meningkatkan keamanan, efisiensi, dan kecepatan konektivitas perangkat di lingkungan kerja Departemen IT, serta memudahkan manajemen jaringan melalui pengelompokan berdasarkan fungsi atau unit kerja.

#### 2. Konfigurasi Switch Departemen IT 2

**Vlan Switch Departemen IT 2**

```
Switch>en
Switch#conf t
Switch(config)#vlan 10
Switch(config-vlan)#name VLAN_IT
Switch(config-vlan)#interface range fa0/1 - 20
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen IT 2**

<img src = IT2.jpg >

<img src = hasilIT2.jpg >

**Penjelasan Vlan Departemen IT 2**

Konfigurasi di atas untuk membuat dan mengatur VLAN 10 pada sebuah switch, yang ditujukan untuk mengelompokkan perangkat-perangkat dalam Departemen IT ke dalam satu jaringan virtual. Proses dimulai dengan masuk ke mode konfigurasi (conf t), kemudian membuat VLAN 10 dan memberikan nama VLAN_IT sebagai identitas jaringan tersebut. Selanjutnya, port FastEthernet dari fa0/1 hingga fa0/20 dipilih untuk dikonfigurasi secara bersamaan sebagai port akses (switchport mode access), yang hanya dapat terhubung ke satu VLAN. Semua port ini dihubungkan ke VLAN 10 dengan perintah switchport access vlan 10, sehingga seluruh perangkat yang tersambung ke port-port tersebut berada dalam jaringan yang sama dan terisolasi dari VLAN lain. Terakhir, spanning-tree portfast diaktifkan pada port-port tersebut agar perangkat dapat langsung aktif tanpa menunggu waktu konvergensi dari Spanning Tree Protocol, yang sangat berguna untuk perangkat end-user seperti komputer atau printer. Secara keseluruhan, konfigurasi ini meningkatkan efisiensi, keamanan, dan kecepatan koneksi dalam jaringan internal Departemen IT.

#### 3. Konfigurasi Switch Departemen Keuangan 1

**Vlan Departemen Keuangan 1**

```
Switch>en
Switch#conf t
Switch(config)#vlan 20
Switch(config-vlan)#name VLAN_Keuangan
Switch(config-vlan)#interface range fa0/1 - 14
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Keuangan 1**

<img src = Keuangan1.jpg >

<img src = hasilKeuangan.jpg >

**Penjelasan Vlan Keuangan 1**

Konfigurasi di atas digunakan untuk membuat dan mengatur VLAN 20 pada sebuah switch, yang diperuntukkan bagi perangkat-perangkat di Departemen Keuangan. Pertama, pengguna masuk ke mode konfigurasi switch, kemudian membuat VLAN dengan ID 20 dan memberikan nama VLAN_Keuangan agar mudah dikenali dan dikelola sesuai fungsi departemen. Setelah itu, port FastEthernet dari fa0/1 hingga fa0/14 dipilih secara serentak untuk dikonfigurasi sebagai port akses (switchport mode access), artinya port tersebut hanya akan terhubung ke satu VLAN saja. Semua port ini lalu dihubungkan ke VLAN 20 dengan perintah switchport access vlan 20, sehingga seluruh perangkat yang terhubung ke port-port tersebut akan berada dalam satu jaringan virtual yang sama, yaitu VLAN_Keuangan. Terakhir, diaktifkan fitur spanning-tree portfast, yang mempercepat proses aktivasi port dengan melewati beberapa tahap Spanning Tree Protocol, sehingga perangkat seperti komputer atau printer yang digunakan oleh staf keuangan bisa langsung terkoneksi ke jaringan saat dinyalakan. Dengan konfigurasi ini, jaringan untuk Departemen Keuangan menjadi lebih terstruktur, aman, dan efisien, serta memudahkan pengelolaan dan pemisahan trafik jaringan antar departemen.

#### 4. Konfigurasi Switch Departemen Keuangan 2

**Vlan Departemen Keuangan 2**
```
Switch>en
Switch#conf t
Switch(config)#vlan 20
Switch(config-vlan)#name VLAN_Keuangan
Switch(config-vlan)#interface range fa0/1 - 12
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Keuangan 2**

<img src = Keuangan2.jpg >

<img src = hasilKeuangan2.jpg >

**Penjelasan Vlan Keuangan 2**

Konfigurasi di atas digunakan untuk membuat dan mengatur VLAN 20 pada switch yang ditujukan khusus untuk Departemen Keuangan. Pertama, mengaktifkan mode konfigurasi (conf t) dan kemudian membuat VLAN dengan ID 20 serta memberikan nama VLAN_Keuangan untuk menandai bahwa VLAN ini digunakan oleh bagian keuangan. Selanjutnya, port FastEthernet dari fa0/1 hingga fa0/12 dipilih secara bersamaan untuk dikonfigurasi. Port-port ini diatur sebagai access port melalui perintah switchport mode access, yang berarti hanya akan terkoneksi ke satu VLAN, dalam hal ini VLAN 20. Dengan perintah switchport access vlan 20, seluruh perangkat yang terhubung ke port-port tersebut akan tergabung dalam jaringan VLAN_Keuangan. Terakhir, perintah spanning-tree portfast digunakan agar port langsung aktif dan bisa digunakan oleh perangkat end-user seperti komputer atau printer tanpa harus menunggu proses konvergensi dari protokol Spanning Tree. Konfigurasi ini membantu menciptakan jaringan yang terpisah, aman, dan stabil untuk Departemen Keuangan, memudahkan manajemen jaringan, serta mempercepat proses koneksi perangkat ke jaringan.

#### 5. Konfigurasi Switch Departemen Sumber Daya Manusia

**Vlan Departemen Sumber Daya Manusia**

```
Switch>en
Switch#conf t
Switch(config)#vlan 30
Switch(config-vlan)#name VLAN_SDM
Switch(config-vlan)#interface range fa0/1 - 20
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 30
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Sumber Daya Manusia**

<img src = sdm.jpg >

<img src = hasilSDM.jpg >

**Penjelasan Vlan Sumber Daya Manusia**

Konfigurasi di atas bertujuan untuk membuat dan mengatur VLAN 30 pada sebuah switch, yang diperuntukkan bagi perangkat-perangkat di Departemen Sumber Daya Manusia (SDM). Proses dimulai dengan masuk ke mode konfigurasi (conf t), lalu membuat VLAN dengan ID 30 dan memberinya nama VLAN_SDM sebagai penanda bahwa jaringan ini khusus digunakan oleh bagian SDM. Selanjutnya, port FastEthernet dari fa0/1 hingga fa0/20 dipilih untuk dikonfigurasi secara bersamaan sebagai port akses menggunakan perintah switchport mode access, sehingga setiap port hanya akan terhubung ke satu VLAN. Kemudian, semua port tersebut dihubungkan ke VLAN 30 melalui perintah switchport access vlan 30, yang berarti perangkat seperti komputer atau printer di Departemen SDM akan berada dalam satu jaringan virtual yang sama. Terakhir, fitur spanning-tree portfast diaktifkan untuk mempercepat proses aktivasi port, sehingga perangkat dapat langsung terkoneksi ke jaringan saat dinyalakan tanpa menunggu proses dari Spanning Tree Protocol. Secara keseluruhan, konfigurasi ini menciptakan jaringan yang terisolasi, aman, dan efisien untuk Departemen SDM, memudahkan pengelolaan, serta meningkatkan kecepatan dan kestabilan koneksi perangkat.

#### 6. Konfigurasi Switch Departemen Server

**Vlan Departemen Server**

```
Switch>en
Switch#conf t
Switch(config)#vlan 30
Switch(config-vlan)#name VLAN_SDM
Switch(config-vlan)#interface range fa0/1 - 20
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 30
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Server**

<img src = server.jpg >

<img src = hasilServer.jpg >

**Penjelasan Vlan Server**

Konfigurasi di atas digunakan untuk membuat dan mengatur VLAN 40 pada sebuah switch yang dikhususkan untuk jaringan server. Langkah pertama adalah masuk ke mode konfigurasi (conf t), kemudian membuat VLAN dengan ID 40 dan memberikan nama VLAN_Server agar VLAN ini mudah dikenali sebagai jaringan untuk perangkat server. Selanjutnya, dipilih port FastEthernet dari fa0/1 hingga fa0/10, yang akan dikonfigurasi secara bersamaan sebagai port akses menggunakan perintah switchport mode access. Hal ini memastikan bahwa setiap port hanya terhubung ke satu VLAN. Dengan perintah switchport access vlan 40, seluruh port tersebut dimasukkan ke dalam VLAN 40, sehingga semua server yang terhubung akan berada dalam jaringan yang sama dan terisolasi dari VLAN lain. Terakhir, spanning-tree portfast diaktifkan agar port dapat langsung aktif saat perangkat dihidupkan, tanpa menunggu proses konvergensi dari protokol Spanning Tree. Konfigurasi ini sangat berguna untuk membangun jaringan server yang stabil, cepat, dan aman, serta memudahkan manajemen jaringan dengan memisahkan trafik server dari trafik pengguna lainnya.

#### 7. Main Switch Gedung A

**Vlan Main Switch Fedung A**

```
Switch>en
Switch#conf t
Switch(config)#vlan 10
Switch(config-vlan)# name VLAN_IT
Switch(config-vlan)#vlan 20
Switch(config-vlan)# name VLAN_Keuangan
Switch(config-vlan)#vlan 30
Switch(config-vlan)# name VLAN_SDM
Switch(config-vlan)#vlan 40
Switch(config-vlan)# name VLAN_Server
Switch(config)#interface range Fa0/1 - 6
Switch(config-if-range)#switchport trunk encapsulation dot1q
Switch(config-if-range)#switchport mode trunk

Switch(config)#vlan 10
Switch(config-vlan)#name VLAN_IT
Switch(config)#interface vlan 10
Switch(config-if)#ip address 192.168.10.1 255.255.255.192
Switch(config-if)#no shutdown

Switch(config-if)#ex
Switch(config)#vlan 20
Switch(config-vlan)#name VLAN_Keuangan
Switch(config)#interface vlan 20
Switch(config-if)#ip address 192.168.20.1 255.255.255.192
Switch(config-if)#no shutdown

Switch(config-if)#ex
Switch(config)#vlan 30
Switch(config-vlan)#name VLAN_SDM
Switch(config)#interface vlan 30
Switch(config-if)#ip address 192.168.30.1 255.255.255.224
Switch(config-if)#no shutdown

Switch(config-if)#ex
Switch(config)#vlan 40
Switch(config-vlan)#name VLAN_Server
Switch(config)#interface vlan 40
Switch(config-if)#ip address 192.168.40.1 255.255.255.240
Switch(config-if)#no shutdown

Switch(config-if)#ex
Switch(config)#ip routing
Switch(config)#ex

```

**Dokumentasi Vlan Main Switch Gedung A**

<img src = MainA1.jpg >
<img src = MainA2.jpg >

<img src = hasilMainA.jpg >

**Penjelasan Vlan Main Switch Gedung A**

Konfigurasi di atas merupakan implementasi inter-VLAN routing pada switch layer 3, yang memungkinkan perangkat di berbagai VLAN (jaringan virtual) untuk saling berkomunikasi satu sama lain melalui IP routing. Langkah awal dilakukan dengan membuat empat VLAN: VLAN_IT (ID 10), VLAN_Keuangan (ID 20), VLAN_SDM (ID 30), dan VLAN_Server (ID 40). Masing-masing VLAN diidentifikasi dengan nama khusus yang mencerminkan fungsinya dalam organisasi.

Selanjutnya, port FastEthernet dari fa0/1 hingga fa0/6 dikonfigurasi sebagai trunk port menggunakan perintah switchport trunk encapsulation dot1q dan switchport mode trunk, yang memungkinkan port tersebut membawa trafik dari beberapa VLAN secara bersamaan—umumnya digunakan untuk koneksi antar switch atau ke router.

Kemudian, untuk setiap VLAN yang telah dibuat, ditetapkan satu interface virtual atau SVI (Switch Virtual Interface) dengan alamat IP masing-masing:

* VLAN 10: 192.168.10.1/26

* VLAN 20: 192.168.20.1/26

* VLAN 30: 192.168.30.1/27

* VLAN 40: 192.168.40.1/28

Setiap SVI diaktifkan dengan perintah no shutdown, agar interface virtual bisa digunakan sebagai default gateway oleh perangkat di dalam VLAN tersebut. Terakhir, perintah ip routing diaktifkan untuk mengaktifkan fitur routing antar VLAN pada switch layer 3, sehingga lalu lintas data dari satu VLAN bisa diarahkan ke VLAN lain sesuai kebutuhan.

Konfigurasi ini sangat penting dalam jaringan perusahaan yang ingin memisahkan lalu lintas jaringan berdasarkan departemen namun tetap membutuhkan komunikasi antar departemen, contohnya antara server dan klien atau antar unit kerja seperti IT, Keuangan, dan SDM. Hasilnya adalah jaringan yang tersegmentasi dengan baik, lebih aman, dan fleksibel, namun tetap terhubung secara logis melalui routing IP.

#### 8. Konfigurasi Main Switch Trunk ke Router Gedung A

**Vlan Main Switch Trunk ke Router Gedung A**

```
Switch#conf t
Switch(config)#interface fa0/7
Switch(config-if)#description trunk_to_Router2
Switch(config-if)#switchport trunk encapsulation dot1q
Switch(config-if)#switchport mode trunk
Switch(config-if)#ex
```

**Dokumentasi Vlan Main Switch Trunk ke Router Gedung A**

<img src = TrunkA.jpg >

**Penjelasan Vlan Main Switch Trunk ke Router Gedung A**

Konfigurasi di atas digunakan untuk mengatur koneksi trunk dari Main Switch ke Router di Gedung A (Router2), yang memungkinkan lalu lintas dari berbagai VLAN diteruskan melalui satu jalur fisik ke router untuk keperluan inter-VLAN routing atau akses jaringan lebih luas.

Berikut penjelasan setiap langkahnya:

* interface fa0/7: Memilih port FastEthernet 0/7 pada switch, yang akan digunakan sebagai jalur koneksi ke Router2.

* description trunk_to_Router2: Menambahkan deskripsi pada port untuk mempermudah identifikasi bahwa port ini terhubung ke router di Gedung A.

* switchport trunk encapsulation dot1q: Menetapkan metode enkapsulasi trunk menggunakan IEEE 802.1Q, standar umum yang digunakan untuk membawa trafik VLAN melalui trunk.

* switchport mode trunk: Mengatur mode port menjadi trunk, yang berarti port ini bisa membawa trafik dari banyak VLAN sekaligus.

* ex: Keluar dari mode konfigurasi interface.

Dengan konfigurasi ini, port fa0/7 akan membawa trafik dari semua VLAN yang telah dibuat di switch, dan mengirimkannya ke Router2 yang kemungkinan besar bertugas melakukan routing antar VLAN (Router-on-a-Stick) atau sebagai penghubung jaringan antar gedung. Konfigurasi ini sangat penting dalam arsitektur jaringan skala besar seperti kampus atau gedung perkantoran, untuk memastikan komunikasi antar VLAN tetap berjalan melalui router pusat.

#### 9. Konfigurasi Router Gedung A

**Vlan Router Gedung A**

```
Router#conf t
Router(config)#interface gig0/0
Router(config-if)#description to_Multilayer_Switch0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.10.10.1 255.255.255.252
Router(config-if)#ex
Router(config)#ex
```

**Dokumentasi Vlan Router Gedung A**

<img src = RA.jpg >

**Penjelasan Vlan Router Gedung A**

Konfigurasi di atas digunakan untuk mengaktifkan dan menetapkan alamat IP pada interface GigabitEthernet 0/0 di sebuah router yang terhubung ke Multilayer Switch0, biasanya sebagai bagian dari koneksi antar perangkat jaringan inti.

Berikut penjelasan dari setiap perintah:

* interface gig0/0: Memilih interface GigabitEthernet 0/0 di router.

* description to_Multilayer_Switch0: Memberikan deskripsi pada interface untuk identifikasi bahwa interface ini terhubung ke Multilayer Switch0.

* no shutdown: Mengaktifkan interface yang sebelumnya mungkin dalam kondisi mati (shutdown).

* ip address 10.10.10.1 255.255.255.252: Mengatur alamat IP dan subnet mask untuk interface tersebut. Alamat IP 10.10.10.1 dengan subnet mask 255.255.255.252 (prefix /30) memungkinkan dua perangkat saling terkoneksi langsung, ideal untuk point-to-point link antara router dan switch layer 3.

* ex: Keluar dari konfigurasi interface.

Tujuan utama dari konfigurasi ini adalah membuat jalur komunikasi langsung antara router dan multilayer switch, misalnya untuk interkoneksi antar gedung, antar jaringan VLAN, atau ke jaringan luar (WAN). Dengan subnet /30, hanya dua IP yang bisa digunakan, sehingga sangat efisien untuk koneksi langsung antar perangkat.

### Gedung B

#### 1. Konfigurasi Switch Departemen Marketing 1

**Vlan Departemen Marketing 1**

```
Konfigurasi Departemen Marketing 1
Switch>en
Switch#conf t
Switch(config)#vlan 50
Switch(config-vlan)#name VLAN_Marketing
Switch(config-vlan)#interface range fa0/1 - 15
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 50
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Marketing 1**

<img src = Marketing1.jpg >

<img src = hasilMarketing.jpg >

**Penjelasan Vlan Marketing 1**

Konfigurasi VLAN ini bertujuan untuk mengelompokkan seluruh perangkat milik Departemen Marketing ke dalam satu jaringan virtual yang terpisah, yaitu VLAN 50. Proses dimulai dengan masuk ke mode konfigurasi pada switch, kemudian membuat VLAN 50 dan memberinya nama VLAN_Marketing agar mudah diidentifikasi sebagai jaringan khusus untuk departemen tersebut. Selanjutnya, port FastEthernet dari 0/1 hingga 0/15 dikonfigurasi dalam mode akses (access mode), yang berarti masing-masing port hanya akan berfungsi dalam satu VLAN tertentu dan tidak bisa berpindah-pindah antar VLAN. Setelah mode akses diatur, semua port tersebut dihubungkan langsung ke VLAN 50, sehingga setiap perangkat yang terhubung ke salah satu port itu akan berada dalam satu jaringan lokal yang sama. Untuk mempercepat konektivitas saat perangkat dinyalakan, fitur spanning-tree portfast diaktifkan pada port-port tersebut. Fitur ini memungkinkan port langsung aktif tanpa harus menunggu proses konvergensi dari protokol Spanning Tree, sehingga sangat cocok untuk perangkat end-user seperti komputer. Dengan konfigurasi ini, jaringan Departemen Marketing menjadi lebih aman, tertata, dan mudah dikelola karena pemisahan fungsi jaringan berdasarkan unit kerja yang jelas.

#### 2. Konfigurasi Switch Departemen Marketing 2

**Vlan Departemen Marketing 2**

```
Switch>en
Switch#conf t
Switch(config)#vlan 50
Switch(config-vlan)#name VLAN_Marketing
Switch(config-vlan)#interface range fa0/1 - 15
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 50
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Marketing 2**

<img src = Marketing2.jpg >

<img src = hasilMarketing2.jpg >

**Penjelasan Vlan Marketing 2**

Konfigurasi VLAN yang dilakukan ditujukan untuk mengelompokkan perangkat-perangkat yang digunakan oleh Departemen Marketing 1 ke dalam satu jaringan virtual tersendiri, yaitu VLAN 50. Proses dimulai dengan masuk ke mode konfigurasi pada switch, kemudian dibuat VLAN 50 dan diberi nama *VLAN_Marketing* agar lebih mudah diidentifikasi sebagai jaringan khusus untuk departemen tersebut. Selanjutnya, port FastEthernet dari 0/1 hingga 0/15 dikonfigurasikan dalam mode akses, yang berarti setiap port hanya akan terhubung ke satu VLAN dan tidak akan menerima lalu lintas dari VLAN lain. Semua port tersebut kemudian dimasukkan ke dalam VLAN 50, sehingga perangkat yang terhubung ke port-port ini akan berada dalam satu segmen jaringan yang sama. Fitur *spanning-tree portfast* juga diaktifkan, yang berguna untuk mempercepat proses koneksi perangkat ke jaringan dengan melewati tahapan konvergensi dari protokol Spanning Tree. Dengan konfigurasi ini, konektivitas antar perangkat di lingkungan kerja Departemen Marketing 1 menjadi lebih cepat, aman, dan efisien, serta memudahkan pengelolaan jaringan berdasarkan fungsi organisasi.

#### 3. Konfigurasi Switch Departemen Operasional 1

**Vlan Departemen Operasional 1**

```
Switch>en
Switch#conf t
Switch(config)#vlan 60
Switch(config-vlan)#name VLAN_Ops
Switch(config-vlan)#interface range fa0/1 - 17
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 60
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Operasional 1**

<img src = Operasional1.jpg >

<img src = hasilOperasional.jpg >

**Penjelasan Vlan Operasional 1**

Konfigurasi VLAN yang diberikan bertujuan untuk mengelompokkan perangkat-perangkat yang digunakan oleh Departemen Operasional ke dalam satu jaringan virtual yang terpisah, yaitu VLAN 60. Langkah pertama adalah masuk ke mode konfigurasi pada switch, kemudian membuat VLAN 60 dan memberinya nama VLAN_Ops agar mudah dikenali sebagai jaringan khusus untuk Departemen Operasional. Setelah itu, port FastEthernet dari 0/1 hingga 0/17 dikonfigurasi dalam mode akses (access mode), artinya setiap port tersebut hanya akan berkomunikasi dengan satu VLAN tertentu. Seluruh port dalam rentang ini kemudian diasosiasikan ke VLAN 60, sehingga perangkat yang terhubung ke port tersebut berada dalam satu segmen jaringan yang sama. Untuk mempercepat proses konektivitas, diaktifkan juga fitur spanning-tree portfast yang memungkinkan port langsung aktif tanpa harus menunggu proses konvergensi Spanning Tree Protocol. Konfigurasi ini membantu meningkatkan efisiensi dan kecepatan jaringan, serta mempermudah pengelolaan infrastruktur jaringan berdasarkan unit kerja, dalam hal ini Departemen Operasional.

#### 3. KOnfigurasi Switch Departemen Operasional 2

**Vlan Departemen Operasional 2**

```
Switch>en
Switch#conf t
Switch(config)#vlan 60
Switch(config-vlan)#name VLAN_Ops
Switch(config-vlan)#interface range fa0/1 - 18
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 60
Switch(config-if-range)#spanning-tree portfast
```

**Dokumentasi Vlan Departemen Operasional 2**

<img src = Operasional2.jpg >

<img src = hasilOperasional2.jpg >

**Penjelasan Vlan Operasional 2**

Konfigurasi VLAN untuk Departemen Operasional 2 bertujuan untuk mengelompokkan perangkat-perangkat yang digunakan oleh departemen tersebut ke dalam jaringan virtual tersendiri, yaitu VLAN 60. Proses dimulai dengan masuk ke mode konfigurasi pada switch, kemudian dibuat VLAN 60 dan diberi nama VLAN_Ops untuk memudahkan identifikasi bahwa ini adalah jaringan khusus bagi Departemen Operasional. Selanjutnya, port FastEthernet dari 0/1 hingga 0/18 dikonfigurasi dalam mode akses (access mode), yang artinya masing-masing port hanya akan terhubung ke satu VLAN, dalam hal ini VLAN 60. Dengan pengaturan ini, semua perangkat yang terhubung ke port-port tersebut akan berada di dalam satu jaringan lokal yang sama, sehingga komunikasi antar perangkat menjadi lebih efisien dan aman. Sebagai tambahan, diaktifkan juga fitur spanning-tree portfast, yang berfungsi untuk mempercepat proses aktivasi port ketika perangkat dihubungkan. Dengan portfast, port akan langsung berada dalam status forwarding tanpa melalui fase-fase Spanning Tree Protocol yang biasa, sehingga perangkat dapat langsung terkoneksi ke jaringan tanpa delay. Konfigurasi ini tidak hanya mempermudah manajemen jaringan berdasarkan unit kerja, tetapi juga meningkatkan kecepatan koneksi dan kestabilan jaringan di lingkungan operasional Departemen Operasional 2.

#### 4. Konfigurasi Main Switch Gedung B

**Vlan Main Switch Gedung B**

```
Switch>en
Switch#conf t
Switch(config)#vlan 50
Switch(config-vlan)# name VLAN_Marketing
Switch(config-vlan)#vlan 60
Switch(config-vlan)# name VLAN_Ops
Switch(config-vlan)#ex
Switch(config)#interface range fa0/1 - 4
Switch(config-if-range)#switchport trunk encapsulation dot1q
Switch(config-if-range)#switchport mode trunk

Switch(config)#interface vlan 50
Switch(config-if)#ip address 192.168.50.1 255.255.255.192
Switch(config-if)#no shutdown
Switch(config)#interface vlan 60
Switch(config-if)#ip address 192.168.60.1 255.255.255.192
Switch(config-if)#no shutdown

Switch(config-if)#ex
Switch(config)#ip routing
Switch(config)#ex

```

**Dokumentasi Vlan Main Switch Gedung B**

<img src = MainB1.jpg >
<img src = MainB2.jpg >

<img src = hasilMainB.jpg >

**Penjelasan Vlaan Main Switch Gedung B**

Konfigurasi pada Main Switch Gedung B ini bertujuan untuk mengelola lalu lintas jaringan antar VLAN dan menyediakan konektivitas antar departemen dalam satu gedung. Pertama, dibuat dua VLAN, yaitu VLAN 50 dengan nama VLAN_Marketing dan VLAN 60 dengan nama VLAN_Ops, yang masing-masing ditujukan untuk Departemen Marketing dan Operasional. Setelah VLAN dibuat, port FastEthernet 0/1 hingga 0/4 dikonfigurasi dalam mode trunk dengan menggunakan enkapsulasi dot1q, yang memungkinkan port tersebut membawa lalu lintas dari berbagai VLAN secara bersamaan, sangat penting untuk konektivitas antar switch atau perangkat layer 3. Selanjutnya, interface VLAN 50 dan VLAN 60 dikonfigurasi dengan alamat IP 192.168.50.1/26 dan 192.168.60.1/26 secara berurutan, dan diaktifkan menggunakan perintah no shutdown. Pengaturan ini memungkinkan switch bertindak sebagai default gateway bagi perangkat-perangkat di masing-masing VLAN. Terakhir, fitur ip routing diaktifkan agar switch dapat melakukan inter-VLAN routing, yaitu mengarahkan lalu lintas antar VLAN secara langsung. Konfigurasi ini mendukung segmentasi jaringan berdasarkan fungsi departemen sekaligus menyediakan konektivitas lintas VLAN di Gedung B dengan efisien dan terstruktur.

#### 5. Konfigurasi Main Switch Trunk Gedung B

**Vlan Main Switch Trunk Gedung B**

```
Switch#conf t
Switch(config)#interface fa0/5
Switch(config-if)#description trunk_to_Router0
Switch(config-if)#switchport trunk encapsulation dot1q
Switch(config-if)#switchport mode trunk
Switch(config-if)#ex
Switch(config)#ex

```

**Dokumentasi Vlan Main Switch Trunk Gedung B**

<img src = TrunkB1.jpg >

**Penjelasan Vlan Main Switch Trunk Gedung B**

Konfigurasi Main Switch Trunk ini bertujuan untuk mengatur port tertentu pada switch agar dapat mengirimkan lalu lintas dari beberapa VLAN ke perangkat lain, dalam hal ini Router0. Pertama, masuk ke mode konfigurasi interface FastEthernet 0/5, lalu diberi deskripsi trunk_to_Router0 untuk memudahkan identifikasi bahwa port ini digunakan sebagai jalur trunk menuju router. Selanjutnya, port tersebut dikonfigurasi menggunakan enkapsulasi dot1q, yang merupakan protokol standar IEEE untuk membawa data dari berbagai VLAN melalui satu koneksi fisik. Setelah itu, port diatur ke mode trunk, yang memungkinkan port ini membawa lalu lintas dari banyak VLAN sekaligus, bukan hanya satu VLAN seperti pada mode akses. Konfigurasi ini sangat penting untuk komunikasi antar VLAN (inter-VLAN routing) melalui router, karena memungkinkan data dari berbagai segmen jaringan dikirim ke Router0 untuk diteruskan atau diproses lebih lanjut. Dengan demikian, konfigurasi ini berperan sebagai penghubung utama antara switch dan router dalam jaringan yang menggunakan VLAN.

#### 6. Konfigurasi Router Gedung B

**Vlan Router Gedung B**

```
Router#conf t
Router(config)#interface gig0/0
Router(config-if)#description to_Multilayer_Switch1
Router(config-if)#no sh
Router(config-if)#ip address 10.10.10.2 255.255.255.252
Router(config-if)#ex
Router(config)#ex

```

**Dokumentasi Vlan Router Gedung B**

<img src = RB.jpg >

**Penjelasan Vlan Router Gedung B**

Konfigurasi Router Gedung B ini bertujuan untuk mengaktifkan koneksi antara router dan switch layer 3 (multilayer switch) yang ada di jaringan Gedung B. Pertama, dilakukan konfigurasi pada antarmuka GigabitEthernet 0/0 yang diberi deskripsi to_Multilayer_Switch1, agar mudah dikenali sebagai jalur koneksi menuju switch tersebut. Kemudian antarmuka ini diaktifkan menggunakan perintah no shutdown, karena secara default antarmuka router dalam keadaan nonaktif. Selanjutnya, diberikan alamat IP 10.10.10.2 dengan subnet mask 255.255.255.252, yang menunjukkan bahwa alamat ini berada dalam jaringan point-to-point yang kecil, hanya terdiri dari dua host. Konfigurasi ini memungkinkan komunikasi antara router dan multilayer switch melalui koneksi khusus, biasanya digunakan untuk pertukaran routing atau pengiriman data lintas jaringan. Dengan kata lain, konfigurasi ini adalah langkah awal untuk menghubungkan router ke jaringan Gedung B secara logis dan fisik.
