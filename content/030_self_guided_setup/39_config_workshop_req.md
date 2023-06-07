---
title: "7. Configure workshop specific requirements"
chapter: true
weight: 17
---

## Configure Workspace

In this section, we will be installing a few tools to help in running through this workshop

1. Copy and run (paste with **Ctrl+P** or **CMD+P**) the commands below.

      Before running it, review what it does by reading through the comments.

    ```sh
    # Remove existing credentials file.
    rm -vf ${HOME}/.aws/credentials
      
    # Set the ACCOUNT_ID and the region to work with our desired region
    export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
    export AZS=($(aws ec2 describe-availability-zones --query 'AvailabilityZones[].ZoneName' --output text --region $AWS_REGION))
    EKS_VERSION="1.26"
    IAM_ROLE='tigera-workshop-admin'
    test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set

    # add vars to .bash_profile
    echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
    echo "export AZS=(${AZS[@]})" | tee -a ~/.bash_profile
    aws configure set default.region ${AWS_REGION}
    aws configure get default.region

   # Validate that our IAM role is valid.
    aws sts get-caller-identity --query Arn | grep tigera-workshop-admin -q && echo "IAM role valid" || echo "IAM role NOT valid"
      ```

   {{% notice warning %}}
   If the IAM role is not valid, <span style="color: red;">**DO NOT PROCEED**</span>. Go back and confirm the steps on this page.
   {{% /notice %}}

   If you are done, please proceed to the **next** section!

2. Clone `tigera-solutions/tigera-eks-workshop` Github repo

    You will use [tigera-solutions/tigera-eks-workshop](https://github.com/tigera-solutions/tigera-eks-workshop) repo to implement use cases for this workshop. Clone the repo and `cd` into it.

    ```bash
    git clone https://github.com/tigera-solutions/tigera-eks-workshop
    cd tigera-eks-workshop
    ```

3. *[Optional]* Create AWS key pair.

    >Follow this step only if you want to access EKS nodes via SSH and want to use your own SSH key. Otherwise, skip this step.  
    >If you do configure your AWS key pair, make sure to uncomment the lines in the cluster configuration manifest YAML in the next section at the `ssh` stanza.

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
