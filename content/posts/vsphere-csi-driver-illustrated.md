---
title: "vSphere CSI Driver Illustrated"
date: 2022-12-25T16:15:26-08:00
draft: true
---

# Objective

To understand how vSphere CSI driver works and is being deployed in pratice.

# vSphere CSI Driver Architecture 
![vSphere CSI Driver Architecture](/images/vsphere-csi-driver-architecture.png)

# vSphere CSI Driver Deployment
Multiple sidecar containers are in vSphere CSI Driver pod, which is a Kubernetes Deployment.

## csi-snapshotter
See [details](https://kubernetes-csi.github.io/docs/external-snapshotter.html#description)

## csi-resizer
See [details](https://kubernetes-csi.github.io/docs/external-resizer.html#description)

## csi-attacher
See [details](https://kubernetes-csi.github.io/docs/external-attacher.html#description)

## csi-provisioner
See [details](https://kubernetes-csi.github.io/docs/external-provisioner.html#description)

## vsphere-syncer

## vsphere-csi-controller

# vSphere CSI Node DaemonSet

## node-driver-registrar

See [details](https://kubernetes-csi.github.io/docs/node-driver-registrar.html#description)

## vsphere-csi-node

# Snapshot controller

Snapshot controller is responsible for managing snapshot objects and operations
across multiple CSI drivers.

## snapshot-controller

See [details](https://kubernetes-csi.github.io/docs/snapshot-controller.html#description)

## snapshot-validation-webhook

See [details](https://kubernetes-csi.github.io/docs/snapshot-validation-webhook.html#description)

# Reference
- [A Deep Dive into the Kubernetes vSphere CSI Driver with TKGI and TKG](https://tanzu.vmware.com/content/blog/a-deep-dive-into-the-kubernetes-vsphere-csi-driver-with-tkgi-and-tkg)
- [CSI driver for vSphere](https://github.com/kubernetes-sigs/vsphere-csi-driver)
- [vSphere CSI Documentation](https://docs.vmware.com/en/VMware-vSphere-Container-Storage-Plug-in/index.html)
- [Kubernetes CSI Documentation](https://kubernetes-csi.github.io/docs/)
- [Kubernetes CSI Projects](https://github.com/kubernetes-csi)
