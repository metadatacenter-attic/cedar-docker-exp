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
VOLUME [ "/srv/certificates/" ]

# Mount a volume containing the CEDAR code 
VOLUME [ "/srv/cedar/" ]

#Install Nginx
RUN yum -y install nginx

# Copy Nginx configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Run Nginx
ENTRYPOINT "/usr/sbin/nginx" -g "daemon off;"

# Expose port 80
EXPOSE 80

