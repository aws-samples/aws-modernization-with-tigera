---
title: "2. Create a Workspace"
chapter: true
weight: 12
---

## Set up the Workspace

[AWS Cloud9](https://aws.amazon.com/cloud9/) is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your laptop for this workshop.

## Access Cloud9 in AWS Management Console 

Once you have logged into the AWS Management Console from your EventEngine team landing page, you will already have an EKS cluster and Cloud9 environment. A few additional steps are required to configure Cloud9 and install the tools as follows. Below set of instructions are also available in the **readme** link in the Event Engine Dashboard.


![cloudd9](/images/event-engine-cloud9-dashboard.png)

Click on the **Open IDE** button and you will see your pre-configured environment. 

## Lab environment
Once you have logged into the AWS Management Console from your EventEngine team landing page, you will already have an EKS cluster and Cloud9 environment. A few additional steps are required to configure Cloud9. Please follow the steps below.

1. Navigate to Cloud9 in the AWS Management console and launch the EKS IDE. It may take a few minutes to start.
* Select the gear icon in the upper right (or else select the "9" icon>Preferences in the upper left)
    1. Scroll down to "AWS Settings" in the "Preferences" tab.
    2. Under "Credentials", disable "AWS managed temporary credentials".
    3. Close the "Preferences" tab.
    4. Close the "AWS Cloud9 Welcome" and "AWS Toolkit" tabs.
* Open a new terminal tab by clicking the green "+" sign and selecting "New Terminal".
    1. Copy and run this command:
       ```bash
       aws s3 cp s3://ee-assets-prod-us-east-1/modules/ad831bb586fb4f77ad39569fdf52fe6d/v1/eksinit.sh . && chmod +x eksinit.sh && ./eksinit.sh ; source ~/.bash_profile
       ```
    2. You can test access to your cluster by running the following command. The output will be a list of worker nodes.
       ```bash
       kubectl get nodes
       ```
You should then see the a similar output to the following

```bash
ip-192-168-103-203.us-east-2.compute.internal   Ready    <none>   26h   v1.20.11-eks-f17b81
ip-192-168-135-115.us-east-2.compute.internal   Ready    <none>   26h   v1.20.11-eks-f17b81
ip-192-168-162-61.us-east-2.compute.internal    Ready    <none>   26h   v1.20.11-eks-f17b81
```

You are now ready to move on to the next step!

{{% notice tip %}}
Cloud9 requires third-party-cookies. You can whitelist the [specific domains](https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).  You are having issues with this, Ad blockers, javascript disablers, and tracking blockers should be disabled for the cloud9 domain, or connecting to the workspace might be impacted.
{{% /notice %}}
