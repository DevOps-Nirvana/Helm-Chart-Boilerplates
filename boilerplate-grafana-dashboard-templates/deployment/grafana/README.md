# Grafana

Grafana helm chart is just using a subchart of the [official stable Grafana helm chart](https://github.com/helm/charts/tree/master/stable/grafana)

## Introduction

This chart bootstraps a simple Grafana deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.6+ with Beta APIs enabled
- The kubectl binary
- The helm binary
- Helm diff plugin installed

## Installing the Chart

To install the chart...

```bash
export SERVICE_NAME="grafana"
export CI_ENVIRONMENT_SLUG="shared"
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

For configuration options possible, please see [official stable Grafana helm chart](https://github.com/helm/charts/tree/master/stable/grafana)
