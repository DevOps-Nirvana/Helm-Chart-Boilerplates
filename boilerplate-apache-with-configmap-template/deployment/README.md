# Boilerplate apache with Configmap template

This template uses an upstream open-source deployment helm chart (apache) and this 
repo highlights just how easily you can customize those helm charts with an configmap
being volume mounted into place during runtime.

## Introduction

This chart bootstraps a highly available deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.17+ cluster
- The kubectl binary
- The helm 2.0+ binary
- Helm diff plugin installed

## Installing the Chart

To install the chart...

```bash
export SERVICE_NAME="http-proxy"
export CI_ENVIRONMENT_SLUG="dev"
export HELM_CHART=$SERVICE_NAME
export CURRENT_HELM_CHART=$SERVICE_NAME
# Go into our deployment folder
cd deployment
# Update our helm subchart...
helm dependencies update $SERVICE_NAME/
# View the diff of what you want to do
helm diff upgrade --namespace infrastructure --allow-unreleased $CURRENT_HELM_CHART $HELM_CHART     -f $CURRENT_HELM_CHART/values.yaml     -f $CURRENT_HELM_CHART/values-${CI_ENVIRONMENT_SLUG}.yaml
# Actually do it...
helm upgrade --namespace infrastructure --install $CURRENT_HELM_CHART $HELM_CHART     -f $CURRENT_HELM_CHART/values.yaml     -f $CURRENT_HELM_CHART/values-${CI_ENVIRONMENT_SLUG}.yaml
```

Hint, the above commands are exactly what you'd need in your CI/CD system to deploy.  :)

## Configuration

For configuration options possible, please see our [Universal Helm Charts](https://github.com/DevOps-Nirvana/Universal-Kubernetes-Helm-Charts) repository
