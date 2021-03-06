# Выполнение работы
## Подготовка:
Были выполненны подготовительные работы и запущен vagrant файл:

![](pictures/p_01.png)

## Выполнение:
### на роутере r1:
Последовательное выполнение комманд:
```bash
sudo vtysh                    # вход в quagga
configure terminal            # вход режим глобальной конфигурации
router ospf                   # вход в режим настройки роутера
router-id  10.0.0.1           # присвоение id роутеру
passive-interface default     # выключение машрута по умолчанию
network 172.16.0.0/24 area 0  # присвоение area 0 сети 172.16.0.0/24
no passive-interface eth1     # включение интерфеса eth1
default-information originate # включение распространения маршрута по умолчанию
exit                          # выход в глобальной конфигурации
exit                          # выход в основной режим
copy running-config startup-config # сохранение новой конфигурации
exit                          # выход в консоль
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE  # включение маскарада на интерфейсе eth1
```
#### Проверки r1:
* пинг интернета:

![](pictures/p_02.png)

* пинг 192.168.1.2:

![](pictures/p_03.png)

* таблица маршрутизации:

![](pictures/p_04.png)

* соседи:

![](pictures/p_05.png)

### на роутере r2:
Последовательное выполнение комманд:
```bash
sudo vtysh                    # вход в quagga
configure terminal            # вход режим глобальной конфигурации
router ospf                   # вход в режим настройки роутера
router-id  10.0.0.2           # присвоение id роутеру
passive-interface default     # выключение машрута по умолчанию
no passive-interface eth1     # включение интерфеса eth1
network 172.16.0.0/24 area 0  # присвоение area 0 сети 172.16.0.0/24
no passive-interface eth2     # включение интерфеса eth2
network 172.16.1.0/24 area 1  # присвоение area 1 сети 172.16.1.0/24
no passive-interface eth3     # включение интерфеса eth3
network 172.31.0.0/24 area 0  # присвоение area 0 сети 172.31.0.0/24
exit                          # выход в глобальной конфигурации
exit                          # выход в основной режим
copy running-config startup-config # сохранение новой конфигурации
```

#### Проверки:
* пинг интернета:

![](pictures/p_06.png)

* пинг 192.168.1.2:

![](pictures/p_07.png)

* таблица маршрутизации:

![](pictures/p_08.png)

* соседи:

![](pictures/p_09.png)

### на роутере r3:
Последовательное выполнение комманд:
```bash
sudo vtysh                     # вход в quagga
configure terminal             # вход режим глобальной конфигурации
router ospf                    # вход в режим настройки роутера
router-id  10.0.0.3            # присвоение id роутеру
passive-interface default      # выключение машрута по умолчанию
no passive-interface eth1      # включение интерфеса eth1
network 172.16.0.0/24 area 0   # присвоение area 0 сети 172.16.0.0/24
no passive-interface eth2      # включение интерфеса eth2
network 192.168.0.0/24 area 0  # присвоение area 1 сети 192.168.0.0/24
no passive-interface eth3      # включение интерфеса eth3
network 172.31.0.0/24 area 0   # присвоение area 0 сети 172.31.0.0/24
exit                           # выход в глобальной конфигурации
exit                           # выход в основной режим
copy running-config startup-config # сохранение новой конфигурации
```
#### Проверки r3:
* пинг интернета:

![](pictures/p_10.png)

* пинг 192.168.1.2:

![](pictures/p_11.png)

* таблица маршрутизации:

![](pictures/p_12.png)

* соседи:

![](pictures/p_13.png)


### на роутере r4:
Последовательное выполнение комманд:
```bash
sudo su
vtysh                              # вход в quagga
configure terminal                 # вход режим глобальной конфигурации
router ospf                        # вход в режим настройки роутера
router-id  10.0.0.4                # присвоение id роутеру
passive-interface default          # выключение машрута по умолчанию
no passive-interface eth1          # включение интерфеса eth1
network 172.16.1.0/24 area 1       # присвоение area 0 сети 172.16.1.0/24
no passive-interface eth2          # включение интерфеса eth2
network 192.168.1.0/24 area 1      # присвоение area 1 сети 192.168.1.0/24
exit                               # выход в глобальной конфигурации
exit                               # выход в основной режим
copy running-config startup-config # сохранение новой конфигурации
```
#### проверки
* пинг интернета:

![](pictures/p_14.png)

* пинг 192.168.0.2:

![](pictures/p_15.png)

* таблица маршрутизации:

![](pictures/p_16.png)

* соседи:

![](pictures/p_17.png)
