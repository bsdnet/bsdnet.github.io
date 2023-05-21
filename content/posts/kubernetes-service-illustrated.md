---
title: "Kubernetes Service Illustrated"
date: 2023-05-13T14:17:22-07:00
draft: false 
---

# Objective

To understand the [Service](https://kubernetes.io/docs/concepts/services-networking/service/) concept in [Kubernetes](https://kubernetes.io/).

# Concepts

The following concepts are critical to understand the Service API in Kubernetes.

## Service
[Service](https://kubernetes.io/docs/concepts/services-networking/service/#services-in-kubernetes) is an abstraction to expose groups of [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) over a newtwork. Pods are selected via [Labels and Selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/). Each Service object defines a logic set of [Endpoints](https://kubernetes.io/docs/reference/kubernetes-api/service-resources/endpoints-v1/) or [EndpointSlice](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/) by Kubernetes control plane automatically.

There are 4 [Services types](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types): ClusterIP, NodePort, LoadBalancer and ExternalName. Refer [this article](https://nigelpoulton.com/explained-kubernetes-service-ports/) for illustration.

## ClusterIP

CluterIP is the default Service type and exposes the Service within the cluster ONLY. The [IP address](https://kubernetes.io/docs/concepts/services-networking/cluster-ip-allocation/) can be statically or dynamically chosen from `service-cluster-ip-range` configured for the Kubernetes API server.

Key fields in the specification is: `type`, `selector`, `clusterIP`, `port`, `protocol`, `targetPort`.

![Kubernetes Service ClusterIP](/images/kubernetes-service-clusterip.png)

## NodePort

[NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) exposes the Service externally on each Node's IP at a static port so that the Service is accessible via each
Node's IP and `nodePort` outside of the Kubernete cluster. Kubernetes control plane allocates a port from a range specified by `--service-node-port-range`.

Key fields in the specification is: `type`, `selector`, `port`, `targetPort`, and `nodePort`.

![Kubernetes Service NodePort](/images/kubernetes-service-nodeport.png)

## LoadBalancer

[LoadBalancer](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer) exposes the Service externally using a load blancer, which directs traffic from a `loadBalancerIP` to `clusterIP`.

Key fields in the specification is: `type`, `clusterIP`, `selector`, `protocol`, `port` and `targetPort`

![Kubernetes Service LoadBalancer](/images/kubernetes-service-loadbalancer.png)

## ExternalName

[ExternalName](https://kubernetes.io/docs/concepts/services-networking/service/#externalname) maps the Service to the DNS name specified by `externalName` field, not a typical seletor such as `cassandra`.

Key fields in the specification is: `type` and `externalName`.

![Kubernetes Service ExternalName](/images/kubernetes-service-externalname.png)

## Ports

Port definition is critical to understand the Service.
`containerPort` or `name` in `Pod` spec is the port the application in the pod actively listens. `targetPort` in `Service` spec
corresponds to `containerPort` in the Pod spec. `port` in `Sevice` spec is the port used by either internal Pod or external services, while `nodePort` is the port on each Node to access the service.

## Service, Load Balancer, Ingress

[Service](https://github.com/kubernetes/kubernetes/blob/master/pkg/apis/core/types.go#L3999) is the main approach to [expose applications running either within or outside of the cluster](https://kubernetes.io/docs/tutorials/services/connect-applications-service/).
Service can be exposed by LoadBalancer by [creating an external Load Balancer](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/) such as F5. While [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) is one way to manage external access to the Service in a Kubernete cluster via HTTP or HTTPS protocol.
 

# Reference
*  [Explained: Kubernete Service Ports](https://nigelpoulton.com/explained-kubernetes-service-ports/)
*  [Service](https://kubernetes.io/docs/concepts/services-networking/service/) 
