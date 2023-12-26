---
title: "Kubernetes Control Plane HA Implementation"
date: 2023-12-25T21:41:59-08:00
draft: false
---

## Objective

To understand how Kubernetes HA is implemented, especially the [stacked etcd topology](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/#stacked-etcd-topology).

# Kubernetes Control Plane HA Architecture

![Kubernetes Control Plane HA Architecture](/images/kubernetes-cp-ha-implementation.png)

## Concepts

In addition to three control plane nodes, HAProxy and Keepalived are the key components to implement Highly Available Kubernetes Control Plane.

### HAProxy

Like [Nginx](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/), [HAProxy](https://www.haproxy.org/) is a popular open source TCP/HTTP Loadbalancer and Proxy solution.
HAProxy balance the traffic among Kubernetes Control Plane nodes via Control Plane VIP. However, if a single HAProxy instance is deployed, Kubernetes Control Plane will become unavailable once the HAProxy failed.
Multiple HAProxy instances are used to avoid the single point of failurei problem.

### Keepalived

When one HAProxy instance failed, the Control Plane VIP needs to float to the HAProxy instance that is up.
This is when [Keepalived](https://www.keepalived.org/) comes to rescue. Keepalived is actively monitoring the liveness of HAProxy at local node and chatting with its peers. Instead of using Keepalived,  [Kubernetes Under the Hood](https://github.com/mvallim/kubernetes-under-the-hood)uese the comibnation of [Corosync](https://corosync.github.io/corosync/) and [Pacemaker](https://clusterlabs.org/pacemaker/) as an alternative.

## Reference

*  [HAProxy/Keepalived Configuration](https://access.redhat.com/documentation/en-us/red_hat_ceph_storage/1.3/html/object_gateway_guide_for_red_hat_enterprise_linux/haproxy_keepalived_configuration)
*  [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)
*  [How To Create a High Availability Setup with Corosync, Pacemaker, and Reserved IPs on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-high-availability-setup-with-corosync-pacemaker-and-reserved-ips-on-ubuntu-14-04)
*  [Kubernetes High Availability Considerations](https://github.com/kubernetes/kubeadm/blob/main/docs/ha-considerations.md)
