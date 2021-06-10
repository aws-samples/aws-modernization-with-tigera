+++
title = "Calico workshop on EKS"
chapter = true
weight = 1
+++

# AWS Modernization with Calico
![Calico on EKS](/images/calico-on-eks.png)
### Welcome

[Project Calico](https://www.projectcalico.org/) is a network policy engine for Kubernetes. With Calico network policy enforcement, you can implement network segmentation and tenant isolation. This is useful in multi-tenant environments where you must isolate tenants from each other or when you want to create separate environments for development, staging, and production. Network policies are similar to AWS security groups in that you can create network ingress and egress rules. Instead of assigning instances to a security group, you assign network policies to pods using pod selectors and labels. The following procedure shows you how to install Calico on Linux nodes in your Amazon EKS cluster.

>To learn more about installing Calico on EKS Cluster, please click [here](https://docs.aws.amazon.com/eks/latest/userguide/calico.html).

