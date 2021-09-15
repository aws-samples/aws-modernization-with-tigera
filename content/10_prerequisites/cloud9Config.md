---
title: "Configure workspace environment"
chapter: false
weight: 19
---

Let's run the commands below. The following actions will take place as we do that:

- Ensure temporary credentials aren’t already in place

- Remove any existing credentials file

- Set the region to work with our desired region

- Validate that the workspace's IAM role matches the IAM role we assigned to the Cloud9 instance

```sh
  if [ -f ${HOME}/.aws/credentials ]; then rm -vf ${HOME}/.aws/credentials; fi
  export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
  export AWS_DEFAULT_REGION=us-east-1
  echo -e "Workspace instance IAM role:\n\t $(curl -s http://169.254.169.254/latest/meta-data/iam/info | jq .InstanceProfileArn | cut -d / -f2 | sed 's/\"$//')"
```

1. Download this repo into your environment:

    ```bash
    git clone https://github.com/tigera-solutions/tigera-eks-workshop
    cd tigera-eks-workshop
    ```

2. Update your kubeconfig file so that you will be able to interact with your Amazon EKS cluster:

    ```bash
    aws eks update-kubeconfig --name basic-eks --region us-east-1
    ```

3. Test that your kubeconfig file was properly updated by running the following command:

    ```bash
    kubectl get svc
    ```
