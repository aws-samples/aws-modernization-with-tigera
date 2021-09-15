---
title: "Create EKS cluster"
chapter: false
weight: 23
---

## Create EKS cluster

{{% notice warning %}}
For the instructor-led workshop at an AWS hosted event (such as *re:Invent, Kubecon, Immersion Day, Dev Day, etc*) you will get a pre-provisioned EKS cluster and can advance to the next step, [Join EKS cluster to Calico Cloud](./joinekstocalicocloud.html)
{{% /notice %}}

>This workshop uses EKS cluster with most of the default configuration settings. To create an EKS cluster and tune the default settings, consider exploring [EKS Workshop](https://www.eksworkshop.com) materials.

### Steps

1. Configure variables.

    ```bash
    export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
    export AZS=($(aws ec2 describe-availability-zones --query 'AvailabilityZones[].ZoneName' --output text --region $AWS_REGION))
    EKS_VERSION="1.20"
    IAM_ROLE='tigera-workshop-admin'
    
    # check if AWS_REGION is configured
    test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set

    # add vars to .bash_profile
    echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
    echo "export AZS=(${AZS[@]})" | tee -a ~/.bash_profile
    aws configure set default.region ${AWS_REGION}
    aws configure get default.region

    # verify that IAM role is configured correctly. IAM_ROLE was set in previous module to tigera-workshop-admin.
    aws sts get-caller-identity --query Arn | grep $IAM_ROLE -q && echo "IAM role valid" || echo "IAM role NOT valid"
    ```

    >Do not proceed if the role is `NOT` valid, but rather go back and review the configuration steps in previous module. The proper role configuration is required for Cloud9 instance in order to use `kubectl` CLI with EKS cluster.

2. *[Optional]* Create AWS key pair.

    >Follow this step only if want to access EKS nodes via SSH and want to use your own SSH key. Otherwise, skip this step.  
    >If you do configure your AWS key pair, make sure to uncomment the lines in the cluster configuration manifest at the next step under `ssh` section.

    In order to test host port protection with Calico network policy we will create EKS nodes with SSH access. For that we need to create EC2 key pair.

    ```bash
    export KEYPAIR_NAME='<set_keypair_name>'
    # create EC2 key pair
    aws ec2 create-key-pair --key-name $KEYPAIR_NAME --query "KeyMaterial" --output text > $KEYPAIR_NAME.pem
    # set file permission
    chmod 400 $KEYPAIR_NAME.pem
    # start ssh-agent
    eval `ssh-agent -s`
    # load SSH key
    ssh-add $KEYPAIR_NAME.pem
    ```

3. Create EKS manifest.

    >If you want to use SSH key created in the previous step, uncomment the lines under the `ssh` section.

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

4. Use `eksctl` to create EKS cluster.

    ```bash
    eksctl create cluster -f configs/tigera-workshop.yaml
    ```

5. View EKS cluster.

    Once cluster is created you can list it using `eksctl`.

    ```bash
    eksctl get cluster tigera-workshop
    ```

6. Test access to EKS cluster with `kubectl`

    Once the EKS cluster is provisioned with `eksctl` tool, the `kubeconfig` file would be placed into `~/.kube/config` path. The `kubectl` CLI looks for `kubeconfig` at `~/.kube/config` path or into `KUBECONFIG` env var.

    ```bash
    # verify kubeconfig file path
    ls ~/.kube/config
    # test cluster connection
    kubectl get nodes
    ```
