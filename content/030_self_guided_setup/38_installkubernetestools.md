---
title: "6. Install Kubernetes Tools"
chapter: true
weight: 16
---
## Install Kubernetes Tools

Amazon EKS clusters require kubectl and kubelet binaries and the aws-cli or aws-iam-authenticator
binary to allow IAM authentication for your Kubernetes cluster.

{{% notice tip %}}
In this workshop we will give you the commands to download the Linux
binaries. If you are running Mac OSX / Windows, please [see the official EKS docs
for the download links.](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)
{{% /notice %}}

#### Install kubectl

{{% notice tip %}}
If needed, you can download the latest version of **kubectl** from [install-kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html) resource.
{{% /notice %}}

```bash
sudo curl --silent --location -o /usr/local/bin/kubectl \
   -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.26.4/2023-05-11/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl
```

#### Install eksctl

```bash
sudo curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

#### Update awscli

Upgrade AWS CLI according to guidance in [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html).

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Run the following command to verify that the AWS CLI has been upgraded:

```
aws --version
```

You should see the following output

```
aws-cli/2.2.15 Python/3.8.8 Linux/4.14.232-177.418.amzn2.x86_64 exe/x86_64.amzn.2 prompt/off
```

#### Install jq, envsubst (from GNU gettext utilities) and bash-completion

```bash
sudo yum -y install jq gettext bash-completion moreutils nc
```

#### Install yq for yaml processing

```bash
echo 'yq() {
  docker run --rm -i -v "${PWD}":/workdir mikefarah/yq "$@"
}' | tee -a ~/.bashrc && source ~/.bashrc
```

#### Verify the binaries are in the path and executable

```bash
for command in kubectl eksctl jq aws nc git
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```

#### Enable kubectl bash_completion

```bash
kubectl completion bash >>  ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```

#### Set alias for kubectl

```bash
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -F __start_kubectl k' >>~/.bashrc
. ~/.bashrc
```


