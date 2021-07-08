+++
title = "AWS + Tigera partnership"
chapter = true
weight = 8
+++

## AWS + Tigera partnership

AWS and Tigera provide DevOps, SREs and Platform owners to get Kubernetes-native networking, security and observability out of the box for EKS and AWS self-managed Kubernetes environments for their cloud-native applications. Users can leverage AWS services to build their applications while addressing their networking and security needs with Calico.

Calico also supports [Bottlerocket](https://aws.amazon.com/bottlerocket/) on [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS). Bottlerocket is an open source Linux distribution built by Amazon to run containers focused on security, operations, and manageability at scale. It is among the first EKS-optimized operating systems to support eBPF functionality in the Linux kernel. Calico can build on top of this foundation to enhance the base networking for EKS beyond just adding network policy support to including accelerating network performance, removing the need to run kube-proxy, and preserving client source IP addresses when accessing Kubernetes Services from outside the cluster.
