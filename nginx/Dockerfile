# Version: 0.1.0
FROM centos:latest
MAINTAINER CEDAR Team "metadatacenter@gmail.com"

# Alternatively, point yum to an Nginx repository
COPY nginx.repo /etc/yum.repos.d/nginx.repo

#Install Nginx
RUN yum -y install nginx

# Run Nginx
ENTRYPOINT "/usr/sbin/nginx" -g "daemon off;"

# Expose port 80
EXPOSE 80

