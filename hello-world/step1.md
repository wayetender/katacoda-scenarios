This is your first step.

## Task

This will create the thrift service protocol Whip.

`docker create -v /data --name dataContainer busybox
docker cp service.thrift dataContainer:/data/
docker run --volumes-from dataContainer thrift thrift -o /data --gen rb /data/service.thrift
docker cp dataContainer:/data/gen-rb .`{{execute}}

Check out what it generated...

`ls gen-rb
head -n 5 gen-rb/service_types.rb`{{execute}}

