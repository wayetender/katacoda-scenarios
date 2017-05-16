Finally, we show how Whip tracks indexed contracts with a special indexed contract form given in `whip/calculator.indexed.whip`. This indexed contract provides adder services only when the first operand (`a`) is exactly equal to `1`. In all other cases, the adder service and discovery service do not vouch for its behavior. In other words, if the client provides an a operand to the adder that is not exactly `1` then it will vouch for the behavior of the adder service. This indexed contract provides adder services only when the first operand a is exactly equal to 1. That is, if the first operand is `1`, then the adder service vouches for the behavior of the adder service (and will be blamed if the service does not meet the contract). If the first operand is not equal to `1`, then the adder service and discovery service do not vouch for the behavior of the adder service. So, that means that if the client invokes the adder service with the first argument being something other than `1`, then it should be the client that is blamed for any incorrect behavior rather than the adder service. (Note that this example is representative of, for example, the client using an invalid authorization token or identifier.)


In the editor in the top right, modify each Whip configuration file (`adapter_adder.yaml`, `adapter_client.yaml`, and `adapter_discovery.yaml`) to have the spec field be `whip/calculator.indexed.whip` instead of `whip/calculator.whip`.

---

Once the configuration files are modified, we can rebuild the containers and try running the client with different arguments for `a`:

``docker-compose down
docker-compose build
docker-compose run client``{{execute}}

Let's now try adding 1 and 2:

``add 1 2``{{execute}}

Note that the adder was blamed (i.e., it was `vouched for by adder`).

Now let's try adding 2 and 2:

``add 2 2``{{execute}}

Now note that client vouched for the service, as `a` was not equal to `1`.

Finally, let's quit out and fix the adder service error.

``quit``{{execute}}


