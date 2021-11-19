---
title: "3. Attach IAM Role"
chapter: true
weight: 14
---

## Attach the IAM role to your instance

Since an EKS Cluster has already been pre-provisioned with all the IAM roles created, all you need to do is attach it!

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Instances:search=aws-cloud9-harness;sort=desc:launchTime)

2. Select the instance, then choose **Actions / Security / Modify IAM role**

    ![Attach IAM role](/images/attach-role.png)

3. Choose the role that contains "BastionStack" in it.

    ![Bastion Instance Profile role](/images/tigera-modify-iam.png)

4. Click **Save**