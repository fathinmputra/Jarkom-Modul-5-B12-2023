# Praktikum Jaringan Komputer
# Modul 5
### Kelompok B12
### Anggota :
|            Nama           |     NRP    |
| ------                    | ------     |
| Darvin Exaudi Simanjuntak | 5025211172 |
| Fathin Muhashibi Putra    | 5025211229 |

**Soal :** [link](https://docs.google.com/document/d/1VhSv39bFIjLpzn3_5u4l2phZCY3EDAGoKxNUObLNvNg/edit)

# Topologi
<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/03c7745d-fa03-49ae-8f19-db722960451d">

Keterangan:	
- Richter adalah DNS Server
- Revolte adalah DHCP Server
- Sein dan Stark adalah Web Server
- Jumlah Host pada SchwerMountain adalah 64
- Jumlah Host pada LaubHills adalah 255
- Jumlah Host pada TurkRegion adalah 1022
- Jumlah Host pada GrobeForest adalah 512

## Penentuan Subnet :

<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/f6c4a764-37c8-486a-8bab-58a3c9155457">

## METODE VLSM
**Langkah 1** - Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan melakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.

<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/6701fceb-9d68-4966-ae50-8699920b7649">

Berdasarkan total IP dan netmask yang dibutuhkan, maka kita dapat menggunakan netmask /20 untuk memberikan pengalamatan IP pada subnet.

Kemudian, subnet diurutkan berdasarkan jumlah netmask : 

<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/098061d4-fd4f-4eb6-a27d-96d683f04949">

**Langkah 2** - Subnet besar yang dibentuk memiliki NID 192.184.0.0 dengan netmask /20. Kemudian menghitung pembagian IP berdasarkan NID dan netmask menggunakan pohon (tree).

<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/9d46ea68-1755-4cf4-995f-63e60500d686">


**Langkah 3** - Melakukan subnetting dengan menggunakan pohon (tree)  tersebut untuk pembagian IP sesuai dengan kebutuhan masing-masing subnet yang ada.

<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/38be86b9-3e29-44d7-9067-8dfdf42d9a0b">

Berdasarkan Tree tersebut akan mendapat pembagian IP sebagai berikut.

<img width="709" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/f79ca2b0-aa96-4fcf-9a77-b7657270aab5">


## Configuration Network
Setelah mendapatkan hasil pembagian IP, kita dapat memasukkan pembagian IP tersebut ke dalam konfigurasi di `GNS3`.

Berikut adalah konfigurasi `router, client, dan server` pada `GNS3` menggunakan pembagian IP `VLSM` :

**ROUTER :**

- Aura
```
#Aura
auto eth0
iface eth0 inet dhcp

# kanan
auto eth1
iface eth1 inet static
	address 192.184.14.149
	netmask 255.255.255.252

# bawah
auto eth2
iface eth2 inet static
	address 192.184.14.145
	netmask 255.255.255.252
```

- Heiter
```
# Heiter
# kiri
auto eth0
iface eth0 inet static
	address 192.184.14.150
	netmask 255.255.255.252

# atas
auto eth1
iface eth1 inet static
	address 192.184.0.1
	netmask 255.255.248.0

# kanan
auto eth2
iface eth2 inet static
	address 192.184.8.1
	netmask 255.255.252.0
```

- Frieren
```
# Frieren
# atas
auto eth0
iface eth0 inet static
	address 192.184.14.146
	netmask 255.255.255.252

# kanan
auto eth1
iface eth1 inet static
	address 192.184.14.141
	netmask 255.255.255.252

# kiri
auto eth2
iface eth2 inet static
	address 192.184.14.137
	netmask  255.255.255.252
```

- Himmel
```
# Himmel
# kanan
auto eth0
iface eth0 inet static
	address 192.184.14.138
	netmask 255.255.255.252

# atas
auto eth1
iface eth1 inet static
	address 192.184.12.1
	netmask 255.255.254.0

# bawah
auto eth2
iface eth2 inet static
	address 192.184.14.1
	netmask  255.255.255.128
```

- Fern
```
# Fern
# kanan
auto eth0
iface eth0 inet static
	address 192.184.14.2
	netmask 255.255.255.128

# atas
auto eth1
iface eth1 inet static
	address 192.184.14.133
	netmask 255.255.255.252

# kiri
auto eth2
iface eth2 inet static
	address 192.184.14.129
	netmask  255.255.255.252
```

**CLIENT :**

- GrobeForest
```
# GrobeForest
#auto eth0
#iface eth0 inet static
#	address 192.184.8.2
#	netmask 255.255.252.0
#        gateway 192.184.8.1

auto eth0
iface eth0 inet dhcp
```

- TurkRegion
```
# TurkRegion
#auto eth0
#iface eth0 inet static
#	address 192.184.0.2
#	netmask 255.255.248.0
#        gateway 192.184.0.1

auto eth0
iface eth0 inet dhcp
```

- LaubHills
```
# LaubHills
#auto eth0
#iface eth0 inet static
#	address 192.184.12.2
#	netmask 255.255.254.0
#        gateway 192.184.12.1

auto eth0
iface eth0 inet dhcp
```

- SchwerMountain
```
# SchwerMountain
#auto eth0
#iface eth0 inet static
#	address 192.184.14.3
#	netmask 255.255.255.128
#        gateway 192.184.14.1

auto eth0
iface eth0 inet dhcp
```

**Server :**

- Sein
```
# Sein
auto eth0
iface eth0 inet static
	address 192.184.8.2
	netmask 255.255.252.0
        gateway 192.184.8.1
```

- Stark
```
# Stark
auto eth0
iface eth0 inet static
	address 192.184.14.142
	netmask 255.255.255.252
        gateway 192.184.14.141
```

- Richter
```
# Richter
auto eth0
iface eth0 inet static
	address 192.184.14.134
	netmask 255.255.255.252
        gateway 192.184.14.133
```

- Revolte
```
# Revolte
auto eth0
iface eth0 inet static
	address 192.184.14.130
	netmask 255.255.255.252
        gateway 192.184.14.129
```

## Routing
Supaya semua subnet dapat saling terhubung, maka diperlukan routing. Berikut adalah perintah routing pada masing masing router GNS :

- Aura
```
route add -net 192.184.0.0 netmask 255.255.248.0 gw 192.184.14.150
route add -net 192.184.8.0 netmask 255.255.252.0 gw 192.184.14.150
route add -net 192.184.14.140 netmask 255.255.255.252 gw 192.184.14.146
route add -net 192.184.14.136 netmask 255.255.255.252 gw 192.184.14.146
route add -net 192.184.12.0 netmask 255.255.254.0 gw 192.184.14.146
route add -net 192.184.14.0 netmask 255.255.255.128 gw 192.184.14.146
route add -net 192.184.14.132 netmask 255.255.255.252 gw 192.184.14.146
route add -net 192.184.14.128 netmask 255.255.255.252 gw 192.184.14.146
```

- Heiter
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.184.14.149
```

- Frieren
```
route add -net 192.184.12.0 netmask 255.255.254.0 gw 192.184.14.138
route add -net 192.184.14.0 netmask 255.255.255.128 gw 192.184.14.138
route add -net 192.184.14.132 netmask 255.255.255.252 gw 192.184.14.138
route add -net 192.184.14.128 netmask 255.255.255.252 gw 192.184.14.138
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.184.14.145
```

- Himmel
```
route add -net 192.184.14.128 netmask 255.255.255.252 gw 192.184.14.2
route add -net 192.184.14.132 netmask 255.255.255.252 gw 192.184.14.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.184.14.137
```

- Fern
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.184.14.1
```

> Pada setiap router di GNS3, terdapat file `route.sh` yang berisi command-command routing di atas sehingga tinggal bash filenya untuk melakukan routing.


## DHCP Configuration


# Soal
## NO. 1
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

### Penjelasan :
Untuk mengonfigurasikan `Aura` menggunakan iptables dan tanpa menggunakan MASQUERADE memakai peritah berikut :
```
ipsource=$(hostname -I | awk '{ print $
iptables -t nat -A POSTROUTING -s 192.184.0.0/20 -o eth0 -j SNAT --to-source $ipsource
```
> konfigurasi disimpan pada `.bashrc`

**Keterangan :**
1. `ipsource=$(hostname -I | awk '{ print $1 }')`
   - Menetapkan variabel `ipsource` dengan alamat IP dari host saat ini.
   - Menggunakan perintah `hostname -I` untuk mendapatkan daftar alamat IP host.
   - `awk '{ print $1 }'` digunakan untuk mengambil hanya alamat IP pertama dari daftar tersebut.

2. `iptables -t nat -A POSTROUTING -s 192.184.0.0/20 -o eth0 -j SNAT --to-source $ipsource`
   - Menambahkan aturan iptables untuk mengatur NAT pada tabel nat (`-t nat`).
   - Aturan ini diterapkan pada chain POSTROUTING (`-A POSTROUTING`), yang berarti setelah paket meninggalkan sistem.
   - Menggunakan opsi `-s 192.184.0.0/20` untuk menentukan subnet sumber dari mana paket berasal.
   - Opsi `-o eth0` mengarahkan paket ke interface jaringan `eth0`.
   - `-j SNAT` mengindikasikan bahwa paket tersebut akan di-NAT (Network Address Translated).
   - `--to-source $ipsource` menetapkan alamat IP sumber yang telah diperoleh sebelumnya sebagai alamat IP yang akan digunakan saat melakukan SNAT. Artinya, paket yang keluar akan memiliki alamat IP sumber yang sudah ditentukan.

**Screenshot Hasil :**

<img width="227" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/c649e91b-2f1a-48dc-8961-c2a6272b527c">


## NO. 2
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

### Penjelasan :
Untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP, menggunakan command berikut ini :
```
iptables -F
iptables -A INPUT -p icmp -j ACCEPT
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
iptables -A INPUT -p udp -j DROP
```
> Command tersebut dijankan pada `SchwerMountain` dan disimpan pada script `no2.sh`.

**Keterangan :**
1. `iptables -F`: Membersihkan (flush) semua aturan pada tabel iptables.
2. `iptables -A INPUT -p icmp -j ACCEPT`: Mengizinkan paket ICMP (ping) masuk.
3. `iptables -A INPUT -p tcp --dport 8080 -j ACCEPT`: Mengizinkan paket TCP dengan tujuan port 8080 masuk.
4. `iptables -A INPUT -p tcp -j DROP`: Menolak semua paket TCP yang tidak sesuai dengan aturan sebelumnya.
5. `iptables -A INPUT -p udp -j DROP`: Menolak semua paket UDP tanpa pengecualian.

**Screenshot Hasil :**
- Menggunakan Port 8080 (bisa):
<img width="364" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/bb6131c7-5aa1-44b0-9174-35e61966dfc6">

<img width="363" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/45a26c62-66cd-4ca3-b755-4a583cbd6ec6">

- Menggunakan Port 80 (tidak bisa):
<img width="363" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/a5c4c0ce-c250-4010-9c50-a13a64fdc146">

<img width="364" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/988febfc-694b-43ee-a646-7efd486197d1">


## NO. 3
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

### Penjelasan :
Untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan dan selebihnya akan di drop, menggunakan command berikut ini :
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
> Command tersebut dijankan pada `Richter` dan `Revlote` dan disimpan pada script `no3.sh`.

**Keterangan :**
- `iptables -A INPUT`: Menambahkan aturan pada chain INPUT.
- `-p icmp`: Menentukan protokol yang diizinkan, dalam hal ini ICMP (ping).
- `-m connlimit --connlimit-above 3 --connlimit-mask 0`: Menggunakan modul connlimit untuk membatasi jumlah koneksi. Opsi ini menolak paket jika jumlah koneksi dari satu sumber (`--connlimit-above 3`) melebihi batas 3. Opsi `--connlimit-mask 0` menunjukkan bahwa pengecekan jumlah koneksi dilakukan per IP individual (tanpa pembagian subnet).
- `-j DROP`: Menentukan bahwa paket yang memenuhi kondisi di atas akan ditolak (DROP).

**Screenshot Hasil :**
Melakukan ping `Richter` pada 4 Device secara bersamaan :

- ping pada device pertama (GrobeForest)

<img width="362" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/109998c2-ac5f-4cfe-9d0e-7675e40e1871">

Keterangan : Berhasil

- ping pada device kedua (TurkRegion)

<img width="364" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/434f269a-1682-4e74-b2e6-b9c2dcd1e76a">

Keterangan : Berhasil

- ping pada device ketiga (Heiter)

<img width="368" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/06e0cf1c-f637-494e-92b0-df1cb76766e8">

Keterangan : Berhasil

- ping pada device keempat (Frieren)
<img width="365" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/520aad62-e503-4e54-be84-c44cf90a1501">

Keterangan : Gagal, karena maksimal ping hanya 3 device secara bersamaan.

## NO. 4
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

### Penjelasan :
Untuk melakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest, menggunakan command berikut ini :
```
service ssh start

iptables -A INPUT -p tcp --dport 22 -s 192.184.8.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP

service ssh restart
```
> Command tersebut dijankan pada `Sein` dan `Stark` dan disimpan pada script `no4.sh`.

**Keterangan :**
- `service ssh start`: Memulai (start) layanan SSH. Ini akan memulai daemon SSH untuk menerima koneksi.
- `iptables -A INPUT -p tcp --dport 22 -s 192.184.8.0/22 -j ACCEPT`: Menambahkan aturan iptables pada chain INPUT untuk mengizinkan koneksi TCP ke port 22 (port default SSH) dari alamat IP dalam rentang 192.184.8.0/22. Artinya, hanya alamat IP dalam rentang tersebut yang diizinkan terhubung melalui SSH.
- `iptables -A INPUT -p tcp --dport 22 -j DROP`: Menambahkan aturan iptables pada chain INPUT untuk menolak semua koneksi TCP ke port 22 yang tidak sesuai dengan aturan sebelumnya. Ini berarti, jika koneksi tidak berasal dari alamat IP dalam rentang 192.184.8.0/22, koneksi tersebut akan ditolak.
- `service ssh restart`: Me-restart layanan SSH. Ini diperlukan agar perubahan konfigurasi pada iptables terkait SSH dapat diterapkan tanpa harus me-restart seluruh sistem.

**Screenshot Hasil :**
Melakukan telnet dengan IP Web Server :

- Pada SchwerMountain :
  
<img width="362" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/baf2b173-056d-4e5e-88a4-26054e04a8c8">

Keterangan : Gagal

- Pada GrobeForest :

<img width="365" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/39ff6734-d147-46a7-a60b-0aee4bdaf69c">

Keterangan : Berhasil

## NO. 5
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

### Penjelasan :
Untuk mengatur akses menuju WebServer yang hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00, menggunakan command berikut ini :
```
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```
> Command tersebut dijankan pada `Sein` dan `Stark` dan disimpan pada script `no5.sh`.

**Keterangan :**
- `iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT`: Mengizinkan koneksi pada hari Senin hingga Jumat antara pukul 08:00 hingga 16:00.
- `iptables -A INPUT -j REJECT`: Menolak semua koneksi yang tidak memenuhi aturan waktu yang telah ditentukan sebelumnya.

**Screenshot Hasil :**
- Diperbolehkan (jam kerja) :
  -  ubah dulu menjadi jam kerja `date -u 1213100023`
  -  kemudian ping Web Server (Sein atau Stark)
 
<img width="364" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/51e9cd0f-0de5-4c8c-93a6-9fb7599e7d96">

<img width="362" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/a781cd79-4137-4605-a788-5fe091d86c23">

- Tidak diperbolehkan (diluar jam kerja) :
  -  ubah dulu menjadi diluar jam kerja `date -u 1213220023`
  -  kemudian ping Web Server (sein atau Stark)

<img width="362" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/c7974bbe-f399-43a7-b305-edb427e2fa2e">

<img width="364" alt="image" src="https://github.com/fathinmputra/Jarkom-Modul-5-B12-2023/assets/103252800/e1da905b-698b-4a32-967d-2dbe9dab1d74">


## NO. 6
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

## NO. 7
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## NO. 8
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## NO. 9
Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)

## NO. 10
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 










