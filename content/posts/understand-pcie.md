---
title: "Understand PCIe"
date: 2024-12-01T03:13:59Z
draft: true
---

## Objective
To understand PCI Express(PCIe) from the perspective of software engigneering.

## Concepts

### PCIe

PCIe, or peripheral component interconnect express, is an interface standard for
connecting high-speed I/O components such as GPUs, RAID/HBA cards, Ethernet
cards, SSD add-on cards or WiFi cards.

PCIe is point to point serial connection.

### Slots, Links and Lanes.

PCIes slots come in different physical configurations: x1, x4, x8 and x16. The
number after x tells how many lanes that the PCIe slot has.

PCIe link is point to point communication channel between two PCIe devices.

PCIe is a packet based protocol.

### PCIe versions and transfer rates


## Reference
*  [Introduction to
PCIe and CXL](https://indico.cern.ch/event/1337180/contributions/5629298/attachments/2883776/5053368/Introduction%20to%20PCI%20Express.pdf)
*  [What is PCIe? Understanding PCIe Slots, Cards and Lanes](https://www.crystalrugged.com/knowledge/what-is-pcie-slots-cards-lanes/)
*  [PCI Express Wiki](https://en.wikipedia.org/wiki/PCI_Express)
*  [Pratical introduction to PCI Express with FPGAs](https://indico.cern.ch/event/121654/attachments/68430/98164/Practical_introduction_to_PCI_Express_with_FPGAs_-_Extended.pdf)
*  [PCI Express Tutorial](http://www.verien.com/pcie-primer.html)
*  [What is PCIE Express](https://www.synopsys.com/glossary/what-is-pci-express.html)
*  [Understanding PCIe Configuration for Maximum Performance](https://enterprise-support.nvidia.com/s/article/understanding-pcie-configuration-for-maximum-performance)
