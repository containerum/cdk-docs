---
title: Nginx Ingress-Controller
linktitle: NGINX Ingress Controller
description: Installing Nginx Ingress-Controller to access applications in Kubernetes by an External IP.

categories: []
keywords: []

menu:
  docs:
    parent: "plugins"
    weight: 5
    identifier: nginx-ingress

draft: false
---

# How to install Ingress-Controller for Kubernetes

Ingress Controller is required to access applications running in Kubernetes by an External IP. Рекомендуемые версии

## Installation
Install the ingress-controller from the Kubernetes repository:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
```

### Service creation
Create a service for the ingress-controller. Create a yaml file (e.g., `ingress-svc.yaml`):

```
apiVersion: v1
kind: Service
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
spec:
  ports:
  - name: http
    port: 80
    targetPort: 80
    protocol: TCP
  - name: https
    port: 443
    targetPort: 443
    protocol: TCP
  selector:
    app.kubernetes.io/name: ingress-nginx
  externalIPs:
  - %EXTERNAL IP%
  ```
Add your machine's external IP address to %EXTERNAL IP%

Then run:
```
kubectl apply -f ingress-svc.yaml
```

Check if the services are there:
```
kubectl get svc -n ingress-nginx
```

The nginx ingress-controller is ready.
