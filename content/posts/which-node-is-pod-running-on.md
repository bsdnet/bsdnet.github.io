---
title: "Which Node Is Pod Running On"
date: 2023-05-21T08:05:52-07:00
draft: true
---
= Objective

To understand which node your pod is running on.

= Overviews

Various applications exist in a Kubernetes clusters: Linux system
daemons, Kubernetes components, Kubernetes Addons and various Kubernetes workloads.

To bind applications to a Kubernete nodes, there are two ways:

*  Static
*  Dynamic


== Static 

Critical Linux system daemons like systemd, chrony, network manager, kubelet are required to run on each node as standalone programs. Kubernetes control plane components are hosted in [static pods](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/), which are managed directly by the kubelet daemon without the API server observing them.

To make system daemons or static pods run on each node is to preload or install them into OS image before creating a node instance. The preloading usually happensstaticaly before the cluster is formed.
![Kubernetes Node Daemons](/images/kubernetes-system-applications.png)

