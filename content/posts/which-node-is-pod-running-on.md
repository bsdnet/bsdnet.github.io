---
title: "Which Node Is Pod Running On"
date: 2023-05-21T08:05:52-07:00
draft: false
---
## Objective

To understand which Kubernetes [node](https://kubernetes.io/docs/concepts/architecture/nodes/) a [pod](https://kubernetes.io/docs/concepts/workloads/pods/) is running on.

## Overview

Various applications can be deployed in a Kubernetes cluster: Linux system
daemons, Kubernetes components, Kubernetes Addons and various Kubernetes workloads.

To bind applications to a Kubernete node, there are two ways:

*  Static Binding
*  Dynamic Scheduling

### Static Binding

Critical Linux system daemons such as [systemd](https://www.freedesktop.org/wiki/Software/systemd/), [chrony](https://chrony.tuxfamily.org/), [Network Manager](https://networkmanager.dev/), [kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/), [Container Runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/) are required to run on each node as standalone programs. Kubernetes control plane components are running in [static pods](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/), which are managed directly by the kubelet daemon using [manifest files](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/) under `/etc/kubernetes/manifests`. Static pod can not refer to other Kubernetes objects like Service Account, ConfigMap, Secret, etc, and do not support [ephemeral containers](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/).

To make system daemons or static pods run on a particular node is to preload or install them into OS image before creating a node instance. The preloading usually happens staticaly before the cluster is formed.

![Kubernetes System Applications](/images/kubernetes-system-applications.png)

### Dynamic Scheduling

The kube-scheduler dynamically schedules pods to a worker node by considering the pod's preferences specified in PodSpec and the node's [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/). Node labels can be attached manually or be well-known labels populated by kubelet.

### nodeSelector

`nodeSelector` is the simplest way to let Kubernetes know your node preference. Add the `nodeSelector` field to Pod specificiation and specify the node labels you want the target node to have.

![Kubernetes Application NodeSelector](/images/kubernetes-application-nodeselector.png)

### Node affinity

Node affinity is similar to `nodeSelector`, allowing Pod to be scheduled based on node labels. There are two types of node affinity: `requiredDuringSchedulingIgnoredDuringExecution` and `preferredDuringSchedulingIgnoredDuringExecution`. Node affinity can be specified using `.spec.affinity.nodeAffinity` field in Pod spec.

![Kubernetes Application NodeAffinity](/images/kubernetes-application-nodeaffinity.png)

### Inter-pod affinity and anti-affinity

Inter-pod affinity and anti-affinity allow to contrain which nodes Pods can be scheduled on based on the labels of Pods already running on the node, instead of the node labels. Two types of inter-node affinity and anti-affinity exist: `requiredDuringSchedulingIgnoredDuringExecution` and `preferredDuringSchedulingIgnoredDuringExecution`. `affinity.podAffinity` field is used for inter-pod affinity; while `affinity.podAntiAffinity` field is used for inter-pod anti-affinity.

![Kubernetes Application InterpodAffinity](/images/kubernetes-application-interpodaffinity.png)

See [Zookeeper tutorial](https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/#tolerating-node-failure) for an example of anti-affinity in practice!

### Taints and Tolerations

Node affinity attracts Pods to a set of nodes; while Taints allow a node to repel a set ofpods.  Taints are a special kind of key/value with taint effect that are applied to nodes.The node should not accept any pods that do not tolerate the taints. Toerations are applied to pods. Tolerations allow the scheduler to schedule pods with matching taints.

![Kubernetes Application Taints](/images/kubernetes-application-taints.png)

### nodeName

`nodeName` is a field in the Pod spec, and used to bypass Kubernetes scheduler. You can
specify the `nodeName` and overrules `nodeSelector` or affinity and anti-affinity rules.
`nodeName` has some limitations to select nodes, and may result to pod scheduling failure.

![Kubernetes Application NodeName](/images/kubernetes-application-nodename.png)

### Pod topology spread constaints

Topology spread constaints is used to control how pods are spread across cluster among failure-domains such as regions, zones, nodes.

## References
* [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)
* [Assign Pods to Nodes](https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/)
* [Viewing Poads and Nodes](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/)
* [Taints and Tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
* [Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)
