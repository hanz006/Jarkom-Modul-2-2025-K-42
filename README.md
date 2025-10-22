# Jarkom-Modul-2-2025-K-42
| Nama | NRP |
| :-------- | :------- | 
| S. Farhan Baig | 5027241097| 
| Dimas Satya Andhika | 5027241032 |

# Soal 1
<img width="2960" height="1610" alt="image" src="https://github.com/user-attachments/assets/9c1f21ee-cb43-47b7-8d67-4ce6b75b18ee" />

Membuat topology seperti yang diminta serta membuat alamat dan default gateway tiap tokoh sesuai glosarium

### Eonwe
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.222.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.222.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.222.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.222.4.1
	netmask 255.255.255.0
```
### Earendil
```
auto eth0
iface eth0 inet static
	address 192.222.1.2
	netmask 255.255.255.0
	gateway 192.222.1.1
```
### Elwing
```
auto eth0
iface eth0 inet static
	address 192.222.1.3
	netmask 255.255.255.0
	gateway 192.222.1.1
```
### Cirdan
```
auto eth0
iface eth0 inet static
	address 192.222.2.2
	netmask 255.255.255.0
	gateway 192.222.2.1
```
### Elrond
```
auto eth0
iface eth0 inet static
	address 192.222.2.3
	netmask 255.255.255.0
	gateway 192.222.2.1
```
### Maglor
```
auto eth0
iface eth0 inet static
	address 192.222.2.4
	netmask 255.255.255.0
	gateway 192.222.2.1
```
### Sirion
```
auto eth0
iface eth0 inet static
	address 192.222.3.2
	netmask 255.255.255.0
	gateway 192.222.3.1
```
### Tirion
```
auto eth0
iface eth0 inet static
	address 192.222.3.3
	netmask 255.255.255.0
	gateway 192.222.3.1
```
### Valmar
```
auto eth0
iface eth0 inet static
	address 192.222.3.4
	netmask 255.255.255.0
	gateway 192.222.3.1
```
### Lindon
```
auto eth0
iface eth0 inet static
	address 192.222.3.5
	netmask 255.255.255.0
	gateway 192.222.3.1
```
### Vingilot
```
auto eth0
iface eth0 inet static
	address 192.222.3.6
	netmask 255.255.255.0
	gateway 192.222.3.1
```

# Soal 2
```
#!/bin/bash

echo 1 > /proc/sys/net/ipv4/ip_forward

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

iptables -A FORWARD -i eth1 -o eth2 -j ACCEPT
iptables -A FORWARD -i eth2 -o eth1 -j ACCEPT
iptables -A FORWARD -i eth1 -o eth3 -j ACCEPT
iptables -A FORWARD -i eth3 -o eth1 -j ACCEPT
iptables -A FORWARD -i eth1 -o eth4 -j ACCEPT
iptables -A FORWARD -i eth4 -o eth1 -j ACCEPT
iptables -A FORWARD -i eth2 -o eth3 -j ACCEPT
iptables -A FORWARD -i eth3 -o eth2 -j ACCEPT
iptables -A FORWARD -i eth2 -o eth4 -j ACCEPT
iptables -A FORWARD -i eth4 -o eth2 -j ACCEPT
iptables -A FORWARD -i eth3 -o eth4 -j ACCEPT
iptables -A FORWARD -i eth4 -o eth3 -j ACCEPT

iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
iptables -A FORWARD -i eth2 -o eth0 -j ACCEPT
iptables -A FORWARD -i eth3 -o eth0 -j ACCEPT
iptables -A FORWARD -i eth4 -o eth0 -j ACCEPT
```
Aktifkan IP forwarding dengan perintah echo 1 > /proc/sys/net/ipv4/ip_forward agar kernel Linux dapat meneruskan paket antar-interface dan berfungsi sebagai router.

Terapkan NAT (Network Address Translation) menggunakan iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE untuk mengubah alamat sumber dari jaringan internal menjadi alamat IP interface eth0 (terhubung ke NAT Cloud), sehingga seluruh host internal dapat mengakses Internet.

Tambahkan aturan FORWARD pada iptables untuk mengizinkan lalu lintas antar-interface internal (eth1–eth4) agar setiap jaringan Barat, Timur, dan DMZ dapat saling berkomunikasi.

Izinkan akses ke Internet dengan menambahkan aturan FORWARD dari setiap interface internal (eth1–eth4) menuju eth0, agar paket dari jaringan lokal bisa diteruskan keluar melalui NAT.

Dengan konfigurasi tersebut, seluruh jaringan internal dapat saling berhubungan dan keluar ke Internet melalui router Eonwe secara terpusat.

# Soal 3
```
#!/bin/bash

ip route add default via 10.15.43.29

echo "nameserver 192.168.122.1" > /etc/resolv.conf

echo "Gateway & DNS awal diatur untuk $(hostname)"

echo "NAT & Routing Internal aktif di Eonwe"
```

# Soal 4
### Set Up DNS
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf

apt update
apt install -y bind9 procps

echo "Setup DNS dasar selesai!
```
### Master
```
#!/bin/bash
echo "tirion" > /etc/hostname
hostname tirion
echo "127.0.1.1 tirion" >> /etc/hosts
ip addr add 192.234.3.3/24 dev eth0 2>/dev/null
ip route add default via 10.15.43.29 2>/dev/null

mkdir -p /etc/bind/zones

cat > /etc/bind/zones/db.k42.com <<'EOF'
$TTL 86400
@   IN  SOA ns1.k42.com. admin.k42.com. (
        2025101301
        3600
        1800
        604800
        86400 )
    IN  NS  ns1.k42.com.
    IN  NS  ns2.k42.com.
ns1 IN  A   192.234.3.3
ns2 IN  A   192.234.3.4
@   IN  A   10.15.43.35
sirion   IN  A   10.15.43.35
lindon   IN  A   10.15.43.38
vingilot IN  A   10.15.43.39
www     IN  CNAME   sirion
static  IN  CNAME   lindon
app     IN  CNAME   vingilot
EOF

cat > /etc/bind/named.conf.local <<'EOF'
zone "k42.com" {
    type master;
    file "/etc/bind/zones/db.k42.com";
    allow-transfer { 192.234.3.4; };
    notify yes;
};
EOF

cat > /etc/bind/named.conf.options <<'EOF'
options {
    directory "/var/cache/bind";
    forwarders {
        192.168.122.1;
    };
    dnssec-validation no;
    listen-on-v6 { any; };
};
EOF

named-checkconf
named-checkzone k42.com /etc/bind/zones/db.k42.com
/usr/sbin/named -c /etc/bind/named.conf &
```
### Slave
```
#!/bin/bash
echo "valmar" > /etc/hostname
hostname valmar
echo "127.0.1.1 valmar" >> /etc/hosts
ip addr add 192.234.3.4/24 dev eth0 2>/dev/null
ip route add default via 10.15.43.29 2>/dev/null
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt update
apt install -y bind9 procps

cat > /etc/bind/named.conf.local <<'EOF'
zone "k42.com" {
    type slave;
    masters { 192.234.3.3; };
    file "/var/lib/bind/db.k42.com";
};
EOF

cat > /etc/bind/named.conf.options <<'EOF'
options {
    directory "/var/cache/bind";
    forwarders {
        192.168.122.1;
    };
    dnssec-validation no;
    listen-on-v6 { any; };
};
EOF

/usr/sbin/named -c /etc/bind/named.conf &
```

# Soal 5
```
#!/bin/bash
echo "valmar" > /etc/hostname
hostname valmar
echo "127.0.1.1 valmar" >> /etc/hosts
ip route add default via 10.15.43.29 2>/dev/null
ip addr add 192.234.3.4/24 dev eth0 2>/dev/null

apt update
apt install -y bind9

cat > /etc/bind/named.conf.local <<'EOF'
zone "K42.com" {
    type slave;
    file "/var/cache/bind/db.K42.com";
    masters { 192.234.3.3; };
};
EOF

service bind9 restart
```
