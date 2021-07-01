---
title: "Attach the IAM role to your Workspace"
chapter: false
weight: 17
---

1. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:tag:Name=aws-cloud9-;sort=desc:launchTime).


4. Configure AMI role for Cloud9 workspace.

    >This is necessary when using Cloud9 environment which has an IAM role automatically associated with it. You need to replace this role with a custom IAM role that provides necessary permissions to build EKS cluster so that you can work with the cluster using `kubectl` CLI.

    

    a. Assign the IAM role to Cloud9 workspace.

    - Click the grey circle button (in top right corner) and select `Manage EC2 Instance`.

        ![Cloud9 manage EC2](../images/cloud9-manage-ec2.png)
1. Select the instance, then choose **Actions / Security / Modify IAM Role**.
![c9instancerole](/images/attach-role2.png)

1. Choose **tigera-workshop-admin** from the **IAM Role** drop down, and select **Apply**.

    a. Select the instance, then choose `Actions` > `Security` > `Modify IAM Role` and assign the IAM role you created in previous step, i.e. `tigera-workshop-admin`.

    ![Modify IAM role](../images/modify-iam-role.png)

    b. Update IAM settings for your workspace.

    - Return to your Cloud9 workspace and click the gear icon (in top right corner)
    - Select AWS SETTINGS
    - Turn off AWS managed temporary credentials
    - Close the Preferences tab

        ![Cloud9 AWS settings](../images/c9disableiam.png)

    - Remove locally stored `~/.aws/credentials`

        ```bash
        rm -vf ~/.aws/credentials
        ```

    c. Unset `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` to allow Cloud9 instance use the configured IAM role.

    ```bash
    unset AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY
    ```
