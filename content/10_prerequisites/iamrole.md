---
title: "Create an IAM role for your workspace"
chapter: false
weight: 13
---

{{% notice info %}}
Starting from here, when you see command to be entered such as below, you will enter these commands into Cloud9 IDE. You can use the **Copy to clipboard** feature (right hand upper corner) to simply copy and paste into Cloud9. In order to paste, you can use Ctrl + V for Windows or Command + V for Mac.
{{% /notice %}}

{{% notice warning %}}
If you are running this workshop at an AWS hosted event (such as *re:Invent, Kubecon, Immersion Day, Dev Day, etc*), please note that there will be an IAM role created for you. Please ignore this step and go to the next step, [Attach the IAM role to your Workspace](../10_prerequisites/workspaceiam.html). 
{{% /notice %}}

1. Follow [this deep link to create an IAM role with Administrator access.](https://console.aws.amazon.com/iam/home#/roles$new?step=review&commonUseCase=EC2%2BEC2&selectedUseCase=EC2&policies=arn:aws:iam::aws:policy%2FAdministratorAccess)
1. Confirm that **AWS service** and **EC2** are selected, then click **Next** to view permissions.
1. Confirm that **AdministratorAccess** is checked, then click **Next** to review.
1. Enter **tigera-workshop-admin** for the Name, and select **Create Role**.
![create-role](/images/create-role1.png)


