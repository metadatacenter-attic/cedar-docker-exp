CEDAR Template Server Container
===============================

This Docker container runs CEDAR's template server. 

#### Building and Running

To build this Docker container:

    docker build -t="metadatacenter/cedar-template-server:0.1.0" .

To run:

    docker run -d 
      -h <host name> -p 443:443
      -v <CEDAR source directory>:/srv/cedar 
      -v <host SSL certificates>:/srv/certificates 
      --name cedar-nginx metadatacenter/cedar-template-server:0.1.0
