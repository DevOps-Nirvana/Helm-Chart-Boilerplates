# Kubernetes Microservice Boilerplate - Grafana and Dashboards Templates

This template doesn't use any of my/our Helm Charts, it uses upstream charts entirely.
This is a great example to understand how helm charts/subcharts works and how to have multiple
charts in one "deployment" folder, which is automatically handled automatically with an CI/CD 
Script such as 
[DevOps-Nirvana/aws-helm-multi-deploy-nodocker](https://github.com/DevOps-Nirvana/aws-helm-multi-deploy-nodocker)
if you are using self-hosted pre-built runners or [DevOps-Nirvana/aws-helm-multi-deploy](https://github.com/DevOps-Nirvana/aws-helm-multi-deploy)
if you are using Github's Actions Runners.  This is also an example of how to use a configmap which
reads from a directory all the files and puts it in a configmap.  See deployment/grafana-dashboards/templates for
the example!


# Usage

View the README.md in the deployment folder of each of the charts in this folder to view the commands to deploy

You can also use this folder directly with these actions

* [DevOps-Nirvana/aws-helm-multi-deploy-nodocker](https://github.com/DevOps-Nirvana/aws-helm-multi-deploy-nodocker)
* [DevOps-Nirvana/aws-helm-multi-deploy](https://github.com/DevOps-Nirvana/aws-helm-multi-deploy)
