---
title: "Update IAM settings for your Workspace"
chapter: false
weight: 19
---

{{% notice info %}}
Cloud9 normally manages IAM credentials dynamically. This isn't currently compatible with
the some AWS services authentication, so we will disable it and rely on the IAM role instead.

{{% /notice %}}

- Return to your workspace and click the gear icon (in top right corner), or click to open a new tab and choose "Open Preferences"
- Select **AWS SETTINGS**
- Turn off **AWS managed temporary credentials**
- Close the Preferences tab
![c9disableiam](/images/c9disableiam.png)


Let's run the command below, the following actions will take place as we do that: 

- Ensure temporary credentials aren’t already in place

- Remove any existing credentials file

- Set the region to work with our desired region

- Validate that our IAM role is valid

```sh
  rm -vf ${HOME}/.aws/credentials
  export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
  export AWS_DEFAULT_REGION=us-east-1
```

1. Download this repo into your environment:

    ```bash
    git clone https://github.com/tigera-solutions/tigera-eks-workshop
    cd tigera-eks-workshop
    ```

2. Update your kubeconfig file so that you will be able to interact with your Amazon EKS cluster: 

```
aws eks update-kubeconfig --name basic-eks --region us-east-1
```

3. Test that your kubeconfig file was properly updated by running the following command:

```bash
kubectl get svc
```
