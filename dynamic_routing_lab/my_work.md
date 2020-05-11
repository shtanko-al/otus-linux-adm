# Выплнение работы
## Подготовка:
Были выполненны подготовительные работы и запущен vagrant файл:

![](///pictures/p_01.png)
## Выполнение:
### на сервере r1:
Вход в quagga и присвоение id интерфейсу:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_02.png)

Назначение area 0 сети 10.0.0.1/32

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_03.png)

Назначение area 0 сетям 172.16.1.0/24 и 172.16.2.0/24:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_4.png)

Включение интерфейсов eth1 и eth2 и сохранение конфигурации:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_05.png)

### на сервере r2:
Вход в quagga и присвоение id интерфейсу:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_06.png)

Выключение интерфейса по умолчанию, назначение area сетям и сохранение конфигурации:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_07.png)

Забыл включить интерфесы eth1 и eth2. Включаю и сохраняю конфигурацию:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_08.png)

### на сервере r3:
На сервере r3, по аналогии с предыдущим, надо выполнить следующие комманды:
```bash
sudo vtysh
configure terminal
router ospf
ospf router-id 10.0.0.3
passive-interface default
no passive-interface eth1
no passive-interface eth2
network 10.0.0.3/32 area 0.0.0.0
network 172.16.2.0/24 area 0.0.0.0
network 172.16.3.0/24 area 0.0.0.0
exit
exit
copy running-config startup-config
```
проверка сохраненной конфигурации:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_09.png)

### на сервере r1:
распространение маршрута по умолчанию:
```default-information originate```

Включение маскарада
```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE```

### на сервере r2:
Проверка таблиц маршрутизации и выхода во внешнюю сеть:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_10.png)

### на сервере r3:
Проверка таблиц маршрутизации и выхода во внешнюю сеть:

![](https://github.com/shtanko-al/otus-linux-adm/blob/master/dynamic_routing_lab/pictures/p_11.png)
