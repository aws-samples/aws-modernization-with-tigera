---
title: "Join EKS cluster to Calico Cloud"
chapter: false
weight: 25
---

## Join EKS cluster to Calico Cloud

>In order to complete this module, you must sign up for a free [Calico Cloud trial account](https://www.calicocloud.io).

### Steps to join cluster

{{% notice warning %}}
Make sure to get your [Calico Cloud trial account](https://www.calicocloud.io) before proceeding.
{{% /notice %}}

1. Join EKS cluster to Calico Cloud management plane.

    ![join EKS cluster](../images/join-eks-cluster.png)

    Use Calico Cloud install script provided in the `Connect Cluster` wizard.

    ```bash
    # script would look similar to this
    curl https://installer.calicocloud.io/xxxxxx_yyyyyyy-saay-management_install.sh | bash
    ```

    >Joining the cluster to Calico Cloud can take a few minutes. Wait for the installation script to finish before you proceed to the next step.

    The script will produce output similar to this:

    ```text
    [INFO] Checking for installed CNI Plugin
    [INFO] Deploying CRDs and Tigera Operator
    [INFO] Creating Tigera Pull Secret
    [INFO] Tigera Operator is Available
    [INFO] Adding Installation CR for Enterprise install
    [WAIT] Tigera calico is Progressing
    [INFO] Tigera Calico is Available
    [INFO] Deploying Tigera Prometheus Operator
    podmonitors.monitoring.coreos.com
    [INFO] Deploying APIServer CRs for Managed Cluster
    [INFO] Deploying LogCollector CRs for Managed Cluster
    [INFO] Tigera Apiserver is Available
    [INFO] Generate New Cluster Registration Manifest
    [INFO] Creating connection
    [INFO] All Tigera Components are Available
    [INFO] Securing Install

    Install Successful
    Your Connected Cluster Name is  xxxxxxxx-management-managed-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-gr7-us-east-1-eks-amazonaws-com
    ```

    >Note the management plane URL and any credentials that you see in the output as we will use them in the following modules.

2. Configure log aggregation and flush intervals.

    ```bash
    kubectl patch felixconfiguration.p default -p '{"spec":{"flowLogsFlushInterval":"10s"}}'
    kubectl patch felixconfiguration.p default -p '{"spec":{"dnsLogsFlushInterval":"10s"}}'
    kubectl patch felixconfiguration.p default -p '{"spec":{"flowLogsFileAggregationKindForAllowed":1}}'
    ```

3. Enable Felix component Policy Sync API.

    >[Felix](https://docs.tigera.io/reference/architecture/overview#felix) is one of Calico components that is responsible for configuring routes, ACLs, and anything else required on the host to provide desired connectivity for the endpoints on that host.

    ```bash
    kubectl patch felixconfiguration default --type='merge' -p '{"spec":{"policySyncPathPrefix":"/var/run/nodeagent"}}'
    ```

You have now completed all the steps necessary to implement the workshop use cases using your Cloud9 workspace.
