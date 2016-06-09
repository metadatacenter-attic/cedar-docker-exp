CEDAR Nginx Docker Container
===========================

To build this Docker container:

    docker build -t="cedar/nginx:0.1.0" .

To run:

    docker run -d 
      -h <host name> -p 443:443 
      -v <CEDAR source directory>:/srv/cedar 
      -v <host SSL certificates>:/srv/certificates 
      --name cedar_nginx cedar/nginx:0.1.0 

e.g.,

    docker run -d \
      -h cedar.metadatacenter.net -p 443:443 \
      -v /Users/moconnor/workspace/cedar:/srv/cedar \
      -v /Users/moconnor/workspace/conf/certificates/metadatacenter.net:/srv/certificates \
      --name cedar_nginx cedar/nginx:0.1.0 

To see that the container is running:

    docker ps

Use DOCKER_HOST environment variable to find the Docker server IP address and map the host name to this IP address in ```/etc/hosts/```.

To test connectivity to Nginx server in container:

    curl -i -vvv https://<host name>/

To look at the container logs:

    docker logs cedar_nginx

To look at container ports:

    docker port cedar_nginx 

To create a shell inside the running container:

    docker exec -it cedar_nginx /bin/bash

To look at Nginx log when inside container:

    tail -f /var/log/nginx/access.log
    tail -f /var/log/nginx/error.log

To stop the container:

    docker stop cedar_nginx

To remove container:

    docker rm cedar_nginx


