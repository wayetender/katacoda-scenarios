To use enhanced communication, we must install an adapter on all services. It turns out that the other services were already enhanced (which can be confirmed by inspecting the `run_adder.sh` and `run_discovery.sh` scripts) and we only need to make the client aware of the discovery service's adapter. We can make the client aware of the discovery Whip adapter with a simple configuration change for the client adapters.

Change the last line of `whip/adapter_client.yaml` file from

```
  - discovery:8000 mapstoservice AdderDiscovery
```

to:

```
  - discovery:8000 proxiedby discovery:38000 mapstoservice AdderDiscovery
```

This change tells the client that the AdderDiscovery service has a Whip adapter on port 38000. This means that the Whip client will use enhanced communication (i.e., will talk to the Whip adapter) when communicating with the AdderDiscovery service.

With this we can bring down the application, rebuild the containers (note: not the applications themselves), and run the client again:

``docker-compose down
docker-compose build
docker-compose run client``{{execute}}

And now when we add 2 + 2...

``add 2 2``{{execute}}

We can see now in this case the adder service was vouched for by the adder adapter (the blame label name "adder" comes from the `whip/adapter_adder.yaml` configuration file).

In the next step, we will discuss _indexed contracts_.
