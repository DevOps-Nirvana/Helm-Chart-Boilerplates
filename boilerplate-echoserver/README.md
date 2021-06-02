# Kubernetes Microservice Boilerplate - Echo Server

A boilerplate microservice example using the Universal Helm charts hosting a HTTP "echo server" from google which is useful for debugging and introspection into what headers are set.

This simple example doesn't require any docker builds or anything, you can just run a few command line commands to get this rolling on your cluster.  Please see ./deployment/boilerplate-echoserver

# Usage

A simple usage to try to deploy this service using the make file would be...

```
# This installs our upstream helm chart
make setup
# Then runs helm diff to see what it would apply to your kubernetes cluster
make diff
# Then run deploy to apply it
make deploy
```

Your service might not immediately be available on the internet, because this "stack" by default requires/uses Nginx Ingress as your Ingress Controller and API Gateway, and requires you set the hostname properly (see values-dev.yaml in deployment/boilerplate-echoserver).  Nginx Ingress adds a lot of great things, I wouldn't host an HTTP-based service on Kubernetes without it.  You may need to either go install and configure Nginx Ingress first, or you may need to change the `service.type: LoadBalancer` in the values file if you wish to use this without the default Nginx Ingress recommendation.

Make any adjustments you want to either the values.yaml and values-dev.yaml files, and/or create another "env" by making a new values-ENVNAME.yaml and changing the configuration around to deploy to that environment.  See values-prod.yml for an example.  Run `make diff` every time you make adjustments to the values files to see what it would change in Kubernetes.  For more info about what is possible to configure in the values files, please see the [Default upstream values.yaml file](https://github.com/DevOps-Nirvana/Universal-Kubernetes-Helm-Charts/blob/master/charts/deployment/values.yaml). Basically you can configure and override everything, but everything has sane defaults.
