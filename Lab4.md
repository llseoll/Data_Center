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

4. Проверка связности:  
```
Leaf4# sh ip route bgp
IP Route Table for VRF "default"
'*' denotes best ucast next-hop
'**' denotes best mcast next-hop
'[x/y]' denotes [preference/metric]
'%<string>' in via output denotes VRF <string>

192.168.1.4/30, ubest/mbest: 1/0
    *via 192.168.1.1, [20/0], 00:39:55, bgp-64520, external, tag 64512
192.168.1.8/30, ubest/mbest: 1/0
    *via 192.168.1.1, [20/0], 00:39:55, bgp-64520, external, tag 64512
192.168.2.4/30, ubest/mbest: 1/0
    *via 192.168.1.1, [20/0], 00:39:55, bgp-64520, external, tag 64512
192.168.2.8/30, ubest/mbest: 1/0
    *via 192.168.1.1, [20/0], 00:39:55, bgp-64520, external, tag 64512
192.168.3.0/30, ubest/mbest: 1/0
    *via 192.168.1.1, [20/0], 00:39:55, bgp-64520, external, tag 64512
192.168.100.0/24, ubest/mbest: 1/0
    *via 192.168.1.1, [20/0], 00:25:06, bgp-64520, external, tag 64512
192.168.150.0/24, ubest/mbest: 1/0
    *via 192.168.2.1, [20/0], 00:23:26, bgp-64520, external, tag 64512

Leaf4#
Leaf4# sh ip bgp neighbors
BGP neighbor is 192.168.1.1, remote AS 64512, ebgp link, Peer index 3
  Inherits peer configuration from peer-template Spine1
  BGP version 4, remote router ID 1.1.1.1
  BGP state = Established, up for 00:40:04
  Peer is directly attached, interface Ethernet1/1
  Enable logging neighbor events
  Last read 00:00:49, hold time = 180, keepalive interval is 60 seconds
  Last written 00:00:58, keepalive timer expiry due 0.999174
  Received 79 messages, 15 notifications, 0 bytes in queue
  Sent 76 messages, 0 notifications, 0(0) bytes in queue
  Connections established 1, dropped 0
  Last reset by us never, due to No error
  Last reset by peer never, due to No error

  Neighbor capabilities:
  Dynamic capability: advertised (mp, refresh, gr) received (mp, refresh, gr)
  Dynamic capability (old): advertised received
  Route refresh capability (new): advertised received
  Route refresh capability (old): advertised received
  4-Byte AS capability: advertised received
  Address family IPv4 Unicast: advertised received
  Graceful Restart capability: advertised received

  Graceful Restart Parameters:
  Address families advertised to peer:
    IPv4 Unicast
  Address families received from peer:
    IPv4 Unicast
  Forwarding state preserved by peer for:
  Restart time advertised to peer: 120 seconds
  Stale time for routes advertised by peer: 300 seconds
  Restart time advertised by peer: 120 seconds
  Extended Next Hop Encoding Capability: advertised received
  Receive IPv6 next hop encoding Capability for AF:
    IPv4 Unicast

  Message statistics:
                              Sent               Rcvd
  Opens:                        16                 16
  Notifications:                 0                 15
  Updates:                       3                  6
  Keepalives:                   56                 40
  Route Refresh:                 0                  0
  Capability:                    2                  2
  Total:                        76                 79
  Total bytes:                 940               1124
  Bytes in queue:                0                  0

  For address family: IPv4 Unicast
  BGP table version 25, neighbor version 25
  9 accepted prefixes (9 paths), consuming 1944 bytes of memory
  1 sent prefixes (1 paths)
  Last End-of-RIB received 00:00:01 after session start
  Last End-of-RIB sent 00:00:01 after session start
  First convergence 00:00:01 after session start with 2 routes sent

  Local host: 192.168.1.2, Local port: 51697
  Foreign host: 192.168.1.1, Foreign port: 179
  fd = 67

BGP neighbor is 192.168.2.1, remote AS 64512, ebgp link, Peer index 4
  Inherits peer configuration from peer-template Spine2
  BGP version 4, remote router ID 2.2.2.2
  BGP state = Established, up for 00:39:24
  Peer is directly attached, interface Ethernet1/2
  Enable logging neighbor events
  Last read 00:00:49, hold time = 180, keepalive interval is 60 seconds
  Last written 00:00:58, keepalive timer expiry due 0.998880
  Received 65 messages, 8 notifications, 0 bytes in queue
  Sent 61 messages, 0 notifications, 0(0) bytes in queue
  Connections established 1, dropped 0
  Last reset by us never, due to No error
  Last reset by peer never, due to No error

  Neighbor capabilities:
  Dynamic capability: advertised (mp, refresh, gr) received (mp, refresh, gr)
  Dynamic capability (old): advertised received
  Route refresh capability (new): advertised received
  Route refresh capability (old): advertised received
  4-Byte AS capability: advertised received
  Address family IPv4 Unicast: advertised received
  Graceful Restart capability: advertised received

  Graceful Restart Parameters:
  Address families advertised to peer:
    IPv4 Unicast
  Address families received from peer:
    IPv4 Unicast
  Forwarding state preserved by peer for:
  Restart time advertised to peer: 120 seconds
  Stale time for routes advertised by peer: 300 seconds
  Restart time advertised by peer: 120 seconds
  Extended Next Hop Encoding Capability: advertised received
  Receive IPv6 next hop encoding Capability for AF:
    IPv4 Unicast

  Message statistics:
                              Sent               Rcvd
  Opens:                         9                  9
  Notifications:                 0                  8
  Updates:                       3                  6
  Keepalives:                   48                 40
  Route Refresh:                 0                  0
  Capability:                    2                  2
  Total:                        61                 65
  Total bytes:                 921               1124
  Bytes in queue:                0                  0

  For address family: IPv4 Unicast
  BGP table version 25, neighbor version 25
  9 accepted prefixes (9 paths), consuming 1944 bytes of memory
  1 sent prefixes (1 paths)
  Last End-of-RIB received 00:00:01 after session start
  Last End-of-RIB sent 00:00:01 after session start
  First convergence 00:00:01 after session start with 2 routes sent

  Local host: 192.168.2.2, Local port: 18063
  Foreign host: 192.168.2.1, Foreign port: 179
  fd = 68
```
  ![Ping](https://github.com/llseoll/Data_Center/blob/main/Screenshot_7.jpg)  
  
  
