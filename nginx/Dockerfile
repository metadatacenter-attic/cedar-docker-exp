# Version: 0.1.0

# TODO Need to pick specific version of CentOS
FROM centos:latest
MAINTAINER CEDAR Team "metadatacenter@gmail.com"

ENV CEDAR_HOME /srv/cedar
ENV CEDAR_HOME /srv/cedar
ENV CEDAR_APP_HOME ${CEDAR_HOME}/cedar-template-editor/app
ENV CEDAR_CERTIFICATES_PATH /srv/certificates

# Point yum to an Nginx repository
COPY nginx.repo /etc/yum.repos.d/nginx.repo

# Make CEDAR home directory
RUN mkdir -p ${CEDAR_HOME}

# Make CEDAR home the default work directory
WORKDIR ${CEDAR_HOME}

# Mount a volume containing the CEDAR code 
# Nginx is expecting an index.html file in the subdirectory ./cedar-template-editor/app
VOLUME [ ${CEDAR_HOME} ]

# Mount a volume containing the host SSL certificates
# The -h flag should be given to the container with a host matching the certificate
VOLUME [ ${CEDAR_CERTIFICATES_PATH} ]

#Install Nginx
RUN yum -y install nginx

# Copy Nginx configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Replace <HOSTNAME> in Nginx configuration file with $HOSTNAME
RUN sed -i -e "s|<HOSTNAME>|${HOSTNAME}|g" /etc/nginx/conf.d/default.conf

# Replace <CEDAR_APP_HOME> in Nginx configuration file with $CEDAR_APP_HOME
RUN sed -i -e "s|<CEDAR_APP_HOME>|${CEDAR_APP_HOME}|g" /etc/nginx/conf.d/default.conf

# Replace <CEDAR_CERTIFICATES_PATH> in Nginx configuration file with $CEDAR_CERTIFICATES_PATH
RUN sed -i -e "s|<CEDAR_CERTIFICATES_PATH>|${CEDAR_CERTIFICATES_PATH}|g" /etc/nginx/conf.d/default.conf

# Run Nginx
ENTRYPOINT "/usr/sbin/nginx" -g "daemon off;"

# Expose port 443
EXPOSE 443

# Test running container with curl https://<host>
