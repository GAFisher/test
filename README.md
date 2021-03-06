# VLAN и маршрутизация между VLAN
## Задание:
1. Создать сеть и настроить основные параметры устройств.
2. Создать сети VLAN и назначить порты коммутаторов.
3. Настроить транк 802.1Q между коммутаторами.
4. Настроить маршрутизацию между сетями VLAN.
5. Проверить, что маршрутизация между VLAN работает.
## Решение:



**Топология**

**Таблица адресации**


# 1. Создание сети и настройка основных параметров устройства
**Произведем базовую настройку маршрутизатора** 

```Router>enable
Router#configure terminal
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

**Произведем базовую настройку коммутаторов.** 
**Настроим ПК.**
