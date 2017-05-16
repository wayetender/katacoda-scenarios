You can fix the broken adder by inspecting and modifying Line 18 of `src/adder.py`. Just change `return a + b - 1` to `return a + b`. By bringing down the services and bringing them back (as was done above), the error will go away.

``docker-compose down
docker-compose build
docker-compose run client``{{execute}}

And now let's try adding 2 and 2.

``add 2 2``{{execute}}

No more error!
