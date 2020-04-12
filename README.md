## Selenium Grid on Azure Kubernetes Services (AKS) with Horizontal Pod Autoscaler on virtual nodes (ACI).

This sample code, setup a Selenium Grid and Nodes on AKS and ACI with autoscaling. Instead of running your browser nodes on AKS nodes, pods use virtual nodes (ACI) to spin up selenium hub nodes(Browsers). 

With AKS virtual nodes, you have fast provisioning of selenium browser nodes pods, and only pay per second for their execution time. Sample scripts spin up new browser nodes depend on CPU usage using Kubernetes Horizontal Pod Autoscaler.

## Prerequisites

Setup AKS with virtual nodes (https://docs.microsoft.com/en-us/azure/aks/virtual-nodes-portal)

## Setup Selenium hub

```
kubectl apply -f hub-AKS-deployment.yaml
```

Create service to access Selenum hub externally

```
kubectl apply -f hub-AKS-service.yaml
```

## Create Chrome node 

```
kubectl apply -f chrome-node-deployment.yaml
```

## Create Chrome node 

```
kubectl apply -f chrome-node-AKS-deployment.yaml
```

## Setup Pod Autoscaler

```
kubectl autoscale deployment chrome-node-rc --cpu-percent=40 --min=1 --max=5
```

```
kubectl get hpa -w
````

