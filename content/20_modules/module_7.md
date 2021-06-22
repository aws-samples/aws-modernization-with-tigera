+++
title = "Module 7: Security alerts"
chapter = false
weight = 20
+++


>**Estimated time:** 10 min

## Learning objectives

Use global alerts to notify security and operations teams about unsanctioned or suspicious activity.

## Steps

{{% notice info %}}
We deployed security alerts in the first module. While we were implementing the use cases, some of them have triggered the alerts and now we can explore them.
{{% /notice %}}

1. Review alerts manifests.

    Navigate to `demo/50-alerts` path and review YAML manifests that represent alerts definitions. Each file containes an alert template and alert definition. Alerts templates can be used to quickly create an alert definition in the UI.

2. View triggered alerts.

    Open `Alerts` view to see all triggered alerts in the cluster. Review the generated alerts.

    ![alerts view](../images/alerts-view.png)

    You can also review the alerts configuration and templates by navigating to alerts configuration in the top right corner.
