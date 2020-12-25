# Overview

Sample deployment of kubernetes deployment and service.

# Files

## nginx-deployment.yaml

Contains sample deployment, which creates two pods of nginx image, which uses port 8080.

## nginx-service.yaml

Contains sample service, which maps container's port 8080 to port 80 for other other containers to access nginx pods. (It is still internal port, which cannot be accessed from the outside.)

## nginx-result.yaml

File generated by using commands below.

# Commands

Apply both configuration files to create deployment, which creates two pods and service, which exposes them on port 80.

```
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
```

Validate that everything is up and running.

```
kubectl get pod
kubectl get pod -o wide
kubectl get service
kubectl describe service nginx-service
```

Now we can obtain the resulting configuration back to file.

```
kubectl get deployment nginx-deployment -o yaml > nginx-result.yaml
```

Afterwards we can delete it using the files again.

```
kubectl delete -f nginx-deployment.yaml
kubectl delete -f nginx-service.yaml
```

# Source
https://www.youtube.com/watch?v=X48VuDVv0do