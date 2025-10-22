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
