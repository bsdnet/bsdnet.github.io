---
title: "vSphere CSI Driver Illustrated"
date: 2022-12-25T16:15:26-08:00
draft: false
---

# Objective

To understand how vSphere CSI driver works and is being deployed in pratice.

# vSphere CSI Driver Architecture 
![vSphere CSI Driver Architecture](/images/vsphere-csi-driver-architecture.png)

# vSphere CSI Driver Deployment

vSphere CSI Driver is a Kubernetes Deployment that includes multiple containers and runs
on the control plane node.

## csi-snapshotter

csi-snapshotter is the sidecar container that watches for VolumeSnapshotContent
create/update/delete events. csi-snapshotter works with CSI snapshot controller
together implement CSI snapshot function.

See [Description](https://kubernetes-csi.github.io/docs/external-snapshotter.html#description)
and [Github](https://github.com/kubernetes-csi/external-snapshotter/tree/master/cmd/csi-snapshotter) for further details.

## csi-resizer
csi-resizer is a sidecar container that watches the Kubernetes API server for `PersistentVolumeClaim` updates
and triggers `ControllerExpandVolume` operation.

See [Description](https://kubernetes-csi.github.io/docs/external-resizer.html#description) and [Github](https://github.com/kubernetes-csi/external-resizer) for further details.

## csi-attacher
csi-attacher is a sidecar container that attaches volumes to nodes by calling `ControllerPublish` and `ControllerUnpublish` functions of CSI drivers. 

See [Description](https://kubernetes-csi.github.io/docs/external-attacher.html#description) and [Github](https://github.com/kubernetes-csi/external-attacher) for further details.

## csi-provisioner
csi-provisioner is a sidecar container that provisions volumes by calling `CreateVolume` and `DeleteVolume` functions of CSI drivers.
See [Description](https://kubernetes-csi.github.io/docs/external-provisioner.html#description) and [Github](https://github.com/kubernetes-csi/external-provisioner)
for further details.

## vsphere-syncer

vsphere-syncer is a container with vSphere CSI controller pod that responsible for pushing the PV, PVC and pod metadata to CNS.
See [Github](https://github.com/kubernetes-sigs/vsphere-csi-driver/blob/master/cmd/syncer/main.go) for further details.

## vsphere-csi-controller
vsphere-csi-controller is the container within vSphere CSI controller that is responsible for volume provisining, attaching and
detaching the volume to VMs, mounting, formatting and umounting volumes from the pod within the VM.

See [Github](https://github.com/kubernetes-sigs/vsphere-csi-driver) for further details.

# vSphere CSI Node DaemonSet

vSphere CSI Node is a Kubernetes DaemonSet running on each worker node.

## node-driver-registrar

node-driver-registrar is a sidecar container that registers the CSI driver within Kubelet using
the kubelet plugin registration machanism so that Kubelets can issue CSI `NodeGetInfo`, `NodeStageVolume`, `NodePublishVolume` calls.

See [Description](https://kubernetes-csi.github.io/docs/node-driver-registrar.html#description) and [Github](https://github.com/kubernetes-csi/node-driver-registrar) for further details.

## vsphere-csi-node

vsphere-csi-node is the container that is responsible for volume provisining, attaching and
detaching the volume to VMs, mounting, formatting and umounting volumes from the pod within the VM.

See [Github](https://github.com/kubernetes-sigs/vsphere-csi-driver/tree/master/cmd/vsphere-csi) for details.

# Snapshot controller

Snapshot controller is responsible for managing snapshot objects and operations
across multiple CSI drivers.

## snapshot-controller

See [Description](https://kubernetes-csi.github.io/docs/snapshot-controller.html#description)
and  [Github](https://github.com/kubernetes-csi/external-snapshotter/tree/master/cmd/snapshot-controller) for further details.

## snapshot-validation-webhook

See [Description](https://kubernetes-csi.github.io/docs/snapshot-validation-webhook.html#description) and [Githb](https://github.com/kubernetes-csi/external-snapshotter/tree/master/cmd/snapshot-validation-webhook) for further details.

# Reference
- [A Deep Dive into the Kubernetes vSphere CSI Driver with TKGI and TKG](https://tanzu.vmware.com/content/blog/a-deep-dive-into-the-kubernetes-vsphere-csi-driver-with-tkgi-and-tkg)
- [CSI driver for vSphere](https://github.com/kubernetes-sigs/vsphere-csi-driver)
- [vSphere CSI Documentation](https://docs.vmware.com/en/VMware-vSphere-Container-Storage-Plug-in/index.html)
- [Kubernetes CSI Documentation](https://kubernetes-csi.github.io/docs/)
- [Kubernetes CSI Projects](https://github.com/kubernetes-csi)
