---
title: "Create a Calico Cloud Account"
chapter: false
weight: 20
---

- [Calico Cloud trial account](https://www.tigera.io/tigera-products/calico-cloud/)
- for instructor-led workshop use instructions in the email you receive to request a Calico Trial account.
- for self-paced workshop follow the [link to register](https://www.tigera.io/tigera-products/calico-cloud/) for a Calico Trial account.
- You will receive something similar to below, please keep it safe you will need it to finish the Cloud9 configuration.

  ```bash
  # script should look similar to this
  kubectl apply -f https://installer.calicocloud.io/manifests/cc-operator/latest/deploy.yaml && curl -H "Authorization: Bearer xxxxxx:yyyyyy:zzzzzzzz" "https://www.calicocloud.io/api/managed-cluster/deploy.yaml" | kubectl apply -f -
  ```
