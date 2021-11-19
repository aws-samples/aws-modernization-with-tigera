---
title: "8. Create EKS Cluster"
chapter: true
weight: 20
---

# Create EKS Cluster

In this section, we will be creating our EKS manifest file and deploying our cluster with eksctl. 

## Create EKS manifest.

If you want to use SSH key created in the previous step, uncomment the lines under the `ssh` section.

```bash
# create EKS manifest file
cat > configs/tigera-workshop.yaml << EOF
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
  metadata:
    name: "tigera-workshop"
    region: "${AWS_REGION}"
    version: "${EKS_VERSION}"

  availabilityZones: ["${AZS[0]}", "${AZS[1]}", "${AZS[2]}"]
  
  managedNodeGroups:
  - name: "nix-t3-large"
    desiredCapacity: 3
    # choose proper size for worker node instance as the node size detemines the number of pods that a node can run
    # it's limited by a max number of interfeces and private IPs per interface
    # t3.large has max 3 interfaces and allows up to 12 IPs per interface, therefore can run up to 36 pods per node
    # see: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html#AvailableIpPerENI
    instanceType: "t3.large"
    ssh:
      # uncomment the lines below to allow SSH access to the nodes using existing EC2 key pair
      # publicKeyName: ${KEYPAIR_NAME}
      # allow: true

  # enable all of the control plane logs:
  cloudWatch:
    clusterLogging:
      enableTypes: ["*"]
  EOF
```

7. Use `eksctl` to create EKS cluster.

    ```bash
    eksctl create cluster -f configs/tigera-workshop.yaml
    ```

8. View EKS cluster.

    Once cluster is created you can list it using `eksctl`.

    ```bash
    eksctl get cluster tigera-workshop
    ```

9. Test access to EKS cluster with `kubectl`

    Once the EKS cluster is provisioned with `eksctl` tool, the `kubeconfig` file would be placed into `~/.kube/config` path. The `kubectl` CLI looks for `kubeconfig` at `~/.kube/config` path or into `KUBECONFIG` env var.

    ```bash
    # verify kubeconfig file path
    ls ~/.kube/config
    # test cluster connection
    kubectl get nodes
    ```