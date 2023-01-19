# Kubernetes Microservice Boilerplate - apache with Configmap template

This template uses an upstream open-source deployment helm chart (apache) and this 
repo highlights just how easily you can customize those helm charts with an configmap
being volume mounted into place during runtime.  This allows you to take apache
and make dozens of various proxy servers, which can be desirable to for example act
as an HTTPS enabler for some non-HTTPS service, or via ingress annotations to add 
custom authorization/authentication layers on top of this service without having
to implement any in your backend service (via things like OAuth Proxy / External Auth, etc)

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

Your service might not immediately be available on the internet, because this "stack" requires you have an ingress controller installed, and requires you set the hostname properly (see values-dev.yaml in deployment/boilerplate-apache-with-configmap-template).  Alternatively, you may change the `service.type: LoadBalancer` in the values file if you wish to use this without an ingress.  This will create an load balancer and public endpoint in basically any kubernetes cluster provider.

Make any adjustments you want to either the values.yaml and values-dev.yaml files, and/or create another "env" by making a new values-ENVNAME.yaml and changing the configuration around to deploy to that environment.  See values-prod.yml for an example.  Run `make diff` every time you make adjustments to the values files to see what it would change in Kubernetes.  For more info about what is possible to configure in the values files, please see the [Default upstream values.yaml file](https://github.com/DevOps-Nirvana/Universal-Kubernetes-Helm-Charts/blob/master/charts/deployment/values.yaml). Basically you can configure and override everything, but everything has sane defaults.
