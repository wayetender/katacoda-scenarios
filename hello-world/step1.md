This is your first step.

## Task

This is an _example_ of creating a scenario and running a **command**

`docker create -v /data --name dataContainer busybox
docker cp service.thrift dataContainer:/data/
docker run --volumes-from dataContainer thrift thrift -o /data --gen rb /data/service.thrift
docker cp dataContainer:/data/gen-rb .`{{execute}}
