+++
title = "Introduction"
chapter = true
weight = 2
+++
# Introduction to Tigera and Calico

Tigera is the industry leader in Kubernetes security and observability, and is also the inventor and maintainer of open-source Calico. Its newest offering, Calico Cloud, is a next-generation, Kubernetes-native cloud service that extends the declarative nature of Kubernetes to specify "security and observability as code," which ensures consistent enforcement of security policies and compliance, and provides observability and troubleshooting across multi-cluster, multi-cloud, and hybrid deployments.

## Most common problems that Calico helps to solve

Calico capabilities range from providing a pluggable and reliable networking layer that "just works", to securing ingress and egress for Kubernetes applications and services, to using full spectrum of Calico security capabilities to implement and enforce zero-trust security for your Kubernetes environments.  

Here are a few of the most common Calico capabilities used by Calico users:

- Implement Egress Access Controls
  - Establishing service to service connectivity within your Amazon EKS cluster is easy. But how do you enable some of your workloads to securely connect to services like Amazon RDS, ElasticCache, etc. that are external to the cluster.
  - With Calico, you can author DNS Policies that implement fine-grained access controls between a workload and the external services it needs to connect to.
- Troubleshoot Microservice Connectivity
  - Troubleshooting microservice connectivity issues can be incredibly difficult due to the dynamic nature of container orchestration in Amazon EKS. Connectivity issues can be related to network performance, but often are the result of your Network Policies not being defined properly.
  - With Calico, you can explore a visual representation of all your microservices communicating with each other, and filter by connections that were accepted and denied. You can further drill into an individual denied connection to see which Network Policy evaluated and denied the connection, and then fix the policy to resolve the connectivity issue.
- Implement Enterprise Security Controls
  - Many applications have compliance requirements such as workload isolation, ensuring dev cannot talk to prod or implementing network zones (e.g. DMZ can communicate with the public internet but not your backend databases). While you can implement these rules using open-source Project Calico, there are a few limitations:
    - It is possible for other users to inadvertently override or intentionally tamper with your security controls, and very difficult to detect when that happens.
    - Proof that the policies have been enforced now and in the past is not possible.
  - With Calico, you can implement Security Controls at a higher precedent policy tier that cannot be overridden by other users. You will also learn how to provide audit reports that demonstrate compliance now and historically, as well as audit (or alert on) changes to policies.
- Pluggable networking data plane that give you the freedom to choose the most suitable networking layer for your Kubernetes environment. You can choose between standard Linux networking, i.e. IPTables/IPSets, eBPF, and VPP. The pluggable design of Calico's networking layer allows you to future proof your Kubernetes environment should any new networking technology arise.
  - eBPF is a Linux kernel feature that allows fast yet safe mini-programs to be loaded into the kernel in order to customise its operation. Calico’s eBPF dataplane is an alternative to our standard Linux dataplane (which is iptables based). While the standard dataplane focuses on compatibility by inter-working with kube-proxy, and your own iptables rules, the eBPF dataplane focuses on performance, latency and improving user experience with features that aren’t possible in the standard dataplane. As part of that, the eBPF dataplane replaces kube-proxy with an eBPF implementation. The main “user experience” feature is to preserve the source IP of traffic from outside the cluster when traffic hits a NodePort; this makes your server-side logs and network policy much more useful on that path.

## AWS + Tigera partnership

AWS and Tigera provide DevOps, SREs and Platform owners to get Kubernetes-native networking, security and observability out of the box for EKS and AWS self-managed Kubernetes environments for their cloud-native applications. Users can leverage AWS services to build their applications while addressing their networking and security needs with Calico.

Calico also supports [Bottlerocket](https://aws.amazon.com/bottlerocket/) on [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS). Bottlerocket is an open source Linux distribution built by Amazon to run containers focused on security, operations, and manageability at scale. It is among the first EKS-optimized operating systems to support eBPF functionality in the Linux kernel. Calico can build on top of this foundation to enhance the base networking for EKS beyond just adding network policy support to including accelerating network performance, removing the need to run kube-proxy, and preserving client source IP addresses when accessing Kubernetes Services from outside the cluster.

## Use cases that you will implement in this workshop

In this workshop we are going to focus on these main use cases:

In this workshop we are going to focus on these main use cases:

- **East-West security**, leveraging zero-trust security approach to implement safeguards within Kubernetes environment against malware and other malicious activities
- **Egress access controls**, using DNS policy to access external resources by their fully qualified domain names (FQDN) to prevent unauthorized access to the application
- **Host micro-segmentation**, leveraging Calico policies to protect host ports and host based services for a multi-tenant environment
- **Observability**, exploring various logs and application level metrics collected by Calico through for live visualization of communication between different components in Kubernetes environment.
- **Security alerts**, leveraging Calico global alerting framework to notify security and operations teams of any security incidents or anomalous behaviors.
- **Dynamic packet capture**, collecting full payload of the flows on demand for further forensic analysis.
- **Compliance**, providing proof of security compliance to meet organizational regulatory requirements

## Summary

You will come away from this workshop with an understanding of how others in your industry are doing Kubernetes security and observability in AWS EKS, and with best practices that you can implement in your own organization.

### Join the Slack Channel

[Calico User Group Slack](https://slack.projectcalico.org/) is a great resource to ask any questions about Calico. If you are not a part of this Slack group yet, we highly recommend [joining it](https://slack.projectcalico.org/) to participate in discussions or ask questions. For example, you can ask questions specific to EKS and other managed Kubernetes services in the `#eks-aks-gke-iks` channel.
