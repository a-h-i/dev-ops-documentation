DevOps Instructions and Guides
==============================


## Warning
This is a work in progress some links may be dead for now.


This repository acts as a knowledge repo for any questions regarding the DevOps
A repository of knowledge as well as instruction.



Fedora or RPM based systems are assumed in these guides.

Please take the time to read the manuals


# Base Server Setup

For what to do after creating a new server and sshing there for the first time, and how to set it up consult
[this](generic/README.md) document.


# Services


For services that start your applications and auto restart them if failed and standarized logging consult [this](generic/SERVICES.md) document

# Timers


For periodic jobs we use systemd **DO NOT USE CRON** consult [this](generic/TIMERS.md) document for further information.


# Languages and Environments

For setting up language support please check [this](languages/README.md) document.



# Nginx Configuration

We use nginx as a reverse proxy and load balancer. To read on how to configure it check [this](nginx/README.md) document.


# HTTPS and certificate configuration

We always use HTTPS even in testing environments, check [this](nginx/HTTPS.md) document for how to.




# Setting up users, a compact beginners guide

Checkout [this](users-and-permissions/simple-user-creation.md) document for how to setup a simple user account for running a web service backend.



# provisioning infrastructure, general rules

Inrastructure for your standard webservice is split into the following components

Minumum of 2GB 1 CPU. For each CPU you add make sure you also add at least 1 GB of memory.
Note that caches and DBs would use up as much memory as you throw at them. With the difference that DBs also require processing power.



- Load balancer
- DB server(s)
- Cache
- Message Queues
- Background Workers
- Instance server(s)


The load balancer can be shared across multiple services.

I always use nginx as a load balancer myself.

DB Servers are things like Mongo or Postgresql again these are shared just like the load balancer.
Both the load balancer and DB Server are scaled vertically before horizontal.

Cache are either redis or memcached. The should be per APP and again scale vertically beforem horizontally. Ideally it would be a per instance of app mot per app.
The idea is you don't want to add network latency to your cache. Or at least minimize it. The best setup with memcached is to use one instance of memcached with each instance server. Thus essentially using memchached to provide an in memory DB cache for each app instance. In that case the app instance VPS would need to be a bit stronger.

Instance server. One server per app instance. not per app. If you want to to run 3 app instances you need exactly 3 app aservers.
The minumum app server or production is 2GB o ram and 1 CPU. Prefer 4GB 2 CPU if you can make the economics work.




# Example systemd service

Checkout [example_app](examples/systemd/example_app.service)



# CORS handling for Nginx

reffer to [cors nginx](snippets/nginx/cors.md)
