+++
title = "Calico workshop on EKS"
chapter = true
weight = 1
+++

# AWS Modernization with Calico

![Calico on EKS](/images/calico-on-eks.png)

## Welcome

[Project Calico](https://www.projectcalico.org/) is a network policy engine for Kubernetes. With Calico network policy enforcement, you can implement network segmentation and tenant isolation. This is useful in multi-tenant environments where you must isolate tenants from each other or when you want to create separate environments for development, staging, and production. Network policies are similar to AWS security groups in that you can create network ingress and egress rules. Instead of assigning instances to a security group, you assign network policies to pods using pod selectors and labels. The following procedure shows you how to install Calico on Linux nodes in your Amazon EKS cluster.

## Learning objectives

During this workshop, we expect attendees to have hands-on experience with Kubernetes security and observability for EKS deployment. You will learn how to design, deploy, and observe security and networking policies in an EKS environment. This ~90-minute hands-on lab provides you with your own provisioned Calico Cloud environment which can be connected with your EKS cluster or AWS EC2 environment running self-managed Kubernetes environment to provide more complete knowledge on how to implement and use:

- Access controls
- DNS policy
- Dynamic Service Graph
- Compliance and reporting
- Observability and troubleshooting
- Alerting on security incidents
- Dynamic packet capture

## Intended audience

This workshop addresses the needs of DevOps, site reliability engineers (SREs), security and cloud architects by implementing Kubernetes-native networking, security and observability in AWS or EKS environments.

This workshop is intended to be **200-300** level. It is assumed that you are familiar with the following concepts:

- Kubernetes constructs at a base level
- Basic networking in Kubernetes
- Use of CNIs with AWS and EKS
- Kubernetes-native security policies and monitoring
- Kubernetes-native observability and troubleshooting

## Workshop flow

The workshop modules are structured to provide a natural flow helping to configure and solve various security, observability and troubleshooting use cases for your Kubernetes applications and services.

>Expected duration to complete the workshop is 90-120 mins.

### Module 1 - Deploy and configure demo applications

Deploy demo applications and enable Calico capabilities that you will use in later modules.

### Module 2 - Secure application and services using security controls

Leverage network policies to segment connections within Kubernetes cluster and prevent known bad actors from accessing the workloads.

### Module 3 - Secure outbound connections using egress controls

Configure egress access for specific applications and services.

### Module 4 - Secure Kubernetes hosts using host endpoint protection (HEP)

Secure EKS hosts ports with Calico network policies.

### Module 5 - Explore Calico observability and troubleshooting tools

Leverage Calico observability and troubleshooting tools to reduce mean time to repair (MTTR) for your Kubernetes applications and services.

### Module 6 - Generate compliance reports

Configure global reports to satisfy compliance requirements.

### Module 7 - Configure security alerts

Use global alerts to notify security and operations teams about unsanctioned or suspicious activity.

### Module 8 - Configure dynamic packet capture

Use dynamic package capture to collect full packet payload on demand.

{{% notice tip %}}
To learn more about installing Calico on EKS Cluster, please click [here](https://docs.aws.amazon.com/eks/latest/userguide/calico.html).
