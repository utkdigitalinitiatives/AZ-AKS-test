# AZ-AKS-test

Goals:
 - Implement FluxCD GitOps in AKS K8s test environment
 - Deploy some test apps
    - solr, prom-kube-stack


## Flux Configurations Used:

Staging:
~~~shell
az k8s-configuration flux create \
  --name solr-staging \
  --cluster-name VS-k8s \
  --resource-group rg-k8s \
  --cluster-type managedClusters \
  --scope cluster \
  --url https://github.com/utkdigitalinitiatives/AZ-AKS-test \
  --branch main \
  --interval 1m \
  --kustomization name=infrastructure path=./infrastructure/staging prune=true \
  --kustomization name=apps path=./apps/staging prune=true depends_on=infrastructure
~~~

Production:
~~~shell
az k8s-configuration flux create \
  --name solr-production \
  --cluster-name VS-k8s \
  --resource-group rg-k8s \
  --cluster-type managedClusters \
  --scope cluster \
  --url https://github.com/utkdigitalinitiatives/AZ-AKS-test \
  --branch main \
  --interval 1m \
  --kustomization name=infrastructure path=./infrastructure/production prune=true \
  --kustomization name=apps path=./apps/production prune=true depends_on=infrastructure
~~~

