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

```
kubectl apply -f kuberenetes_deployement_demo.yaml
```

#### After running this command, you can check the pods by running this command

```
kubectl get pods
```

#### You can check the deployment of containers by running this command

```
kubectl get deployments
```

#### Now Refer kubernetes_service.yml file and run this command

```
kubectl apply -f kubernetes_service.yml
```

#### After running this command, you can check the service by running this command

```
mnikube services service_name
```

#### TO delete the deployment and service, run this command

```
kubectl delete deployment my-nodedb-app

```

## Two pods with one container in each pod

### Create config file Each contain configuraton for deployement and service 

 1. For database (In our case Mongodb) 
 2. For Web app (In our case NodeApp)
 3. For Config Map 

* The configMap file contains the configuration of configMap and secret for the mongo-db
*  We can also call this host mapping
  

### Run The config file using following command :

```
kubectl apply -f mongo-db.yml
```
```
kubectl apply -f node-app.yml
```
```
kubectl apply -f mongo-config.yml
```

### Now run minikube service 

```
minikube service <service name>
```


## volumes and data management in kubernetes 

#### Why Volumes ?


* In Kubernetes, volumes play a crucial role in persisting and sharing data among containers within the same pod or across different pods. These volumes decouple the storage configuration from individual containers, offering a flexible solution for managing data.

* If a server experiences downtime due to various reasons, Kubernetes is designed to automatically handle the recovery of applications. Kubernetes can reschedule and restart the affected pods on healthy nodes, ensuring the availability of the application. However, in the absence of a persistent storage solution, the data within the containers may be lost during these disruptions.

* This is where volumes become essential. Volumes provide a means to persist data beyond the lifecycle of a pod or container. By using volumes, data can survive pod terminations, rescheduling, and even node failures. In the event of server downtime or pod rescheduling, Kubernetes can recreate the pods, and the data stored in volumes remains intact.

### Persistent Volumes (PVs) and Persistent Volume Claims (PVCs):

#### Create Two config file one for Persistent Volume for reserving volume or storage and one for Persistent Volume Claims for claming that reserved storage space.

#### Now Run this Commands in same order :

```
kubectl apply -f host-pv.yml
```
```
kubectl apply -f host-pvc.yml
```

#### After claiming volume now run our container 

```
kubectl apply -f mongo-db.yml
```
```
kubectl apply -f node-app.yml
```

### Now run minikube service 

```
minikube service <service name>
```







