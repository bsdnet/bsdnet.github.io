---
title: "Kubernetes Cluster Illustrated"
date: 2023-05-20T13:36:28-08:00
categories: kubernetes
draft: fasle 
---

## Objective

To illustrate kubernetes cluster architecture and understand critical Kubernetes components.

## Cluster Architecture

![Kubernetes Cluster Architecture](/images/kubernetes-cluster-architecture.png)

## Control Plane Components 

Control Plane components run on one or mulptile control plane nodes.

### kube-apiserver

[kube-apiserver](https://github.com/kubernetes/apiserver) implements the Kubernetes API, and is designed to scale horizontally.

kube-apiserver runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/) or systemd daemon, configured using Pod specification or systemd unit and configuration file in /etc.

### etcd 

[etcd](https://etcd.io/docs/) is a consistent and highly-available key value store used for storing Kubernetes' cluster data.

etcd runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/) or systemd daemon, configured using Pod specification or systemd unit and configuration file in /etc.

### kube-scheduler

[kube-scheduler](https://github.com/kubernetes/kube-scheduler) watches for newly created Pods and selects a node for Pods to run on.

kube-scheduler runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/) or systemd daemon, configured using Pod specification or systemd unit and configuration file in /etc.

### kube-controller-manager

kube-controller-manager implements Node, Job, EndpointSlice and ServiceAccount controllers. 

kube-controller-manager runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/) or systemd daemon, configured using Pod specification or systemd unit and configuration file in /etc..

### cloud-controller-manager

[cloud-controller-manager](https://kubernetes.io/docs/concepts/architecture/cloud-controller/) implements cloud-specfic control logic.

cloud-controller-manager is optional. One example is [vSphee Cloud Controller Manager](https://github.com/kubernetes/cloud-provider-vsphere).

cloud-controller-manager runs as a static pod or systemd daemon, configured using Pod specification or systemd unit and configuration file in /etc.

## Node Components

Node Components run on every node including Control Plane nodes.

### kubelet

kubelet is the node agent that runs on each node, and make sure containers are running in a pod.

kubelet runs as a system daemon, configured using systemd unit and configuration file in /etc.

### kube-proxy

kube-proxy runs on each node as a network proxy that maintains network rules.

kube-proxy usually runs as a [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), configured using DaemonSet specification

### Container runtime

Container runtime such as [containerd](https://github.com/containerd/containerd), [CRI-O](https://github.com/cri-o/cri-o) is reponsible for running containers.

Containerd runs as a system daemon, configured using systemd unit and configuration file in /etc

## Kubernete Nodes 

A Kubernetes cluster consists of two kinds of nodes: control plane nodes and worker nodes.

Node can run on hardware, virtual platform like vSphere and KVM, cloud platform like Amazon AWS, MicrsoftAzure, Google GCP. Linux is the common Operating System running Kubernetes. Binaries and libraries are built on top of Linux Kernel, e.g Systemd, Kubelet, Containerd. Containerd/Runc is the most common container runtime. etcd, kube-apiserver, kube-scheduler, kube-control-manager, cloud-control-manager usually run as static pods on control plane nodes. kube-proxy runs as a daemonset. 

![Kubernetes Nodes](/images/kubernetes-node.png)
   
## References

* [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
