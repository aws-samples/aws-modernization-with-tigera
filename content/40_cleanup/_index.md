+++
title = "Cleanup"
chapter = true
weight = 20
+++


Congrats! You've reached the end of today's workshop.

## Cleanup

1. Delete application stack to clean up any `loadbalancer` services.

    ```bash
    kubectl delete -f demo/dev/app.manifests.yaml
    kubectl delete -f https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/master/release/kubernetes-manifests.yaml
    ```

2. Delete EKS cluster.

    ```bash
    eksctl delete cluster --name tigera-workshop
    ```

3. Delete EC2 Key Pair.

    ```bash
    export KEYPAIR_NAME='<set_keypair_name>'
    aws ec2 delete-key-pair --key-name $KEYPAIR_NAME
    ```

4. Delete Cloud9 instance.

    Navigate to `AWS Console` > `Services` > `Cloud9` and remove your workspace environment, e.g. `tigera-workshop`.

5. Delete IAM role created for this workshop.

    Navigate to `AWS Console` > `Services` > `IAM` and remove your `tigera-workshop-admin` role.
