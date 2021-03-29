# Society

Society is a PoC used to implement microservices.

The context of the project is very broad: Reflect how a society works trough microservices, in a self sufficient way.

This repository will be used as the parent of all sub repositories as we work in a multi repository fashion for all the pieces of the PoC.

## The Universe service

By self sufficient, I mean that there is no user interaction needed for the society to grow, this is handled by the Universe service. Every N seconds ( N being defined in the configuration, based on the environement we are in. For the DEV environment I use a shorter N for testing purposes. ) the Universe "Ticks". A "Tick" is the equivalent for 1 day passing. So for example if N is 60 seconds, every 60 seconds a day passes in our Universe. The Universe service then publishes a message and all interested parties can listen and act on it.

The Universe service can be found [here](https://github.com/BusschaertTanguy/Society.Service.Universe)

## The Citizen service

The Citizen service will be the services handling the Citizens of our Society. This can be seen as a register of all the people that are / were present in our Society, with basic information around that person ( their name, age, gender, ... ).

The Citizen service can be found [here](https://github.com/BusschaertTanguy/Society.Service.Citizen)

## API Gateway

The services are hidden behind an API gateway for the consumer. Only the gateway has direct access to the services.

The gateway can be found [here](https://github.com/BusschaertTanguy/Society.ApiGateway)

## Service Discovery & Registry

I use Consul as service registry. All the services implement a hosted service that registers / deregisters themselves, and the API GW uses the provider to get the location of the service

## Web Application

Finally, A web application is exposed to interact with the services.

The angular application can be found [here](https://github.com/BusschaertTanguy/Society.Client.Angular)
