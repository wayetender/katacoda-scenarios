We will start by installing an adapter on the client to catch the error.

To do this we will need a Whip contract and a Whip adapter configuration. For the tutorial, we have provided both: the contract is located in `whip/calculator.whip` and the configuration file for the client is located in `whip/adapter_client.yaml`.

Of particular interest is the client proxy string:

```
  - discovery:8000 mapstoservice AdderDiscovery
```

This states that that there is an `AdderDiscovery` service at the `discovery` host with port `8000`.

In order to deploy the client with the Whip adapter with the above configuration, we need to create an adapter and use the shim library on the client. The shim command is a shell script that instructs the operating system to preload the interposition library to intercept on new network connections.

The entry point of the client application is in the `run_client.sh` script (take a look at it in your editor in the top right window). Inspecting the file, we can see that the adapter is already created in the first line of the script. The only remaining step is to add the shim library. We can do that by modifying the last line of the `run_client.sh` script from:

```
python src/client.py discovery 8000
```

to:

```
shim python src/client.py discovery 8000
```

This will successfully install the Whip adapter on the client, without any code changes to the client itself.

With the adapter installed we can bring down the application, rebuild the containers (note: not the service applications themselves), and run the client again:

``docker-compose down
docker-compose build
docker-compose run client``{{execute}}

Now let's add 2 and 2:

``add 2 2``

Success! I mean, failure! We have a contract failure, that is. We have successfully captured a first-order contract failure (i.e., that `2 + 2` is not equal to `3`).

Note that the service was `vouched for by unknown`. That is, the imprecise blame label was used. That is because the client was using unenhanced communication due to partial deployment. In the next step, we will switch the client adapter to use enhanced communication with the other services.

