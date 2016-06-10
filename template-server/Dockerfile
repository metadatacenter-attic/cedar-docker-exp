# Version: 0.1.0

# TODO Need to pick specific version of CentOS
FROM centos:latest
MAINTAINER CEDAR Team "metadatacenter@gmail.com"

ENV CEDAR_HOME /srv/cedar

# Make CEDAR home directory
RUN mkdir -p ${CEDAR_HOME}

# Make CEDAR home the default work directory
WORKDIR ${CEDAR_HOME}

RUN yum -y install java

RUN yum -y install unzip

COPY cedar-template-server-play-0.1.0-dist.zip $CEDAR_HOME

RUN ls -al
RUN unzip -xfzv cedar-template-server-play-0.1.0-dist.zip 

WORKDIR ${CEDAR_HOME}/cedar-template-server-play-0.1.0



