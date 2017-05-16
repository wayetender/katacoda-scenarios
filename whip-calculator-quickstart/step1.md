This is the Katacoda interactive tutorial page. Instructions will be printed here. On the bottom right is your terminal. On the top right is an editor where you can edit files (it will save automatically).

You can click a code example in this document to execute it in the terminal automatically -- no need to copy and paste.

This tutorial revovles around a simple microservices application.

The microservices application is a simple distributed calculator. It consists of three services: an adder, which performs numeric addition (which you could imagine being an extremely computationally expensive operation that must be distributed), a discovery service for adders, and a client which issues addition commands. The workflow of the application is:

1. An adder joins the set of available adders by invoking the `register_adder` operation on the discovery service that includes the address where the adder can be invoked.
2. A client requests the address of an available adder by invoking the `get_adder_info`. The discovery service returns a random available adder to the client.
3. With the given adder service address, the client invokes the `add` operation on the adder. The adder performs the computation and returns the result to the client.

The Thrift network protocol is defined in `src/calc.thrift`. You can click on the file in the editor in the top right pane. The services are implemented in Python and their implementations can be found in the `src/` subdirectory.
