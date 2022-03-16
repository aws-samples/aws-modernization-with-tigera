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

    ![alerts view](/images/alerts-view.png)

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

2. Install `calicoctl` CLI

    The easiest way to retrieve captured `*.pcap` files is to use [calicoctl](https://docs.tigera.io/maintenance/clis/calicoctl/) CLI.

    ```bash
    CALICO_VERSION=$(kubectl get clusterinformation default -ojsonpath='{.spec.cnxVersion}')
    # download and configure calicoctl
    curl -o calicoctl -O -L https://docs.tigera.io/download/binaries/${CALICO_VERSION}/calicoctl
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
    tcpdump -Ar $(ls dev-* | head -1)
    tcpdump -Xr $(ls dev-* | head -1)
    ```

4. Clean up packet capture resource

    {{% notice info %}}
If a packet capture resource does not have `endTime` field, the capture would be continuous until the resource is removed.
    {{% /notice %}}

    Stop packet capture by removing the `PacketCapture` resource.

    ```bash
    kubectl delete -f demo/60-packet-capture/nginx-pcap.yaml
    ```

{{% notice tip %}}
   Note Packet Captures can also be created and scheduled directly from the Calico UI. Follow the Service Graph method for this alternative [procedure](https://docs.tigera.io/visibility/packetcapture#access-packet-capture-files-via-service-graph).
{{% /notice %}}

## Configure deep packet inspection for sensitive workloads

{{% notice tip %}}
Refer to [deep packet inspection](https://docs.tigera.io/threat/deeppacketinspection) documentation for more details about this capability.
{{% /notice %}}

1. Configure deep packet inspection (DPI) resource.

    Deploy DPI resource to allow Calico inspect packets bound for `dev/nginx` pods.

    ```bash
    kubectl apply -f demo/70-deep-packet-inspection/nginx-dpi.yaml
    ```

    >Once the `DeepPacketInspection` resource is deployed, Calico configures DPI controller to scan packets for endpoints matching the `selector` field configuration.

    Wait until all DPI pods become `Ready`

    ```bash
    watch kubectl get po -n tigera-dpi
    ```

2. Simulate malicious request and review alerts.

    Query `dev/nginx` application with payload that triggers a Snort rule alert.

    ```bash
    # example before v3.11
    kubectl -n dev exec -t centos -- sh -c "curl http://nginx-svc -H 'User-Agent: Mozilla/4.0' -XPOST --data-raw 'smk=1234'"

    # example for v3.11+
    kubectl -n uat exec -t netshoot -- sh -c "curl http://nginx-svc/secid_canceltoken.cgi -H 'X-CMD: Test' -H 'X-KEY: Test' -XPOST"
    ```

    Navigate to the Alerts view in Tigera UI and review alerts triggered by DPI controller. Calico DPI controller uses [Snort](https://www.snort.org/) signatures to perform DPI checks.
