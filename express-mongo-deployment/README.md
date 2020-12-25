# Overview

Example deployment of mongo database and express application, which communicate via internal service between each other.  
Express application is also accessible from browser via external service.

# Files

## mongo.yaml

Contains deployment and service definition for mongo db container.  
Deployment creates one pod with username and passwords loaded from secret.
Service exposes container to other containers on port 27017.

## mongo-secret.yaml

Contains username and password for mongodb. 
**IMPORTANT**: Those values must be base64 encoded.

## mongo-configmap.yaml

Contains key-value with mongodb url, which is simply name of the service which exposes mongodb pod.

# Commands

First of all, we need to create secrets before deployment.

```
kubectl apply -f mongo-secret.yaml
```

Next we will create MongoDB pod and internal service, which exposes container's port 27017 to other containers on kubernetes cluster.

```
kubectl apply -f mongo.yaml
```

Once again, we need to create configmap before deployment, which uses values from configmap.

```
kubectl apply -f mongo-configmap.yaml
```

Now we can create the express app deployment. We also create an external service, which is different from internal service by being a type of LoadBalancer and having nodePort value.

```
kubectl apply -f mongo-express.yaml
```

Lastly, we need to assign external IP address, which is done in minikube with the following command.

```
minikube service mongo-express-service
```

# Source
https://www.youtube.com/watch?v=X48VuDVv0do