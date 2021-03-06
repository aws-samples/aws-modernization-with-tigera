
# AWS Modernization with Tigera


### Welcome

The intent of this workshop is to educate any person working with EKS cluster in one way or another about Calico features and how to use them. While there are many capabilities that Calico provides, this workshop focuses on a subset of those that are used most often by different types of technical users.

### Learning Objectives

In this workshop we are going to focus on these main use cases:

- **East-West security**, leveraging zero-trust security approach.
- **Egress access controls**, using DNS policy to access external resources by their fully qualified domain names (FQDN).
- **Host micro-segmentation**, leveraging Calico policies to protect host ports and host based services.
- **Observability**, exploring various logs and application level metrics collected by Calico.
- **Compliance**, providing proof of security compliance.

### Instruction to run workshop on your own: 

This page is build with Hugo, so you'll need to install it - https://gohugo.io/getting-started/installing/

Next, clone this repo: 

```
git clone git@github.com:aws-samples/aws-modernization-with-tigera.git 
```

Ensure that you have also cloned the submodules:

```
git submodule init
git submodule update
```

Start the server with Hugo:
```
hugo server
```

Go to localhost: to view the content in your web browser of choice
