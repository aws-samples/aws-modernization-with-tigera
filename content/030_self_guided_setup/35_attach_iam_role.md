---
title: "5. Attach the IAM role to your Workspace"
chapter: false
weight: 14
---

{{% notice info %}}
If you are running this at an AWS hosted event (such as *re:Invent, Kubecon, Immersion Day, Dev Day, etc*), the IAM role has been created for you so the IAM role you are attaching in this step will be different, e.g. __mod-*****__, than if you were to create your own IAM role, e.g. `tigera-workshop-admin`.
{{% /notice %}}

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Instances:tag:Name=aws-cloud9-tigera-workshop;sort=desc:launchTime) <br> Note: If no instances are found, click the gear icon in the top right corner and verify that "Use regular expression matching" is enabled.

2. Select the instance, then choose **Actions / Security / Modify IAM Role**

    ![c9instancerole](/images/tigera-workshop-admin.png)

3. Choose **tigera-workshop-admin** from the **IAM Role** drop down, and select **Apply**

4. Update IAM settings for your workspace.

    {{% notice info %}}
Cloud9 normally manages IAM credentials dynamically. This isn't currently compatible with
some AWS services authentication, so we will disable it and rely on the IAM role instead.

    {{% /notice %}}

    - Return to your Cloud9 workspace and click the gear icon (in top right corner)
    - Select AWS SETTINGS
    - Turn off AWS managed temporary credentials
    - Close the Preferences tab

        ![Cloud9 AWS settings](../images/c9disableiam.png)
