# boilerplate-simple

This helm chart is just using a subchart of our standardized deployment helm charts

## Introduction

This chart bootstraps a highly available deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager following best-practices in the arena of Kubernetes.  This includes deploying a PDB if needed, horizontal pod autoscaling, AWS Security Groups (if specified), service accounts, etc.  For more details on this upstream helm chart, please see [DevOps Nirvana / Universal Helm Charts](https://github.com/DevOps-Nirvana/Universal-Kubernetes-Helm-Charts)

## Prerequisites

- Kubernetes 1.10+ with Beta APIs enabled
- The kubectl binary
- The helm binary (3.0+)
- Helm diff plugin installed

## Installing the Chart

To install and use this chart...

First, edit the file values-dev.yaml in this folder and put in the hostname(s) at which you wish to host this service in your cluster.  This is optional, but this is considered the "best practice" in a DevOps Nirvana setup, every service defines a service and an ingress, but does _not_ create a Load Balancer.  Your load balancer is Nginx Ingress which adds routing, metrics, red/blue capabilities, and more.

```bash

# Define the necessary env vars, tweak as desired
export SERVICE_NAME="boilerplate-simple"
export CI_ENVIRONMENT_SLUG="dev"  # This is the values file which based on this (values-dev.yaml)
export K8S_NAMESPACE="dev"        # This is the namespace to deploy to, this must exist already
export HELM_CHART=$SERVICE_NAME   # For simplicity this is the same as the above service name
export CURRENT_HELM_CHART=$SERVICE_NAME  # Ditto

# Go into our deployment folder
cd deployment
# Update our helm subchart...
helm dependencies update $SERVICE_NAME/
# View the diff of what you want to do
helm diff upgrade --namespace $K8S_NAMESPACE --allow-unreleased $CURRENT_HELM_CHART $HELM_CHART     -f $CURRENT_HELM_CHART/values.yaml     -f $CURRENT_HELM_CHART/values-${CI_ENVIRONMENT_SLUG}.yaml        --set global.namespace="$K8S_NAMESPACE"
# Actually do it...
helm upgrade --namespace $K8S_NAMESPACE --install $CURRENT_HELM_CHART $HELM_CHART     -f $CURRENT_HELM_CHART/values.yaml     -f $CURRENT_HELM_CHART/values-${CI_ENVIRONMENT_SLUG}.yaml  --set global.image.tag="$HELM_IMG_TAG" --set global.namespace="$K8S_NAMESPACE"
```

## Configuration

For configuration options possible, please see our [helm-charts](#todo) repository
