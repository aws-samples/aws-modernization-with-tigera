---
title: "Finish Cloud9 configuration"
chapter: false
weight: 21
---


Your Cloud9 environment comes prebuilt with a version of Docker that doesn't have the features that we will need for this workshop. Please follow the steps below to install and verify that you have the correct version.

1. Open the terminal on Cloud9 and run the following: 

2. Ensure your environment has these tools:

    - [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
    - [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
    - [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html)
    - [EKS kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)
    - `jq` and `netcat` utilities

    Check whether these tools already present in your environment. If not, install the missing ones.

    ```bash
    # run these commands to check whether the tools are installed in your environment
    aws --version
    git --version
    eksctl version
    kubectl version --short --client

    # install jq and netcat
    sudo apt install jq netcat -y
    jq --version
    nc --version
    ```

    >For convenience consider configuring [autocompletion for kubectl](https://kubernetes.io/docs/tasks/tools/included/optional-kubectl-configs-bash-linux/#enable-kubectl-autocompletion).

3. Download this repo into your environment:

    ```bash
    git clone https://github.com/tigera-solutions/tigera-eks-workshop
    cd tigera-eks-workshop
    ```
