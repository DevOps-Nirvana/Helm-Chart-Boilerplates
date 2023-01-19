# Grafana-Dashboards

Grafana-dashboards helm chart is just a simple helm chart which deploys a bunch of configmaps which Grafana imports

# Usage

Make sure you set the following on the Grafana helm chart...

```
grafana:
  sidecar:
    dashboards:
      enabled: true
      label: grafana_dashboard
```

## Prerequisites

- Kubernetes 1.6+ with Beta APIs enabled
- The kubectl binary
- The helm binary
- Helm diff plugin installed

## Installing the Chart

To install the chart...

```bash
export SERVICE_NAME="grafana-dashboards"
export CI_ENVIRONMENT_SLUG="dev"
export HELM_CHART=$SERVICE_NAME
export CURRENT_HELM_CHART=$SERVICE_NAME
# Go into our deployment folder
cd deployment
# Update our helm subchart...
helm dependencies update $SERVICE_NAME
# View the diff of what you want to do
helm diff upgrade --namespace infrastructure --allow-unreleased $CURRENT_HELM_CHART $HELM_CHART     -f $CURRENT_HELM_CHART/values.yaml  -f $CURRENT_HELM_CHART/values-$CI_ENVIRONMENT_SLUG.yaml
# Actually do it...
helm upgrade --install --namespace infrastructure $CURRENT_HELM_CHART $HELM_CHART     -f $CURRENT_HELM_CHART/values.yaml   -f $CURRENT_HELM_CHART/values-$CI_ENVIRONMENT_SLUG.yaml
```

## Configuration

None