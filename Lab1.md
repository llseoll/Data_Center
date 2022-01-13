1) Добавлены и подключены между собой 3 Spine и 4 Leaf на устройствах Cisco IOL
2) Устройства объединены (VPC пару нужно настраивать?)
3) В качестве клиентов добавлены Cisco IOL
4) Связку Spine-Leaf сделал на L3, Spine 192.168.<номер свича>.1/30, 5/30, 9/30. Spine-Spine 192.168.5.0/29. Клиенты 192.168.50.0/24, 192.168.100.0/24, 192.168.150.0/24.
То есть:
Spine1#
Interface            IP Address      Interface Status
Eth1/1               192.168.1.1     protocol-up/link-up/admin-up
Eth1/2               192.168.1.5     protocol-up/link-up/admin-up
Eth1/3               192.168.1.9     protocol-up/link-up/admin-up
Eth1/4               192.168.5.1     protocol-up/link-up/admin-up
Spine2# 
Interface            IP Address      Interface Status
Eth1/1               192.168.2.1     protocol-up/link-up/admin-up
Eth1/2               192.168.2.5     protocol-up/link-up/admin-up
Eth1/3               192.168.2.9     protocol-up/link-up/admin-up
Eth1/4               192.168.5.2     protocol-up/link-up/admin-up
Spine3#
Interface            IP Address      Interface Status
Eth1/1               192.168.3.1     protocol-up/link-up/admin-up
Eth1/2               192.168.5.3     protocol-up/link-up/admin-up
Leaf4#
Interface            IP Address      Interface Status
Eth1/1               192.168.1.2     protocol-up/link-up/admin-up
Eth1/2               192.168.2.2     protocol-up/link-up/admin-up
Eth1/7               192.168.50.1    protocol-up/link-up/admin-up
Leaf5#
Interface            IP Address      Interface Status
Eth1/1               192.168.1.6     protocol-up/link-up/admin-up
Eth1/2               192.168.2.6     protocol-up/link-up/admin-up
Leaf6#
Interface            IP Address      Interface Status
Eth1/1               192.168.2.10    protocol-up/link-up/admin-up
Eth1/2               192.168.1.10    protocol-up/link-up/admin-up
Eth1/7               192.168.100.1   protocol-up/link-up/admin-up
Leaf7#
Interface            IP Address      Interface Status
Eth1/1               192.168.3.2     protocol-up/link-up/admin-up
Eth1/7               192.168.150.1   protocol-up/link-up/admin-up


Ссылка на лабу:
http://10.120.0.18/legacy/Lab1.unl/topology

Топология:

![Топология](https://github.com/llseoll/Data_Center/blob/main/Screenshot_5.jpg)

