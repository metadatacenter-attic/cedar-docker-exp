CEDAR Nginx Docker Container
============================

This Docker container runs CEDAR's Nginx server. 

The Nginx server is configured to use SSL so the containter must be supplied with certificates
that correspond to the domain and relevant CEDAR subdomains that are assigned to the container.
The container mounts a volume that maps to a host directory containing these certificates. 
The SSL certificates must match the ```cedar```-prepended host name given to the machine and also be 
valid for the subdomains ```auth```, ```cedar```,```folder```, ```repo```, 
```resource```, ```schema```, ```template```, ```terminology```, and ```valuerecommender```. 

As present, the container also mounts a source directory containing the CEDAR code base.

#### Building and Running

To build this Docker container:

    docker build -t="metadatacenter/cedar-nginx-server:0.1.0" .

To run:

    docker run -d 
      -h <host name> -p 443:443 
      -v <CEDAR source directory>:/srv/cedar 
      -v <host SSL certificates directory>:/srv/certificates 
      --name cedar-nginx metadatacenter/cedar-nginx-server:0.1.0

The host name must have matching SSL certificates in the ```host SSL certificates``` directory. 

e.g.,

    docker run -d \
      -h cedar.metadatacenter.net -p 443:443 \
      -v /Users/bob/workspace/cedar:/srv/cedar \
      -v /Users/bob/private/certificates/metadatacenter.net:/srv/certificates \
      --name cedar-nginx metadatacenter/cedar-nginx-server:0.1.0

To see that the container is running:

    docker ps

Use the ```DOCKER_HOST``` environment variable to find the Docker server IP address and map the host name to this 
IP address in the host machine's ```/etc/hosts/``` file. 
(The SSL layer is expecting a host name matching the certificate so a raw IP address will not work.)

To test connectivity to the Nginx server in the container:

    curl -i -vvv https://<host name>/

To look at the container logs:

    docker logs cedar-nginx-server

To look at the container ports:

    docker port cedar-nginx-server 

To create a shell inside the running container:

    docker exec -it cedar-nginx-server /bin/bash

To look at Nginx log when inside container:

    tail -f /var/log/nginx/access.log
    tail -f /var/log/nginx/error.log

To stop the container:

    docker stop cedar-nginx-server

To remove the container:

    docker rm cedar-nginx-server


