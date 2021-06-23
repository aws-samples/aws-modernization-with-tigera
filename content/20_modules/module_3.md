+++
title = "Module 3: Use security alerts and leverage dynamic packet capture"
chapter = false
weight = 12
+++


>**Estimated time:** 20 min

## Learning objectives

- Use global alerts to notify security and operations teams about unsanctioned or suspicious activity.
- Configure packet capture for specific pods to capture packet payload for further forensic analysis and explore the captured payload.

## Use security alerts

{{% notice info %}}
We deployed security alerts in the first module. While we were implementing the use cases, some of them have triggered the alerts and now we can explore them.
{{% /notice %}}

1. Review alerts manifests.

    Navigate to `demo/50-alerts` path and review YAML manifests that represent alerts definitions. Each file containes an alert template and alert definition. Alerts templates can be used to quickly create an alert definition in the UI.

2. View triggered alerts.

    Open `Alerts` view to see all triggered alerts in the cluster. Review the generated alerts.

    ![alerts view](../images/alerts-view.png)

    You can also review the alerts configuration and templates by navigating to alerts configuration in the top right corner.

## Leverage dynamic packet capture

{{% notice tip %}}
Refer to [packet capture](https://docs.tigera.io/visibility/packetcapture) documentation for more details about this capability.
{{% /notice %}}

1. Configure packet capture.

    Navigate to `demo/60-packet-capture` and review YAML manifests that represent packet capture definition. Each packet capture is configured by deploing a `PacketCapture` resource that targets endpoints using `selector` and `labels`.

    Deploy packet capture definition to capture packets for `dev/nginx` pods.

    ```bash
    kubectl apply -f demo/60-packet-capture/nginx-pcap.yaml
    ```

    >Once the `PacketCapture` resource is deployed, Calico starts capturing packets for all endpoints configured in the `selector` field.

    Stop packet capture by removing the `PacketCapture` resource.

    ```bash
    kubectl delete -f demo/60-packet-capture/nginx-pcap.yaml
    ```

2. Install `calicoctl` CLI

    The easiest way to retrieve captured `*.pcap` files is to use [calicoctl](https://docs.tigera.io/maintenance/clis/calicoctl/) CLI.

    ```bash
    # download and configure calicoctl
    curl -o calicoctl -O -L https://docs.tigera.io/download/binaries/v3.7.0/calicoctl
    chmod +x calicoctl
    sudo mv calicoctl /usr/local/bin/
    calicoctl version
    ```

3. Fetch and review captured payload.

    >The captured `*.pcap` files are stored on the hosts where pods are running at the time the `PacketCapture` resource is active.

    Retrieve captured `*.pcap` files and review the content.

    ```bash
    # get pcap files
    calicoctl captured-packets copy dev-capture-nginx --namespace dev

    ls dev-nginx*
    # view *.pcap content
    tcpdump -Xr dev-nginx-XXXXXX.pcap
    ```
