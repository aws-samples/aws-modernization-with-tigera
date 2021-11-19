+++
title = "Common problems"
chapter = true
weight = 3
+++

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
  - eBPF is a Linux kernel feature that allows fast yet safe mini-programs to be loaded into the kernel in order to customize its operation. Calico’s eBPF dataplane is an alternative to our standard Linux dataplane (which is iptables based). While the standard dataplane focuses on compatibility by inter-working with kube-proxy, and your own iptables rules, the eBPF dataplane focuses on performance, latency and improving user experience with features that aren’t possible in the standard dataplane. As part of that, the eBPF dataplane replaces kube-proxy with an eBPF implementation. The main “user experience” feature is to preserve the source IP of traffic from outside the cluster when traffic hits a NodePort; this makes your server-side logs and network policy much more useful on that path.
