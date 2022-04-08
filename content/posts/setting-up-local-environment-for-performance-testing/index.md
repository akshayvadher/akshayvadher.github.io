---
title: "Setting Up Local Environment for Performance Testing"
date: 2022-04-04T19:10:40+05:30
draft: true
tags: ["performance", "testing", "minikube", "kubernetes", "grafana", "opentelemetry"]
categories: ["tech"]
author: ["Akshay Vadher"]
summary: Setup the local environment to test application using k6, kubernetes, grafana, opentelemetry, etc.
cover:
    image: "indira-tjokorda-Y-VYK0SDLxs-unsplash.jpg"
    alt: "Speed Skating"
    caption: Speed Skating"
    relative: true # To use relative path for cover image, used in hugo Page-bundles
---
![Speed Skating](indira-tjokorda-Y-VYK0SDLxs-unsplash.jpg)

I wanted to test Spring MVC vs Spring WebFlux performance. Before I get started on a technology, I wanted to do a quick performance test.

Here is my setup to do performance testing in local. 

## Tools
| Tool           | For                                                  |
|----------------|------------------------------------------------------|
| docker         | continer                                             |
| kubernetes     | container orchestration                              |
| minikube       | Local Kubernetes                                     |
| k6             | Bombarding Tool - Tool to generate load              |
| grafana        | Visulization                                         |
| Influx DB      | K6 and Grafana integration - DB to store API reports |
| Open telemetry | Monitor traces                                       |

## Installation Steps
### Docker
Go to [docker](https://www.docker.com/products/docker-desktop/) and install for your OS

### Kubernetes
We will be installing minikube(next step) for this.

Install `kubectl` to interect with k8s. [Link](https://kubernetes.io/docs/tasks/tools/). For windows, 

```
choco install kubernetes-cli
kubectl version --client
```

### Minikube
[Minikube](https://minikube.sigs.k8s.io/docs/start/) has a good getting started guide. 

For windows like me, following commands will install minikube if choco is already installed
```
choco install minikube
```

Start minikube using 
```
minikube start
```

### k6
[k6](https://k6.io/docs/getting-started/installation/) is a good load generation tool by grafana. It has getting started guide for different OS, however for Windows
```
choco install k6
```

### Helm
[helm](https://helm.sh/docs/intro/install/) is a package manager for kubenetes. We will use it to install Grafana and other monitoring tools. We can install everything manually as well but this will help us speed up installation. 
```
choco install kubernetes-helm
helm repo update
```

### Prometheus
We will use Prometheus to capture metrics data for k8s cluster.
Add helm chart
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm search repo prometheus
```
Install 
```
helm install prometheus prometheus-community/prometheus
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack
```
Expose from kubernetes and create minkube tunnel so that It can be accessed from local.
```
kubectl expose service prometheus-server --type=LoadBalancer --port=9090 --name=prometheus-server-lb
kubectl get all // check if prometheus is up
minikube tunnel
```
Make sure you don't close minikube tunnel, otherwise we cannot access it from local. Go to [http://127.0.0.1:9090](http://127.0.0.1:9090) to access.

### InfluxDB
[InfluxDB](https://www.influxdata.com/products/influxdb-overview/) is a time seriese DB. We will use it to capture k6 (load testing report)
```
helm repo add influxdata https://helm.influxdata.com/
// OR
helm repo add bitnami https://charts.bitnami.com/bitnami
// Search
helm search repo influxd
// Install
helm install influx influxdata/influxdb
// OR
helm install influx bitnami/influxdb
// Check
kubectl get all
// Create tunnel
kubectl expose service/influxdb --type=LoadBalancer --port=8086 --name=influxdb-lb
```

### Grafana
[Grafana](https://github.com/grafana/helm-charts) can be installed using helm charts easily.
```
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana
kubectl get all // check if grafana is up
kubectl expose service grafana --type=LoadBalancer --port=3000 --name=grafana-lb
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}"
```
Go to [http://127.0.0.1:3000](http://127.0.0.1:3000) to check if Grafana is accessible with `admin`:`prom-operator`

## Running
Create a file test.js with
```javascript
import { check, sleep } from 'k6';
import http from 'k6/http';
import { Counter } from 'k6/metrics';

let errorCount = new Counter('Status Failures');
export const options = {};
// export const options = {
//   vus: 1000,
//   duration: '10s',
// };

// export const options = {
//   stages: [
//     { duration: '10s', target: 10 },
//     { duration: '10s', target: 100 },
//     { duration: '10s', target: 100 },
//     { duration: '10s', target: 1000 },
//     { duration: '10s', target: 1000 },
//     { duration: '10s', target: 10 },
//     { duration: '10s', target: 0 },
//   ],
// };

let token;

export function setup() {
  let tokenResponse = http.post(
    'https://monnai-main-test.auth.ap-southeast-1.amazoncognito.com/oauth2/token',
    {
      client_id: '1q5q5ciegvc8f284fpr1lj01ov',
      grant_type: 'client_credentials',
      scope:
        'insights/phone_basic insights/phone_identity insights/phone_social insights/email_basic insights/email_social',
      client_secret: '1qgimfcsshdqan6gt0ujufq7l20iugstglfaks7r5n9lglm3ant6',
    },
  );
  token = tokenResponse.json().access_token;
}

export default function () {
  let response = http.post(
    'https://test.monnai.com/api/insights',
    {
      eventType: 'ACCOUNT_CREATION',
      cleansingFlag: true,
      packages: ['PHONE_BASIC'],
      email: '',
      phoneNumber: '+919662059401',
      phoneDefaultCountryCode: 'IN',
      originalCountryCode: 'IN',
    },
    { headers: { 'Content-Type': 'application/json' } },
  );
  let success = check(response, {
    'Status is 200': (r) => r.status === 200,
  });

  if (!success) {
    errorCount.add(1);
    console.log(response)
  }

  // sleep(2 * Math.random())
}

```

Run it using
```
k6 run --out influxdb=http://localhost:8086/k6 test.js
```

##### Credit
Photo by <a href="https://unsplash.com/@indiratjokorda?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Indira Tjokorda</a> on <a href="https://unsplash.com/s/photos/speed-api?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  