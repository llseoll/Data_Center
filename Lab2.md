### Построение Underlay сети(OSPF)

Пересобрал Схему из Лабораторной работы 1 на NXOS, доступ admin:123Qwerty=, лаба:
http://10.120.0.18/legacy/Lab2.unl/topology

![Топология](https://github.com/llseoll/Data_Center/blob/main/Screenshot_5.jpg)

1. Адресация совпадает с предыдущей лабой.  
Связку Spine-Leaf сделал на L3, Spine 192.168.<номер свича>.1/30, 5/30, 9/30. Spine-Spine 192.168.5.0/29. Клиенты 192.168.50.0/24, 192.168.100.0/24, 192.168.150.0/24.  
2. Не вижу смысла при данной топологии делать больше, чем 1 area, т.к. кол-во LSA сообщений будет небольшим, а задачи по фильтрации маршрутов на ABR нет.
3. Конфигурация устройств:
<details>
<summary>Spine1</summary>
version 9.2(2) Bios:version  
hostname Spine1  
vdc Spine1 id 1  
  limit-resource vlan minimum 16 maximum 4094  
  limit-resource vrf minimum 2 maximum 4096  
  limit-resource port-channel minimum 0 maximum 511  
  limit-resource u4route-mem minimum 248 maximum 248  
  limit-resource u6route-mem minimum 96 maximum 96  
  limit-resource m4route-mem minimum 58 maximum 58  
  limit-resource m6route-mem minimum 8 maximum 8  
  
feature ospf  
  
username admin password 5 $5$xzHb6s6T$42B.ksenYoK8avu3LcSjYZYYZ8H.0th1yCCTOG/kJvC  role network-admin  
ip domain-lookup  
ip access-list 101  
  10 permit ip 192.168.0.0 0.0.255.255 any   
snmp-server user admin network-admin auth md5 0x7c87232d76e7eacd40c909e2d830aa96 priv 0x7c87232d76e7eacd40c909e2d830aa96 localizedkey  
rmon event 1 description FATAL(1) owner PMON@FATAL  
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL  
rmon event 3 description ERROR(3) owner PMON@ERROR  
rmon event 4 description WARNING(4) owner PMON@WARNING  
rmon event 5 description INFORMATION(5) owner PMON@INFO  
  
vlan 1  
  
route-map ospf permit 10  
  match ip address 101   
vrf context management  
  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.1/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  

interface Ethernet1/2  
  no switchport  
  ip address 192.168.1.5/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  

interface Ethernet1/3  
  no switchport  
  ip address 192.168.1.9/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface Ethernet1/4  
  no switchport   
  ip address 192.168.5.1/29  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router ospf 1  
  router-id 192.168.1.1  
  network 192.168.1.0/30 area 0.0.0.0  
  network 192.168.1.4/30 area 0.0.0.0  
  network 192.168.1.8/30 area 0.0.0.0  
  network 192.168.5.0/29 area 0.0.0.0  
  redistribute direct route-map ospf  
  
!end  
  
</details>
  
<details>
<summary>Spine2</summary>
version 9.2(2) Bios:version    
hostname Spine2  
vdc Spine2 id 1  
  limit-resource vlan minimum 16 maximum 4094  
  limit-resource vrf minimum 2 maximum 4096  
  limit-resource port-channel minimum 0 maximum 511  
  limit-resource u4route-mem minimum 248 maximum 248  
  limit-resource u6route-mem minimum 96 maximum 96  
  limit-resource m4route-mem minimum 58 maximum 58  
  limit-resource m6route-mem minimum 8 maximum 8  
  
feature ospf  
  
username admin password 5 $5$as3/9Dkn$znzd28Y82AahmueFsE06cn7nbFZ5p4bo8yinANGrt7.  role network-admin  
ip domain-lookup  
ip access-list 101  
  10 permit ip 192.168.0.0 0.0.255.255 any   
copp profile strict  
snmp-server user admin network-admin auth md5 0x341fad63897e284856de4c4934caf770 priv 0x341fad63897e284856de4c4934caf770 localizedkey  
rmon event 1 description FATAL(1) owner PMON@FATAL  
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL  
rmon event 3 description ERROR(3) owner PMON@ERROR  
rmon event 4 description WARNING(4) owner PMON@WARNING  
rmon event 5 description INFORMATION(5) owner PMON@INFO  
  
vlan 1  
  
route-map ospf permit 10  
  match ip address 101   
vrf context management  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.2.1/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.5/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface Ethernet1/3  
  no switchport  
  ip address 192.168.2.9/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface Ethernet1/4  
  no switchport  
  ip address 192.168.5.2/29  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router ospf 1  
  router-id 192.168.2.1  
  network 192.168.2.0/30 area 0.0.0.0  
  network 192.168.2.4/30 area 0.0.0.0  
  network 192.168.2.8/30 area 0.0.0.0  
  network 192.168.5.0/30 area 0.0.0.0  
  redistribute direct route-map ospf  
  
!end  
</details>
<details>
<summary>Spine3</summary>
version 9.2(2) Bios:version  
hostname Spine3  
vdc Spine3 id 1  
  limit-resource vlan minimum 16 ma ximum 4094  
  limit-resource vrf minimum 2 maximum 4096  
  limit-resource port-channel minimum 0 maximum 511  
  limit-resource u4route-mem minimum 248 maximum 248  
  limit-resource u6route-mem minimum 96 maximum 96  
  limit-resource m4route-mem minimum 58 maximum 58  
  limit-resource m6route-mem minimum 8 maximum 8  
  
feature ospf  
  
username admin password 5 $5$FNPL5Jz5$Yq8PgFHE4hqY9sj47Z1h2B4UM8Yb8XCWI6K4plLoDx3  role network-admin  
ip domain-lookup  
ip access-list 101  
  10 permit ip 192.168.0.0 0.0.255.255 any   
snmp-server user admin network-admin auth md5 0x611812a19dd7e708404347d06febeac3 priv 0x611812a19dd7e708404347d06febeac3 localizedkey  
rmon event 1 description FATAL(1) owner PMON@FATAL  
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL  
rmon event 3 description ERROR(3) owner PMON@ERROR  
rmon event 4 description WARNING(4) owner PMON@WARNING  
rmon event 5 description INFORMATION(5) owner PMON@INFO  
  
vlan 1
  
route-map ospf permit 10  
  match ip address 101   
vrf context management  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.3.1/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown   
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.5.3/29  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router ospf 1  
  router-id 192.168.3.1  
  network 192.168.3.0/30 area 0.0.0.0   
  network 192.168.5.0/29 area 0.0.0.0  
  redistribute direct route-map ospf  
  
  
!end  
  
</details>
<details>
<summary>Leaf4</summary>
version 9.2(2) Bios:version  
hostname Leaf4  
vdc Leaf4 id 1  
  limit-resource vlan minimum 16 maximum 4094  
  limit-resource vrf minimum 2 maximum 4096  
  limit-resource port-channel minimum 0 maximum 511  
  limit-resource u4route-mem minimum 248 maximum 248  
  limit-resource u6route-mem minimum 96 maximum 96  
  limit-resource m4route-mem minimum 58 maximum 58  
  limit-resource m6route-mem minimum 8 maximum 8  
  
feature ospf  
  
username admin password 5 $5$sjAvtSPP$jk1JDECbMMe0uBpXHAMLET.ILJAn8DlwNUkfeAn0HIB  role network-admin  
ip domain-lookup  
ip access-list 101  
  10 permit ip 192.168.0.0 0.0.255.255 any   
snmp-server user admin network-admin auth md5 0xdee84800e26c74a8527a5d3c994f7b75 priv 0xdee84800e26c74a8527a5d3c994f7b75 localizedkey  
rmon event 1 description FATAL(1) owner PMON@FATAL  
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL  
rmon event 3 description ERROR(3) owner PMON@ERROR  
rmon event 4 description WARNING(4) owner PMON@WARNING  
rmon event 5 description INFORMATION(5) owner PMON@INFO  
  
vlan 1  
  
route-map ospf permit 10  
  match ip address 101   
vrf context management  
  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.2/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.2/30  
  ip ospf authentication-key 3 c15a77a8059d3296  
  ip ospf network point-to-point  
  no shutdown  
  
interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router ospf 1  
  router-id 192.168.50.1  
  network 192.168.1.0/30 area 0.0.0.0  
  network 192.168.2.0/30 area 0.0.0.0  
  redistribute direct route-map ospf  
  
!end  
   
</details>


