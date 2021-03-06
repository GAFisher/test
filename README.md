# VLAN и маршрутизация между VLAN
## Задание:
1. Создать сеть и настроить основные параметры устройств.
2. Создать сети VLAN и назначить порты коммутаторов.
3. Настроить транк 802.1Q между коммутаторами.
4. Настроить маршрутизацию между сетями VLAN.
5. Проверить, что маршрутизация между VLAN работает.
## Решение:
1. Создание сети и настройка основных параметров устройства  
- Произведем базовую настройку маршрутизатора
- Произведем базовую настройку коммутаторов
- Настроим ПК
2. Создание сетей VLAN и назначение портов коммутатора
-	Создадим сети VLAN на коммутаторах	
-	Настроим интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации

**Топология**

**Таблица адресации**


## 1. Создание сети и настройка основных параметров устройства
**Произведем базовую настройку маршрутизатора** 

```Router>enable
Router#configure terminal
Router(config)#hostname R1
R1(config)#no ip domain-lookup 
R1(config)#enable secret class
R1(config)#line console 0
R1(config-line)#password cisco
R1(config-line)#login 
R1(config-line)#exit
R1(config)#line vty 0 4
R1(config-line)#password cisco
R1(config-line)#login         
R1(config-line)#exit          
R1(config)#service password-encryption 
R1(config)#banner motd #Authorized Access Only!#
R1(config)#end
R1#copy running-config startup-config
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#clock set 14:18:00 6 march 2021
R1#
```

**Произведем базовую настройку коммутаторов** 

```Switch>enable 
Switch#configure terminal 
Switch(config)#hostname S1
S1(config)#no ip domain-lookup 
S1(config)#enable secret class
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#line vty 0 4
S1(config-line)#password cisco
S1(config-line)#login         
S1(config-line)#exit          
S1(config)#service password-encryption
S1(config)#banner motd #Authorized Access Only!#
S1(config)#end
S1#clock set 14:21:00 6 march 2021
S1#copy running-config startup-config
Destination filename [startup-config]? 
Building configuration...
Compressed configuration from 992 bytes to 724 bytes[OK]
S1#
```
```Switch>enable
Switch#configure terminal 
Switch(config)#hostname S2
S2(config)#no ip domain-lookup 
S2(config)#enable secret class
S2(config)#line console 0
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
S2(config)#line vty 0 4
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
S2(config)#service password-encryption
S2(config)#banner motd #Authorized Access Only!#
S2(config)#end
S2#clock set 14:23:00 6 march 2021
S2#copy running-config startup-config
Destination filename [startup-config]? 
Building configuration...
Compressed configuration from 992 bytes to 723 bytes[OK]
S2#
```
**Настроим ПК**
```VPCS> set pcname PC-A

PC-A> ip 192.168.3.3 255.255.255.0 192.168.3.1
Checking for duplicate address...
PC1 : 192.168.3.3 255.255.255.0 gateway 192.168.3.1

PC-A> save
Saving startup configuration to startup.vpc
.  done

PC-A> 
```

```VPCS> set pcname PC-B

PC-B> ip 192.168.4.3 255.255.255.0 192.168.4.1
Checking for duplicate address...
PC1 : 192.168.4.3 255.255.255.0 gateway 192.168.4.1

PC-B> save
Saving startup configuration to startup.vpc
.  done

PC-B>
```
## 2. Создание сетей VLAN и назначение портов коммутатора
**Создадим сети VLAN на коммутаторах**
```S1#configure terminal 
S1(config)#vlan 3
S1(config-vlan)#name Management
S1(config-vlan)#vlan 4
S1(config-vlan)#name Operations
S1(config-vlan)#vlan 7
S1(config-vlan)#name ParkingLot
S1(config-vlan)#vlan 8
S1(config-vlan)#name Native
S1(config-vlan)#exit
S1(config)#
```
```S2#configure terminal 
S2(config)#vlan 3
S2(config-vlan)#name Management
S2(config-vlan)#vlan 4
S2(config-vlan)#name Operations
S2(config-vlan)#vlan 7
S2(config-vlan)#name ParkingLot
S2(config-vlan)#vlan 8
S2(config-vlan)#name Native
S2(config-vlan)#exit
S2(config)#
```
**Настроим интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации**
```S1(config)#interface vlan 3
S1(config-if)#ip address 192.168.3.11 255.255.255.0
S1(config-if)#no shutdown 
S1(config-if)#exit
S1(config)#ip default-gateway 192.168.3.1
S1(config)#
```
```S2(config)#interface vlan 3
S2(config-if)#ip address 192.168.3.12 255.255.255.0
S2(config-if)#no shutdown 
S2(config-if)#exit
S2(config)#ip default-gateway 192.168.3.1
S2(config)#
```
