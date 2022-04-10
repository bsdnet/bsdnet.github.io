---
title: "Kubernetes Container Stack"
date: 2022-04-09T18:51:57-07:00
draft: true
---

In Kubernetes 1.24, [dockershim](https://kubernetes.io/blog/2021/11/12/are-you-ready-for-dockershim-removal/) will be removed. What does it mean, let's take a look the container stackbefore and after dockershim removal. 


# Objective

To walkthrough container stack on a Kubernetes node.

# Before 1.24 release

![Kubernetes Container Stack Before 1.24](/images/kubernetes-container-stack-before-124.png)

# Since 1.24 release

![Kubernetes Container Stack Since 1.24](/images/kubernetes-container-stack-124.png)

# Walk-through

Using the opportunity, we can walkthrough the container stack and corresponding tooling on a Kubernetes node from top to bottom.

## kubectl and API server 

## kubelet

## CRI compatible Container  Runtime

## OCI Runtime

Performance, security and compability results in multiple OCI compatible runtimes in Kubernetes Ecosystem.

[runc](https://github.com/opencontainers/runc) is the default OCI runtime in kubernetes that spawns and runs containers on Linux. While [crun](https://github.com/containers/crun) is a fast and low-memory footprint OCI Ctontainer Runtime fully written in C. [runsc](https://github.com/google/gvisor) in gVisor implement a sandbox mechanism by mapping system calls invoked in applications to less Linux system calls on the host kernel. [runnc](https://github.com/nabla-containers/runnc) in [Nabla Containers](https://nabla-containers.github.io/) achieve the same by using less Linux system calls. [kata-runtime](https://github.com/kata-containers/kata-containers/tree/main/src/runtime) is the OCI runtime that enables lightweight virtual machines that feel and perform like standard Linux containers, which provides stronger workload isolation and security.
