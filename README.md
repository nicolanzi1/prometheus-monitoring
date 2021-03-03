## Project Specifications

In this project, we will monitor a MongoDB (third-party) application in Kubernetes, using Prometheus Monitoring, MongoDB Exporter, Service Monitor, Service Discovery, and Grafana.

We will be able to achieve this with the following steps:

1. We will deploy a Prometheus Operator in our Minikube cluster using a helm chart
2. Then we will deploy a MongoDB application as an example
3. Lastly, we will configure our MongoDB application for Prometheus monitoring using a MongoDB exporter, Prometheus UI, Prometheus Alert Manager and Grafana

### Tools

First we need to install the following tools:

[Docker Download](https://www.docker.com/get-started)

Then, in our terminal, inside the project's folder:

```
~$ Hyperkit - brew install hyperkit
~$ Minikube - brew install minikube
~$ Helm - brew install helm
```

#### Create Minikube Cluster

```
~$ minikube start --cpus 4 --memory 8192 --vm-driver hyperkit
```

or (depending on Memory's capacity)

```
~$ minikube start --cpus 4 --memory 4096 --vm-driver hyperkit
```

#### Install Prometheus-Operator

###### Add Repos

In our terminal, inside the project's folder:

```
~$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
~$ helm repo add stable https://kubernetes-charts.storage.googleapis.com/
~$ helm repo update
```

###### Install Chart

```
~$ helm install prometheus prometheus-community/kube-prometheus-stack
```

###### You can also install the Chart with a fixed version

```
~$ helm install prometheus prometheus-community/kube-prometheus-stack --version "9.4.1"
```

###### Link to Chart

[Prometheus Chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)

#### Install Mongodb-Exporter

###### Add Repos

```
~$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
~$ helm repo update
```

###### Install Chart

```
~$ helm install mongodb-exporter prometheus-community/prometheus-mongodb-exporter
```

###### Yo can also install the Chart with a fixed version

```
~$ helm install mongodb-exporter prometheus-community/prometheus-mongodb-exporter --version "2.8.1"
```

###### Link to Chart

[MongoDB Exporter](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-mongodb-exporter)

#### port-forwardings

###### Prometheus-UI

```
~$ kubectl port-forward service/prometheus-kube-prometheus-prometheus 9090
```

###### Alert Manager UI

```
~$ kubectl port-forward svc/prometheus-kube-prometheus-alertmanager 9093
```

###### Grafana

```
~$ kubectl port-forward deployment/prometheus-grafana 3000
```

###### Grafana Dashboard credentials

- User: admin
- Password: prom-operator (from values.yaml file set as default)

###### Mongodb-exporter

```
~$ kubectl port-forward service/mongodb-exporter-prometheus-mongodb-exporter 9216
```
