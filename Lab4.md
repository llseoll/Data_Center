### Построение Underlay сети(BGP)  

1. Схема и адресация остается из прошлых лабораторных работ.
2. Используется топология из прошлых лабораторных, Spine - AS64512, Leaf AS64520-64523:
![Топология](https://github.com/llseoll/Data_Center/blob/main/Screenshot_6.jpg)
3. Конфигурация устройств:
<details>
<summary>Spine1</summary>

hostname Spine1    
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.1/30  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.1.5/30  
  no shutdown  
  
interface Ethernet1/3  
  no switchport  
  ip address 192.168.1.9/30  
  no shutdown  
  
interface Ethernet1/4  
  no switchport  
  ip address 192.168.5.1/29  
  no shutdown  
  
router bgp 64512  
  router-id 1.1.1.1  
  address-family ipv4 unicast  
    network 192.168.1.0/30  
    network 192.168.1.4/30  
    network 192.168.1.8/30  
  template peer Leaf4  
    remote-as 64520  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Leaf5  
    remote-as 64521  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Leaf6  
    remote-as 64522  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine1  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine2  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine3  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.1.2  
    inherit peer Leaf4  
  neighbor 192.168.1.6  
    inherit peer Leaf5  
  neighbor 192.168.1.10  
    inherit peer Leaf6  
  neighbor 192.168.5.2  
    inherit peer Spine2  
  neighbor 192.168.5.3  
    inherit peer Spine3  
    
!end  
  
</details>
<details>
<summary>Spine2</summary>
  
hostname Spine2  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.2.1/30  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.5/30  
  no shutdown  
  
interface Ethernet1/3  
  no switchport  
  ip address 192.168.2.9/30  
  no shutdown  
  
interface Ethernet1/4  
  no switchport  
  ip address 192.168.5.2/29  
  no shutdown  
  
router bgp 64512  
  router-id 2.2.2.2  
  address-family ipv4 unicast  
    network 192.168.2.0/30  
    network 192.168.2.4/30  
    network 192.168.2.8/30  
  template peer Leaf4  
    remote-as 64520  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Leaf5  
    remote-as 64521  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Leaf6  
    remote-as 64522  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine1  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine3  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.2.2  
    inherit peer Leaf4  
  neighbor 192.168.2.6  
    inherit peer Leaf5  
  neighbor 192.168.2.10  
    inherit peer Leaf6  
  neighbor 192.168.5.1  
    inherit peer Spine1  
  neighbor 192.168.5.3  
    inherit peer Spine3  
  
!end  
  
</details>
<details>
<summary>Spine3</summary>
  
hostname Spine3  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.3.1/30  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.5.3/29  
  no shutdown  
  
router bgp 64512  
  address-family ipv4 unicast  
    network 192.168.3.0/30  
  template peer Leaf7  
    remote-as 64523  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine1  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine2  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.3.2  
    inherit peer Leaf7  
  neighbor 192.168.5.1  
    inherit peer Spine1  
  neighbor 192.168.5.2  
    inherit peer Spine2  
  
!end  
  
</details>
<details>
<summary>Leaf4</summary>
   
hostname Leaf4  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.2/30  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.2/30  
  no shutdown  
  
interface Ethernet1/7  
  no switchport  
  ip address 192.168.50.1/24  
  no shutdown  
  
router bgp 64520  
  router-id 4.4.4.4  
  address-family ipv4 unicast  
    network 192.168.50.0/24  
  template peer Spine1  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine2  
    remote-as 64512
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.1.1  
    inherit peer Spine1  
  neighbor 192.168.2.1  
    inherit peer Spine2  
  
!end  
  
</details>
<details>
<summary>Leaf5</summary>
  
hostname Leaf5  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.6/30  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.6/30  
  no shutdown  
  
router bgp 64521  
  router-id 5.5.5.5  
  address-family ipv4 unicast  
  template peer Spine1  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine2  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.1.5  
    inherit peer Spine1  
  neighbor 192.168.2.5  
    inherit peer Spine2  
  
!end  
  
</details>
<details>
<summary>Leaf6</summary>
  
hostname Leaf6  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.2.10/30  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.1.10/30  
  no shutdown  
  
interface Ethernet1/7  
  no switchport  
  ip address 192.168.100.1/24  
  no shutdown  
  
router bgp 64522  
  router-id 6.6.6.6  
  address-family ipv4 unicast  
    network 192.168.100.0/24  
  template peer Spine1  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  template peer Spine2  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.1.9  
    inherit peer Spine1  
  neighbor 192.168.2.9  
    inherit peer Spine2  
  
!end  
  
</details>
<details>
<summary>Leaf7</summary>
  
hostname Leaf7  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.3.2/30  
  no shutdown  
  
interface Ethernet1/7  
  no switchport  
  ip address 192.168.150.1/24  
  no shutdown  
  
router bgp 64523  
  router-id 7.7.7.7  
  address-family ipv4 unicast  
    network 192.168.150.0/24  
  template peer Spine3  
    remote-as 64512  
    log-neighbor-changes  
    address-family ipv4 unicast  
  neighbor 192.168.3.1  
    inherit peer Spine3  
  
!end  
  
</details>  


  
