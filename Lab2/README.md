# Построение Underlay сети(OSPF)
# Цель:
* Исследовать построение Underlay сети с использованием OSPF

# Описание/Пошаговая инструкция выполнения домашнего задания:
1. Настройка OSPF в Underlay сети, для IP связанности между всеми сетевыми устройствами.
2. Зафиксируете в документации - план работы, адресное пространство, схему сети, конфигурацию устройств
3. Убедитесь в наличии IP связанности между устройствами в OSFP домене


# Выполнение:

## Таблица адресации:


| Device  | Interface    | IP Address     | Description                |
|:--------|:-------------|:---------------|:---------------------------|
| Spine1  | Loopback0    | 10.0.0.1/32    | Underlay BGP Router-ID     |
|         | Loopback1    | 10.0.1.1/32    | VTEP        |
|         | Eth1  | 10.0.2.0/31    | P2P линк к Leaf1          |
|         | Eth2  | 10.0.2.2/31    | P2P линк к Leaf2          |
|         | Eth3  | 10.0.2.4/31    | P2P линк к Leaf3          |
|         |              |                |                            |
| Spine2  | Loopback0    | 10.0.0.2/32    | Underlay BGP Router-ID     |
|         | Loopback1    | 10.0.1.2/32    | VTEP       |
|         | Eth1  | 10.0.2.6/31    | P2P линк к Leaf1          |
|         | Eth2  | 10.0.2.8/31    | P2P линк к Leaf2          |
|         | Eth3  | 10.0.2.10/31   | P2P линк к Leaf3          |
|         |              |                |                            |
| Leaf1   | Loopback0    | 10.0.0.11/32   | Underlay BGP Router-ID     |
|         | Loopback1    | 10.0.1.11/32   | VTEP address  |
|         | Eth1  | 10.0.2.1/31    | P2P линк к Spine1         |
|         | Eth2  | 10.0.2.7/31    | P2P линк к Spine2         |
|         |              |                |                            |
| Leaf2   | Loopback0    | 10.0.0.12/32   | Underlay BGP Router-ID     |
|         | Loopback1    | 10.0.1.12/32   | VTEP address  |
|         | Eth1  | 10.0.2.3/31    | P2P линк к Spine1         |
|         | Eth2  | 10.0.2.9/31    | P2P линк к Spine2         |
|         |              |                |                            |
| Leaf3   | Loopback0    | 10.0.0.13/32   | Underlay BGP Router-ID     |
|         | Loopback1    | 10.0.1.13/32   | VTEP address   |
|         | Eth1  | 10.0.2.5/31    | P2P линк к Spine1         |
|         | Eth2  | 10.0.2.11/31   | P2P линк к Spine2         |




## Конфигурации устрайств(Также в формате файлов в папке проекта):

### Конфигурация Spine1:

```
! device: Spine1 (vEOS-lab, EOS-4.29.2F)
!
! boot system flash:/vEOS-lab.swi
!
no aaa root
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model ribd
!
hostname Spine1
!
spanning-tree mode mstp
!
interface Ethernet1
   description p2p-leaf1
   mtu 9214
   no switchport
   ip address 10.0.2.0/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet2
   description p2p-leaf2
   mtu 9214
   no switchport
   ip address 10.0.2.2/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet3
   description p2p-leaf3
   mtu 9214
   no switchport
   ip address 10.0.2.4/31
   ip ospf network point-to-point
   ip ospf area 0.0.0.0
!
interface Ethernet4
!
interface Ethernet5
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Loopback0
   description Router-ID
   ip address 10.0.0.1/32
!
interface Loopback1
   description VTEP
   ip address 10.0.1.1/32
!
interface Management1
!
ip routing
!
router ospf 1
   router-id 10.0.0.1
   max-lsa 12000
!
end

```