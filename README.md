# dpar gRPC interface 

## Requiremets
- go version 1.21
- [dapr cli](https://docs.dapr.io/getting-started/install-dapr-cli/)
- docker
## Overview
### Service Invocation in Dapr: Simplifying Cross-Application Communication
Dapr's service invocation feature enhances cross-application communication by providing seamless methods to call functions between microservices applications or external HTTP endpoints.
* HTTP Service Invocation:
  If your application already utilizes HTTP protocols, incorporating Dapr is straightforward. Simply include the Dapr HTTP header, dapr-app-id, without the need to alter existing endpoint URLs. This allows you to quickly integrate service invocation capabilities. For detailed information, refer to [Invoke Services using HTTP](https://docs.dapr.io/developing-applications/building-blocks/service-invocation/howto-invoke-discover-services/).
* gRPC Service Invocation:
### Description
The provided Go code implements a Dapr application featuring service gRPC invocation capabilities. The key functionalities include:

* Method Invocation: The application defines a method, EchoMethod, which responds with "pong" when invoked. This serves as a basic demonstration of remote method invocation.

* Event Handling: The code includes methods, such as OnBindingEvent and OnTopicEvent, to handle events triggered by registered bindings and subscribed topics.

* List Topic Subscriptions: The ListTopicSubscriptions method specifies the application's interest in subscribing to a topic named "TopicA."

In summary, Dapr supports native interaction with gRPC, allowing users to maintain their own proto services effortlessly. This enables the invocation of existing gRPC applications without requiring additional Dapr SDKs or custom gRPC services. Explore [the Dapr and gRPC tutorial for a step-by-step guide](https://docs.dapr.io/developing-applications/building-blocks/service-invocation/howto-invoke-services-grpc/).

## Initialize  dapr
Dapr runs as a sidecar alongside your application. In self-hosted mode, this means it is a process on your local machine. By initializing Dapr, you:

Fetch and install the Dapr sidecar binaries locally.
Create a development environment that streamlines application development with Dapr.

1) Make sur that docker is runing & Run the init CLI command
    ````azure
    dapr init
    ````
2) Verify containers are running
    ````azure
    docker ps
    ````
## Testing
1) Run the application 
   ````azure
   dapr run --app-id gosvc --app-port 50001 --app-protocol grpc go run main.go
   ````
2) Invoke the App:
   ````azure
   dapr invoke --app-id gosvc --method EchoMethod
   ````
   This should return **pong** as defined in your **EchoMethod**
3) Test Bindings and Topics (Optional)
   * publish a message to a topicA
     ````azure
     dapr publish --publish-app-id gosvc --pubsub pubsub --topic TopicA --data "Hello, Dapr!"
     ````