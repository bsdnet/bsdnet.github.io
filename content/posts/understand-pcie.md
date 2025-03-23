---
title: "Understand PCIe"
date: 2024-12-01T03:13:59Z
draft: false
---

## Objective
To understand PCI Express(PCIe) from the perspective of software engigneering.

## Concepts

### PCIe

PCIe, or peripheral component interconnect express, is an interface standard for
connecting high-speed I/O components such as GPUs, TPUs, RAID/HBA cards, Ethernet NICs
,  SSD add-on cards or WiFi cards.

PCIe is point to point serial connection.

### SerDes, Lanes,  Links and Slots.

Each PCIe lane utilizes two SerDes(Serializer/Deserializer)pairs, one for
transmitting and one for receiving data, resulting in a total of four physical
wires or signal traces.

PCIes slots come in different physical configurations: x1, x4, x8 and x16. The
number after x tells how many lanes that the PCIe slot has.

PCIe link is point to point communication channel between two PCIe devices.

PCIe is a packet based protocol.

### PCIe versions and transfer rates

The following is half Duplex speed table from Gen1 to Gen6.

| SPEC                | X1         | X2         | X4         | X8         | X16         |
| ------------------- | ---------- | ---------- | ---------- | ---------- | ----------- |
| PCIe 1.x (2.5 GT/s) | 250 MB/s   | 500 MB/s   | 1 GB/s     | 2 GB/s     | 4 GB/s      |
| PCIe 2.x (5.0 GT/s) | 500 MB/s   | 1 GB/s     | 2 GB/s     | 4 GB/s     | 8 GB/s      |
| PCIe 3.x (8.0 GT/s) | 984.6 MB/s | 1.97 GB/s  | 3.94 GB/s  | 7.88 GB/s  | 15.75 GB/s  |
| PCIe 4.x (16 GT/s)  | 1.97 GB/s  | 3.94 GB/s  | 7.88 GB/s  | 15.75 GB/s | 31.51 GB/s  |
| PCIe 5.x (32 GT/s)  | 3.94 GB/s  | 7.88 GB/s  | 15.75 GB/s | 31.51 GB/s | 63.02 GB/s  |
| PCIe 6.x (64 GT/s)  | 7.88 GB/s  | 15.75 GB/s | 31.51 GB/s | 63.02 GB/s | 126.03 GB/s |

PCIe 1.x and PCIe 2.x utilize 8b/10b encoding; With PCIe 3, the coding was
changed to
128b/130b encoding, which increased the effective data rate from around 80% to
more than 98%.

GT/s standas for Gigatransfers per second. Here is how to convert GT/s to Gbit/s, Gbps or Gigabits per
second.

One PCI 1.x lane can transfer 2.5GT/s * 8/10=2.0Gbps or 250MB/s. X16 means
4GB/s.

One PCI 5.x lane transfer 32GT/s * 128/132= 31.5Gbps or 3.938GB/s. X16 means
63.01GB/s.

Keep in mind, the above speed is half duplex. In networking, people always use
half duplex speed; while in PCIe world, people intends to use full duplex, which
is cofusing.

This article uses half duplex speed for the sake of simplicity.

## Reference
*  [Introduction to
PCIe and CXL](https://indico.cern.ch/event/1337180/contributions/5629298/attachments/2883776/5053368/Introduction%20to%20PCI%20Express.pdf)
*  [What is PCIe? Understanding PCIe Slots, Cards and Lanes](https://www.crystalrugged.com/knowledge/what-is-pcie-slots-cards-lanes/)
*  [PCI Express Wiki](https://en.wikipedia.org/wiki/PCI_Express)
*  [Pratical introduction to PCI Express with FPGAs](https://indico.cern.ch/event/121654/attachments/68430/98164/Practical_introduction_to_PCI_Express_with_FPGAs_-_Extended.pdf)
*  [PCI Express Tutorial](http://www.verien.com/pcie-primer.html)
*  [What is PCIE Express](https://www.synopsys.com/glossary/what-is-pci-express.html)
*  [Understanding PCIe Configuration for Maximum Performance](https://enterprise-support.nvidia.com/s/article/understanding-pcie-configuration-for-maximum-performance)
