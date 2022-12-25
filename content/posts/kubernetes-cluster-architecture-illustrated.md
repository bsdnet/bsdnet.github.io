---
title: "Kubernetes Cluster Architecture Illustrated"
date: 2022-12-25T13:36:28-08:00
draft: fasle 
---

# Objective

To illustrate kubernetes cluster architecture and understand critical Kubernetes components.

# Kubernetes Cluster Architecture

![Kubernetes Cluster Architecture](/images/kubernetes-cluster-architecture.png)

# Control Plane Components 

Control Plane components run on one or mulptile control plane nodes.

## kube-apiserver

[kube-apiserver](https://github.com/kubernetes/apiserver) implements the Kubernetes API, and is designed to scale horizontally.

kube-apiserver runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/).

## etcd 

[etcd](https://etcd.io/docs/) is a consistent and highly-available key value store used for storing Kubernetes' cluster data.

etcd runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/).

## kube-scheduler

[kube-scheduler](https://github.com/kubernetes/kube-scheduler) watches for newly created Pods and selects a node for Pods to run on.

kube-scheduler runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/).

## kube-controller-manager

kube-controller-manager implements Node, Job, EndpointSlice and ServiceAccount controllers. 

kube-controller-manager runs as a [static pod](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/).

## cloud-controller-manager

cloud-controller-manager implements cloud-specfic control logic.

cloud-controller-manager is optional.

# Node Components

Node Components run on every node including Control Plane nodes.

## kubelet

kubelet is the node agent that runs on each node, and make sure containers are running in a pod.

kubelet runs as a systemd service.

## kube-proxy

kube-proxy runs on each code as a network proxy that maintains network rules.

kube-proxy usually runs as a [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

## Container runtime

Container runtime such as [containerd](https://github.com/containerd/containerd), [CRI-O](https://github.com/cri-o/cri-o) is reponsible for running containers.

# References

* [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
