### Построение Underlay сети(ISIS)  

1. Аналогичное с предыдущей лабораторной не вижу смысла в разделении сети на разные зоны.
2. Используется топология из прошлых лабораторных:
![Топология](https://github.com/llseoll/Data_Center/blob/main/Screenshot_6.png)
3. Конфигурация устройств:
<details>
<summary>Spine1</summary>
  
version 9.2(2) Bios:version  
hostname Spine1  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.1/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.1.5/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/3  
  no switchport  
  ip address 192.168.1.9/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/4  
  no switchport  
  ip address 192.168.5.1/29  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0001.00  
!end  
  
</details>
<details>
<summary>Spine2</summary>
  
version 9.2(2) Bios:version  
hostname Spine2  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.2.1/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.5/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/3  
  no switchport  
  ip address 192.168.2.9/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/4  
  no switchport  
  ip address 192.168.5.2/29  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0010.00  
!end  
  
</details>
</details>
<details>
<summary>Spine3</summary>
  
version 9.2(2) Bios:version  
hostname Spine3  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.3.1/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.5.3/29  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  

interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0011.00  
!end  
  
</details>
<details>
<summary>Leaf4</summary>
  
version 9.2(2) Bios:version  
hostname Leaf4  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.2/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.2/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/7  
  no switchport  
  ip address 192.168.50.1/24  
  no shutdown  
    
 interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0100.00  
!end  
  
</details>
<details>
<summary>Leaf5</summary>
  
version 9.2(2) Bios:version  
hostname Leaf5  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.6/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.6/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  

 interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0101.00  
!end  
  
</details>
<summary>Leaf6</summary>
  
version 9.2(2) Bios:version  
hostname Leaf6  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.1.10/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/2  
  no switchport  
  ip address 192.168.2.10/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/7  
  no switchport  
  ip address 192.168.100.1/24  
  no shutdown  
    
 interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0110.00  
!end  
  
</details>
<summary>Leaf7</summary>
  
version 9.2(2) Bios:version  
hostname Leaf7  
  
interface Ethernet1/1  
  no switchport  
  ip address 192.168.3.2/30  
  isis network point-to-point  
  ip router isis 1  
  no shutdown  
  
interface Ethernet1/7  
  no switchport  
  ip address 192.168.150.1/24  
  no shutdown  
    
 interface mgmt0  
  vrf member management  
line console  
line vty  
boot nxos bootflash:/nxos.9.2.2.bin   
router isis 1  
  net 49.0000.0000.0000.0111.00  
!end  
  
</details>

