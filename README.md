# Proxy Challenge MELI using K8S

API Proxy developed for the Mercado Libre technical challenge using kuberntes instead of Docker directly.

## Getting Started
These challenge was developed in kubernetes, for that reason all configuration files were made in .yaml format.
that said, these instructions will get you a copy of the project up and running on your local machine for development and testing purposes.


### Prerequisites
- Docker (https://www.docker.com/get-started)
- Minikube (https://minikube.sigs.k8s.io/docs/start/)

### Development Profile
NOTE: In order to use a Kubernetes node, we decided to use minikube. That said, before deploying any configuration we need to get installed and running Docker and Minikube.

1.- Initialize Docker in your system.

2.- Initialize Minikube in order to run a K8S node:
```
minikube start
```

3.- Run the configuration files in this order:
```
kubectl apply -f nginx_configmap.yaml
```
```
kubectl apply -f nginx_deployment.yaml
```
```
kubectl apply -f nginx_service.yaml
```
```
kubectl apply -f prometheus_configmap.yaml
```
```
kubectl apply -f prometheus_deployment.yaml
```
```
kubectl apply -f prometheus_service.yaml
```

### Check Reverse Proxy and Metrics
NOTE: check the node IP address (kubectl get nodes -o wide) and use it in the links, in my case was 192.168.49.2

Test the proxy:
```
curl http://192.168.49.2:30080/categories/MLA5725
```

Check the statistics of the proxy:
```
curl http://192.168.49.2:30080/nginx_status
```

Check the Nginx metrics in Prometheus metrics format:
```
http://http://192.168.49.2:30113/metrics
```

Check the Nginx metrics in Prometheus:
```
http://192.168.49.2:30090
```

## Solution diagram
![diagram](https://user-images.githubusercontent.com/77750560/194356318-be7cd5b6-4a12-40e6-b48f-263c4ceb9bce.jpg)

## Notes
* Proxy exclusively created with Nginx
* The proxy is configured to accept 50000 requests per second.
* It's possible to filter the requests based on IP addresses (change nginx.conf)