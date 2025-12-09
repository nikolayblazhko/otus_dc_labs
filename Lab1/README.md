# Проектирование адресного пространства
# Цель:
* Собрать схему CLOS;
* Распределить адресное пространство.

# Описание/Пошаговая инструкция выполнения домашнего задания:
1. Собрать топологию CLOS, как на схеме:

   ![Схема]net_map.jpg
2. Распределите адресное пространство для Underlay сети


#Выполнение:

# Таблица адресации:

| Device   | Interface   | IP address   | Description          |
|:---------|:------------|:-------------|:---------------------|
| Spine 1  | Loopback1   | 10.1.1.0/32  | Loopback1 (Underlay) |
|          | Loopback2   | 10.1.11.0/32 | Loopback2 (VTEP)     |
|          | Eth1        | 10.1.1.2/31  | to leaf1 (P2P)       |
|          | Eth2        | 10.1.1.4/31  | to leaf2 (P2P)       |
|          | Eth3        | 10.1.1.6/31  | to leaf3 (P2P)       |
|          |             |              |                      |
| Spine 2  | Loopback1   | 10.1.2.0/32  | Loopback1 (Underlay) |
|          | Loopback2   | 10.1.22.0/32 | Loopback2 (VTEP)     |
|          | Eth1        | 10.1.2.2/31  | to leaf1 (P2P)       |
|          | Eth2        | 10.1.2.4/31  | to leaf2 (P2P)       |
|          | Eth3        | 10.1.2.6/31  | to leaf3 (P2P)       |
|          |             |              |                      |
| Leaf1    | Loopback1   | 10.1.3.0/32  | Loopback1 (Underlay) |
|          | Loopback2   | 10.1.12.0/32 | Loopback2 (VTEP)     |
|          | Eth1        | 10.1.1.3/31  | to spine1 (P2P)      |
|          | Eth2        | 10.1.2.3/31  | to spine2 (P2P)      |
|          |             |              |                      |
| Leaf2    | Loopback1   | 10.1.4.0/32  | Loopback1 (Underlay) |
|          | Loopback2   | 10.1.13.0/32 | Loopback2 (VTEP)     |
|          | Eth1        | 10.1.1.5/31  | to spine1 (P2P)      |
|          | Eth2        | 10.1.2.5/31  | to spine2 (P2P)      |
|          |             |              |                      |
| Leaf3    | Loopback1   | 10.1.5.0/32  | Loopback1 (Underlay) |
|          | Loopback2   | 10.1.14.0/32 | Loopback2 (VTEP)     |
|          | Eth1        | 10.1.1.7/31  | to spine1 (P2P)      |
|          | Eth2        | 10.1.2.7/31  | to spine2 (P2P)      |

