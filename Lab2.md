Пересобрал Схему из Лабораторной работы 1 на NXOS, доступ admin:123Qwerty=, лаба:
http://10.120.0.18/legacy/Lab2.unl/topology

![Топология](https://github.com/llseoll/Data_Center/blob/main/Screenshot_5.jpg)

Связку Spine-Leaf сделал на L3, Spine 192.168.<номер свича>.1/30, 5/30, 9/30. Spine-Spine 192.168.5.0/29. Клиенты 192.168.50.0/24, 192.168.100.0/24, 192.168.150.0/24.
Настроил через добавление подсетей в глобальной настройке, почему-то на интерфейсах команды ip ospf id area 0 и ip ospf bfd не заработали. Так же не было redistribute connected, добавил через redistribute direct route-map + RM с acl.
