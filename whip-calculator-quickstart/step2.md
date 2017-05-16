The first step is to build the containers. This can be done with the `docker-compose build` command. Let's perform that command. (You can just click the command below to execute it.)

``docker-compose build``{{execute}}

We can then run the client by using the `docker-compose run client` command. When run, we will be presented with the calculator client. This command will also start up the adder and discovery service.

``docker-compose run client``{{execute}}

Let's try adding 2 and 2.

``add 2 2``{{execute}}

_Uh oh._ Two plus two does not equal three. Let’s use Whip to pinpoint the error. (Though, it should be no surprise, the adder has not held up its part of the bargain to perform the addition correctly.)

Let's quit the client program first.

``quit``{{execute}}

Note that the adder and discovery services are still running. To view their status, run the ``docker-compose ps`` command. 

``docker-compose ps``{{execute}}

To stop them, run ``docker-compose down``.

``docker-compose down``{{execute}}

In the next step, we will install a Whip adapter on the client.
