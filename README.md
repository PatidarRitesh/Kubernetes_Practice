# Kubernetes with the help of Docker and Minikube

* Note : To learn kubernetes, you need to have some basic knowledge of Docker and Minikube.
  
  
## Docker installation
[Install Docker](https://docs.docker.com/engine/install/)

## Kubernetes installation
[Install Kubernetes](https://kubernetes.io/docs/tasks/tools/)

## Minikube installation
[Install Minikube](https://kubernetes.io/docs/tasks/tools/)

## Start minikube
```minikube start```

### Minikube Dashboard
```minikube dashboard```

### Minikube Stop
```minikube stop```

### Minikube Delete
```minikube delete```

## Docker Commands for building image and running container
## Commands for building image :

### web app image : 

```  docker build -t patidarritesh/node_mongo_demo . ```

<!-- ### Mongo db image : 
``` docker pull mongo  ``` -->


### Push the image to Docker Hub

``` docker push patidarritesh/node_mongo_demo:latest ```

### Run kubernrtes Deployement

```
kubectl create deployment <deployment_name> --image=nginx:latest

```

### Expose the deployment

```
kubectl expose deployment <deployment_name> --type=LoadBalancer --port=80

```

### Run the service

```
minikube service <service_name>

```


<!-- ### To run MongoDb

```
docker run -d -p 27017:27017 --network my-net --name mongo mongo 
```

### To run NodeApp
```
docker run -p 3000:3000 --network my-net --name nodeapp patidarritesh/node_mongo_demo:latest

``` -->

# Kubernetes Deployment
## Two containers in one pod

### Create a pod with two containers

#### Refer kuberenetes_deployement_demo.yaml file and run this command

```kubectl apply -f kuberenetes_deployement_demo.yaml```

#### After running this command, you can check the pods by running this command

```kubectl get pods```

#### You can check the deployment of containers by running this command

```kubectl get deployments```

#### Now Refer kubernetes_service.yaml file and run this command

```kubectl apply -f kubernetes_service.yaml```

#### After running this command, you can check the service by running this command

```mnikube services service_name```

#### TO delete the deployment and service, run this command

```
kubectl delete -n default deployment my-nodedb-app

```

## Two pods with one container in each pod
