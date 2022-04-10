---
title: "Kubernetes Container Stack"
date: 2022-04-09T18:51:57-07:00
draft: false
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

## apiserver

[apiserver](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/) sits on the Kubernetes master, validates and configures data for the api objects which include pods, services, replicationcontrollers and others. The API Server services REST operations and provides the cluster's shared state.

## kubelet

[kublet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/) is the primary node agent that runs on each Kubernetes node and register the node with the apiserver. kubelet manages pod using PodSpec in YAML or JSON format. kubelet implement the CRI client, and also have dockershim before Kubernete 1.24.

## CRI Container Runtime

A container runtime is software that executes containers and manage container images. [Container Runtime Interface(CRI)](https://kubernetes.io/docs/concepts/architecture/cri/) is a plugin interface which enables kubelet to use a wide variety of container runtimes without recompiling. CRI consists of a protocol buffers, gRPC API, and libraries. Popular contianer runtimes include [docker engine](https://docs.docker.com/engine/), [cri-o](https://cri-o.io/), [contaienrd](https://containerd.io/), and rktlet, frakti. dockershim in kubelet implements CRI interfaces; cri-o implements OCI conformant runtime; frakti is hypervisor-based container runtime while rktlet is the rkt contaienr runtime that is in frozen state.

containerd is an OCI compliant core container runtime and provides minimum set of functinoality to execute containers and manages images. Other than container lifecycle management and image management, [networking(CNI)](https://github.com/containernetworking/cni), [volume(CSI)](https://github.com/container-storage-interface/spec/blob/master/spec.md) and persistent logging are not the scope of containerd. Now the original cri-containerd elvoves into cri package in containerd, and containerd becomes the default runtime in Kubernetes.

The biggest change in Kubernetes 1.24 is dockershim removal from kubelet source code. To keep docker engine as a container runtime, cri-dockerd is invented to bridge the gap.


## OCI Runtime

Performance, security and compability results in multiple OCI compatible runtimes in Kubernetes Ecosystem.

[runc](https://github.com/opencontainers/runc) is the default OCI runtime in kubernetes that spawns and runs containers on Linux. While [crun](https://github.com/containers/crun) is a fast and low-memory footprint OCI Ctontainer Runtime fully written in C. [runsc](https://github.com/google/gvisor) in gVisor implement a sandbox mechanism by mapping system calls invoked in applications to less Linux system calls on the host kernel. [runnc](https://github.com/nabla-containers/runnc) in [Nabla Containers](https://nabla-containers.github.io/) achieve the same by using less Linux system calls. [kata-runtime](https://github.com/kata-containers/kata-containers/tree/main/src/runtime) is the OCI runtime in [Kata Containers](https://katacontainers.io/) that builds a standard implementation of lightweight Virtual Machines (VMs) that feel and perform like containers, but provide the workload isolation and security advantages of VMs. 
