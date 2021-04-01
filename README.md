# Society

Society is a PoC used to implement microservices.

The context of the project is very broad: Reflect how a society works trough microservices, in a self sufficient way.

This repository will be used as the parent of all sub repositories as we work in a multi repository fashion for all the pieces of the PoC.

## Web Client

The web client we use for this application is made in angular, and can be found [here](https://github.com/BusschaertTanguy/Society.Client.Angular)

## Service Discovery

The stack is deployed on kubernetes, so service discovery is purely handled by kubernetes. The API gateway communicates with kubernetes services, which sit in front of deployment pods. 1 Microservice thus have 1 service, 1 deployment with N replicas per deployment.

## API Gateway

I use [Ocelot](https://ocelot.readthedocs.io/en/latest/index.html) as an API gateway, it simply takes upstream calls and forwards them to the right downstream service.

## Inter service communication

Inter service communication happens in 2 ways:

- Response/Request model: Trough a REST API
- Asynchronous messaging: Trough a [message queue](https://masstransit-project.com/)

## The Universe service

By self sufficient, I mean that there is no user interaction needed for the society to grow, this is handled by the Universe service. Every N seconds ( N being defined in the configuration, based on the environement we are in. For the DEV environment I use a shorter N for testing purposes. ) the Universe "Ticks". A "Tick" is the equivalent for 1 day passing. So for example if N is 60 seconds, every 60 seconds a day passes in our Universe. The Universe service then publishes a message and all interested parties can listen and act on it.

The Universe service can be found [here](https://github.com/BusschaertTanguy/Society.Service.Universe)

## The Citizen service

The Citizen service will be the services handling the Citizens of our Society. This can be seen as a register of all the people that are / were present in our Society, with basic information around that person ( their name, age, gender, ... ).

The Citizen service can be found [here](https://github.com/BusschaertTanguy/Society.Service.Citizen)

## Running the stack on a local environment
### Prerequisites

Kubernetes purely hosts the microservices and the gateway, everything storage or queue related is on the host. So for this to work, you have to have:

- MS SQL
- RabbitMQ
- Docker
- Minikube

installed on your host machine.

For configuration, you only have to change the environment variables in the YAML file of the microservices, the following has to be changed:

- MS SQL Host address and user credentials
- RabbitMQ Host address and user credentials

Everything else should be good.

### Starting the stack

When your MS SQL instance, RabbitMQ instance and minikube are running, the first thing you have to do is open a minikube tunnel so that your host machine can access the api gateway, open a separate terminal and run

```
minikube tunnel
```

Then, u can start the kubernetes services and deployment pods by running:

```
kubectl create -f ./
```

In the root of this repository. This should all the services and deployment pods.

For now, you can just start the frontend trough your IDE, the endpoint is already configured to point to the gateway.
