CEDAR Nginx Docker Container
===========================

This Docker container runs CEDAR's Nginx server. The host machine must have a directory
containing the CEDAR code base and a directory containing SSL certificates, both
of which are mounted as volumes by the container when it runs. The SSL
certificates must match the ```cedar```-prepended host name given to the machine and also be 
valid for the subdomains ```auth```, ```folder```, ```repo```, ```resource```, ```schema```, ```template```, ```terminology```, and ```valuerecommender```. 

==== Building and Running

To build this Docker container:

    docker build -t="metadatacenter/cedar-nginx:0.1.0" .

To run:

    docker run -d 
      -h <host name> -p 443:443 
      -v <CEDAR source directory>:/srv/cedar 
      -v <host SSL certificates>:/srv/certificates 
      --name cedar-nginx metadatacenter/cedar-nginx:0.1.0

The host name must have matching SSL certificates in the ```host SSL certificates>``` directory. 

e.g.,

    docker run -d \
      -h cedar.metadatacenter.net -p 443:443 \
      -v /Users/moconnor/workspace/cedar:/srv/cedar \
      -v /Users/moconnor/workspace/conf/certificates/metadatacenter.net:/srv/certificates \
      --name cedar-nginx metadatacenter/cedar-nginx:0.1.0

To see that the container is running:

    docker ps

Use DOCKER_HOST environment variable to find the Docker server IP address and map the host name to this 
IP address in the host machine's ```/etc/hosts/``` file.

To test connectivity to the Nginx server in the container:

    curl -i -vvv https://<host name>/

To look at the container logs:

    docker logs cedar-nginx

To look at the container ports:

    docker port cedar-nginx 

To create a shell inside the running container:

    docker exec -it cedar-nginx /bin/bash

To look at Nginx log when inside container:

    tail -f /var/log/nginx/access.log
    tail -f /var/log/nginx/error.log

To stop the container:

    docker stop cedar-nginx

To remove the container:

    docker rm cedar-nginx


