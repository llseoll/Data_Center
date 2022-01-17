### Построение Underlay сети(BGP)  

1. Схема и адресация остается из прошлых лабораторных работ.
2. Используется топология из прошлых лабораторных, Spine - AS64512, Leaf AS64520-64523:
![Топология](https://github.com/llseoll/Data_Center/blob/main/Screenshot_6.jpg)
3. Конфигурация устройств:
<details>
<summary>Spine1</summary>

feature bgp  
  
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
