<<<<<<< HEAD
# prometheus_grafana_k8s_demo

## Introduction: What is the purpose and value of Prometheus and Grafana?

## How to install Prometheus and Grafana on K8s?

## How to deploy some applications to K8s?

## Result: What is the value of monitoring applicatons?
=======
# Prometheus and Grafana on Kubernetes Demo

This demo shows you how to deploy Prometheus and Grafana into your Minikube/K8s cluster. Prometheus will help us monitor our Kubernetes Cluster and other resources running on it. Grafana will help us visualize metrics recorded by Prometheus and display them in fancy dashboards.

## What is the purpose and value of Prometheus?

Monitoring Production Kubernetes Cluster(s) is an important and progressive operation for any Cluster Administrator. There are myriad of solutions that fall into the category of Kubernetes monitoring stack, and some of them are Prometheus and Grafana. This guide is created with an intention of guiding Kubernetes users to Setup Prometheus and Grafana on Kubernetes using prometheus-operator.

Prometheus is a full fledged solution that enables Developers and SysAdmins to access advanced metrics capabilities in Kubernetes. The metrics are collected in a time interval of 30 seconds, this is a default settings. The information collected include resources such as Memory, CPU, Disk Performance and Network IO as well as R/W rates.

## What is the purpose and value of Grafana?

Grafana is an open source solution for running data analytics, pulling up metrics that make sense of the massive amount of data & to monitor our apps with the help of cool customizable dashboards.

Grafana connects with every possible data source, commonly referred to as databases such as Graphite, Prometheus, Influx DB, ElasticSearch, MySQL, PostgreSQL etc.

Grafana being an open source solution also enables us to write plugins from scratch for integration with several different data sources.

The tool helps us study, analyse & monitor data over a period of time, technically called time series analytics.

It helps us track the user behaviour, application behaviour, frequency of errors popping up in production or a pre-prod environment, type of errors popping up & the contextual scenarios by providing relative data.

A big upside of the project is it can be deployed on-prem by organizations which do not want their data to be streamed over to a vendor cloud for security & other reasons.

## How to install Prometheus and Grafana on K8s?

- Clone the demo project repository

```
git clone https://github.com/prometheus-operator/kube-prometheus.git
```

- Switch to the root project directory

```
cd kube-prometheus
```

- Create a namespace and required CustomResourceDefinitions

```
kubectl create -f manifests/setup
```

- Confirm that the monitoring namespace is working

```
kubectl get ns monitoring
```

- Confirm that the prometheus-operator pod is running

```
kubectl get pods -n monitoring
```

- Deploy prometheus monitoring stack on K8s

```
kubectl create -f manifests/
```

- Ensure the pods within the monitoring stack is running on K8s

```
kubectl get pods -n monitoring
```

- List the services running within the monitoring namespace

```
kubectl get svc -n monitoring
```

## Method 1: Local Deployment

- Expose the grafana service locally

```
kubectl --namespace monitoring port-forward svc/grafana 3000
```

Grafana URL: http://localhost:3000

Grafana Credentials: Username: admin Password: admin

- Expose the prometheus service locally

```
kubectl --namespace monitoring port-forward svc/prometheus-k8s 9090
```

Prometheus URL: http://localhost:9090

- Expose the alert manager dashboard locally

```
kubectl --namespace monitoring port-forward svc/alertmanager-main 9093
```

Alert Manager URL: http://localhost:9093

## Method 2: NodePort for Private Clusters

- Prometheus:

```
kubectl --namespace monitoring patch svc prometheus-k8s -p '{"spec": {"type": "NodePort"}}'
```

- Alertmanager:

```
kubectl --namespace monitoring patch svc alertmanager-main -p '{"spec": {"type": "NodePort"}}'
```

- Grafana:

```
kubectl --namespace monitoring patch svc grafana -p '{"spec": {"type": "NodePort"}}'
```

- Confirm that the each of the services have a Node Port assigned:

```
kubectl -n monitoring get svc | grep NodePort
```

Access URLs
  
- Grafana:

```
http://node_ip:31123
```

- Prometheus
  
```
http://node_ip:31123
```

- Alert Manager
  
```
http://node_ip:31237
```

## Method 3: Using Load Balancers

- TODO
## How to destoy or tear down the deployment?

``` 
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```

>>>>>>> 140e107 (Updated structure and intructions)
