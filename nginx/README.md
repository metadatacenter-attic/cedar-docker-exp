To build this Docker container:

  docker build -t="cedar/nginx:0.1.0" .

To run:

  docker run -d -p 8080:80 
    -v <CEDAR source directory>:/srv/cedar 
    -v <Host SSL certificates>:/srv/certificates 
    --name cedar_nginx cedar/nginx:0.1.0 

e.g.,

  docker run -d -p 8080:80 
    -v /Users/moconnor/workspace/cedar:/srv/cedar 
    -v /Users/moconnor/workspace/conf/certificates/metadatacenter.net:/srv/certificates 
    --name cedar_nginx cedar/nginx:0.1.0 

To look at container logs:

  docker logs cedar_nginx

To remove container:

  docker rm cedar_nginx

To look at container ports:

  docker port cedar_nginx 

To test connectivity to Nginx:

  http://192.168.99.100:8080/

