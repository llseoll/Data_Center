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
