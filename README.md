# Jarkom_Modul4_Lapres_D04

## Tim D4

## Kevin Angga Wijaya - 05111840000024

## Samuel C. Y. Sinambela -05111840000036

### 1. Menentukan Subnet

![subnet](/img/subnet.JPG)

- Server dan cloud diberikan sesuai dengan IP yang di soal.

### 2. Menghitung Jumlah IP dan Netask dari Tiap Subnet

![hitung](/img/hitung_subnet.JPG)

### 3. VLSM

#### - Membentuk Tree dari VLSM

![VLSM](/img/VLSM.png)

- Lalu input ke cpt berdasarkan dari tree.
- Contoh pada subnet A1

  - Pada Surabaya

    ![Surabaya](/img/A1_SURABAYA.JPG)

  - Pada Sampang

    ![Sampang](/img/A1_SAMPANG.JPG)

#### - Routing

![routing](/img/routing_vlsm.JPG)

- Lalu input routing ke cpt
- Contoh pada Surabaya

![Routing](/img/routing_surabaya.JPG)

### 4. CIDR

#### - Membentuk Tree dari CIDR

![CIDR](/img/CIDR.png)

Untuk pembagian netmask, bisa dilihat pada gambar dibawah ini:

![bagi-netmask](/img/bagi-netmask.png)

Dari gambar diatas, dapat dilihat bahwa A13-A12 digabung sehingga membentuk /21 lalu hasil dari (A13-A12) akan digabung dengan A11 yang akan membentuk /20. Kemudian A2-A9 digabung dan membentuk /20 lalu hasil dari A2-A9 akan digaubng dengan A3 dan membentuk /19 dan seterusnya.

![table-cidr](/img/table-cidr.png)

Hasil dari pembagian tree.

#### - Topologi UML

Topologi pada UML :

```bash
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch6 > /dev/null < /dev/null &
uml_switch -unix switch7 > /dev/null < /dev/null &
uml_switch -unix switch8 > /dev/null < /dev/null &
uml_switch -unix switch9 > /dev/null < /dev/null &
uml_switch -unix switch10 > /dev/null < /dev/null &
uml_switch -unix switch11 > /dev/null < /dev/null &
uml_switch -unix switch12 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch14 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.78.21 eth1=daemon,,,switch15 eth2=daemon,,,switch10 eth3=daemon,,,switch9 eth4=daemo$
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch10 eth1=daemon,,,switch12 eth2=daemon,,,switch11 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch12 eth1=daemon,,,switch14 eth2=daemon,,,switch13 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch9 eth1=daemon,,,switch5 eth2=daemon,,,switch6 eth3=daemon,,,switch8 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch5 eth1=daemon,,,switch4 eth2=daemon,,,switch2 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch4 eth1=daemon,,,switch3 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch8 eth1=daemon,,,switch7 mem=64M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch1 mem=64M &

# Client
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch15 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch14 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch13 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch13 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch11 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch4 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch3 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch6 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch7 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch8 mem=64M &
```

Forward IPv4 untuk UML Surabaya, Probolinggo, Pasuruan, Batu, Kediri, Blitar, Madiun dengan cara `nano /etc/sysctl.conf` dan uncomment `#net.ipv4.forward=1`. Lalu simpan dan jalankan `sysctl -p`.

#### - Interfaces tiap UML

- Surabaya

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.78.22
netmask 255.255.255.252
gateway 10.151.78.21

auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 10.151.79.41
netmask 255.255.255.252
```

Buat route.sh dengan isi:

```
ip route add 192.168.128.0/18 via 192.168.192.2 dev eth2
ip route add 192.168.0.0/19 via 192.168.32.2 dev eth3
ip route add 10.151.79.44/30 via 192.168.32.2 dev eth3
```

- Probolinggo

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252
gateway 192.168.144.1

auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.255.128

auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0

PASURUAN
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.160.1
netmask 255.255.252.0
```

Buat route.sh yang berisi:

```
ip route add 192.168.128.0/20 via 192.168.144.2 dev eth1
```

- Batu

```
auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0
```

Buat route.sh yang berisi:

```
ip route add 192.168.18.0/28 via 192.168.16.2 dev eth3
ip route add 192.168.0.0/21 via 192.168.8.2 dev eth1
ip route add 10.151.79.44/30 via 192.168.8.2 dev eth1

```

- Kediri

```
auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.255.252
gateway 192.168.8.1

auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.151.79.45
netmask 255.255.255.252
#
```

Buat route.sh yang berisi:

```
ip route add 192.168.0.0/27 via 192.168.4.2 dev eth1
```

- Blitar

```
auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateway 192.168.4.1

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.255.224

```

- Madiun

```
auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240
```

- Malang

```
auto eth0
iface eth0 inet static
address 10.151.79.46
netmask 255.255.255.252
gateway 10.151.79.45
```

- Mojokerto

```
auto eth0
iface eth0 inet static
address 10.151.79.42
netmask 255.255.255.252
gateway 10.151.79.41

```

- Sampang

```
auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1

```

- Bondowoso

```
auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.192
gateway 192.168.136.1

```

- Jember

```
auto eth0
iface eth0 inet static
address 192.168.132.1
netmask 255.255.248.0
gateway 192.168.128.1

```

- Banyuwangi

```
auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1

```

- Sidoarjo

```
auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateway 192.168.160.1

```

- Lumajang

```
auto eth0
iface eth0 inet static
address 192.168.4.3
netmask 255.255.255.0
gateway 192.168.4.1

```

- Tulungagung

```
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.224
gateway 192.168.0.1

```

- Nganjuk

```
auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1

```

- Bojonegoro

```
auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1

```

- Jombang

```
auto eth0
iface eth0 inet static
address 192.168.16.3
netmask 255.255.254.0
gateway 192.168.16.1

```
