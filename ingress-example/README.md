# Overview

Sample deployment of ingress, ingress controller and exposing kubernetes dashboard to public IP on minikube.

# Files

## nginx-deployment.yaml

Contains sample deployment, which creates two pods of nginx image, which uses port 8080.

# Commands

Enable ingress addon on minikube and start dashboard.

```
minikube addons enable ingress
minikube dashboard
```

Validate that we have ingress controller pod, dashboard namespace.

```
kubectl get pod -n kube-system
kubectl get ns
```

Deploy our Ingress service.

```
kubectl apply -f dashboard-ingress.yaml
```

Validate that we have ingress running and obtain IP address that controller used for our ingress.

```
kubectl get ingress -n kubernetes-dashboard
```

Now we have to add that IP address as DNS record to our host file. For example if your Ingress' IP adress is 192.168.123.5

```
192.168.123.5 dashboard.com >> C:\Windows\System32\drivers\etc
```

Now try to load dashboard.com in your browser.

http://dashboard.com/

Lastly, you may want to configure default http backend, which is something, where ingress will route all its request which do not match any defined path.

You need to define a Service with name default-http-backend on port 80, which you map to some app/pod, which handles that request with some custom error page or redirect. 

# Source
https://www.youtube.com/watch?v=X48VuDVv0do