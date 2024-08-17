# e-Commerce-Amit spring boot services.

## Important Note: Tried to cover as many as portion from the 12 facttor app by cloud native.

<!--## Better Code Hub
I analysed this repository according to the clean code standards on [Better Code Hub](https://bettercodehub.com/) just to get an independent opinion of how bad the code is. Surprisingly, the compliance score is high!
-->
## Introduction
- This project is a development of a small set of **Spring Boot** and **Cloud** based Microservices projects that implement cloud-native intuitive, Reactive Programming, Event-driven, Microservices design patterns, and coding best practices.
- The project follows **CloudNative**<!--(https://www.cncf.io/)--> recommendations and The [**twelve-factor app**](https://12factor.net/) methodology for building *software-as-a-service apps* to show how μServices should be developed and deployed.
- This project uses cutting edge technologies like Docker, Kubernetes, Elasticsearch Stack for
 logging and monitoring, Java SE 17, Postgres,Mongo and MySQL databases, all components developed with TDD in mind, covering integration & performance testing, and many more.
 - This project is going to be developed as stages.
---
## Getting started
### System components Structure
Let's explain first the system structure to understand its components:
```
eCommerceAmit [MicroService] --> Parent folder.
|- docs --> All docs and diagrams.
|- k8s --> All **Kubernetes** config files.
    |- api-gateway --> API Gateway server is single entry points for all the services including  Authentication & Authorization Service using keycloak.  
    |- service-discovery --> Service Registery server(As project is moving to K8, this project is removed as Kubernates provide this functionality)
    |- cloud-config --> Centralized Configuration server(As project is moving to K8, this project is removed as Kubernates provide this functionality)
    |- Product Service --> Manage products for eCommerece, all products will be saved with these API.
    |- Order-service --> Manage orders and save order after checking records in Inventory services. Also store messages to Kafka topic if order is placed successfully.
    |- Inventory-service --> its keep the inventory data, order services uses it before placing order.
    |- Notification Service --> Consumer for Kafka topic which receive messages from the topic and send the email to concern store.
  
|- compose.yml --> contains all services landscape with Kafka  

```
Now, as we have learned about different system components, then let's start.

### System Boundary *Architecture* - μServices Landscape

![System Boundary](app-architecture.drawio.png)

### Required software

The following are the initially required software pieces:

1. **Java 17**: JDK 17 LTS can be downloaded and installed from https://www.oracle.com/

1. **Git**: it can be downloaded and installed from https://git-scm.com/downloads

1. **Maven**: Apache Maven is a software project management and comprehension tool, it can be downloaded from here https://maven.apache.org/download.cgi

1. **curl**: this command-line tool for testing HTTP-based APIs can be downloaded and installed from https://curl.haxx.se/download.html

1. **Spring Boot Initializer**: This *Initializer* generates *spring* boot project with just what you need to start quickly! Start from here https://start.spring.io/

1. **Docker**: The fastest way to containerize applications on your desktop, and you can download it from here [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

1. **Kubernetes**: We can install **minikube** for testing puposes https://minikube.sigs.k8s.io/docs/start/

   > structure is created but not yet tested. 

Follow the installation guide for each software website link and check your software versions from the command line to verify that they are all installed correctly.

## Using an IDE

I recommend that you work with your Java code using an IDE that supports the development of Spring Boot applications such as Spring Tool Suite or IntelliJ IDEA Ultimate Edition. So you can use the Spring Boot Dashboard to run the services, run each microservice test case, and many more.

All that you want to do is just fire up your IDE **->** open or import the parent folder `ecommerce-microservice-backend-app`, and everything will be ready for you.

## Data Model
### Entity-Relationship-Diagram
![System Boundary](ecommerce-ERD.drawio.png)

## Playing With e-Commerce-boot Project

### Cloning It

The first thing to do is to open **git bash** command line, and then simply you can clone the project under any of your favorite places as the following:

```bash
> git clone https://github.com/amittelang1976/eCommerceAmit.git
```

### Build & Test Them In Isolation

To build and run the test cases for each service & shared modules in the project, we need to do the following:

#### Build & Test µServices
Now it is the time to build our **4 microservices** and run each service integration test in
 isolation by running the following commands:

```bash
$ ./mvnw clean package 
```

## How to build the backend services

Run the following command to build and package the backend services into a docker container

```shell
mvn spring-boot:build-image -DdockerPassword=<your-docker-account-password>
```

The above command will build and package the services into a docker container and push it to your docker hub account.

## How to run the backend services

Make sure you have the following installed on your machine:

- Java 21
- Docker
- Kind Cluster - https://kind.sigs.k8s.io/docs/user/quick-start/#installation

### Start Kind Cluster
    
Run the k8s/kind/create-kind-cluster.sh script to create the kind Kubernetes cluster

```shell
./k8s/kind/create-kind-cluster.sh
```
This will create a kind cluster and pre-load all the required docker images into the cluster, this will save you time downloading the images when you deploy the application.

### Deploy the infrastructure

Run the k8s/manisfests/infrastructure.yaml file to deploy the infrastructure

```shell
kubectl apply -f k8s/manifests/infrastructure.yaml
```

### Deploy the services

Run the k8s/manifests/applications.yaml file to deploy the services

```shell
kubectl apply -f k8s/manifests/applications.yaml
```

### Access the API Gateway

To access the API Gateway, you need to port-forward the gateway service to your local machine

```shell
kubectl port-forward svc/gateway-service 9000:9000
```

### Access the Keycloak Admin Console
To access the Keycloak admin console, you need to port-forward the keycloak service to your local machine

```shell
kubectl port-forward svc/keycloak 8080:8080
```

### Access the Grafana Dashboards
To access the Grafana dashboards, you need to port-forward the grafana service to your local machine

```shell
kubectl port-forward svc/grafana 3000:3000
```
In the end, I hope you enjoyed the application and find it useful, as I did when I was developing it. 
If you would like to enhance, please: 
- **Open PRs**, 
- Give **feedback**, 
- Add **new suggestions**, and
- Finally, give it a 🌟.

*Happy Coding ...* 🙂
