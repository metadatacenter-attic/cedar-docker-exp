# Version: 0.1.0

# TODO Need to pick specific version of CentOS
FROM centos:latest
MAINTAINER CEDAR Team "metadatacenter@gmail.com"

# Point yum to an Nginx repository
COPY nginx.repo /etc/yum.repos.d/nginx.repo

# Make CEDAR home directory
RUN mkdir -p /srv/cedar

# Make CEDAR home the default work directory
WORKDIR /src/cedar

# Mount a volume containing the host SSL certificate 
# The -h flag should be given to the container with a host matching the certificate
VOLUME [ "/srv/certificates/" ]

# Mount a volume containing the CEDAR code 
# Nginx is expecting an index.html file in the subdirectory ./cedar-template-editor/app
VOLUME [ "/srv/cedar/" ]

#Install Nginx
RUN yum -y install nginx

# Copy Nginx configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Replace <HOSTNAME> in Nginx configuration file with actual host name
RUN sed -i -e "s/<HOSTNAME>/${HOSTNAME}/g" /etc/nginx/conf.d/default.conf

# Run Nginx
ENTRYPOINT "/usr/sbin/nginx" -g "daemon off;"

# Expose port 443
EXPOSE 443

# Test running container with curl https://<host>
