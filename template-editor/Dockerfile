#
# NOTE Not yet set up for HTTPS
#
# This sets up the CEDAR front end using the development server on port 4200,
# with the live reload port on 35729. The CEDAR_HOST variable passed to container
# indicates the host running the CEDAR back end.
# 
# To build this Docker container:
#
#  docker build -t="metadatacenter/cedar-template-editor:0.5.6" .
#
# To run:
#
# docker run -d -p 4200:4200 -p 35729:35729 -e CEDAR_HOST='staging.metadatacenter.net' \
#   -e CEDAR_TEST_USER='XXX' -e CEDAR_TEST_PASSWORD='XXX' \
#   --name cedar-template-editor metadatacenter/cedar-template-editor:0.5.6
#
# To access the web application go to a browser and enter:
#
#   http://${DOCKER_HOST}:4200
#
# To look at logs:
#
#  docker logs cedar-template-editor
#
# To kill:
#
#  docker kill cedar-template-editor
#
# To remove:
#
#  docker rm cedar-template-editor

# TODO Need to pick specific version of CentOS
FROM centos:latest
MAINTAINER CEDAR Team "metadatacenter@gmail.com"

ENV CEDAR_HOME /srv/cedar
ENV CEDAR_TEMPLATE_EDITOR_HOME ${CEDAR_HOME}/cedar-template-editor/

ENV CEDAR_PROFILE local
ENV CEDAR_ANALYTICS_KEY false
ENV CEDAR_SELENIUM_SERVER_JAR 2.50.1-server.jar
ENV CEDAR_CHROME_DRIVER 2.21-x64-chromedriver

# Make CEDAR appplication home directory
RUN mkdir -p ${CEDAR_TEMPLATE_EDITOR_HOME}

#Copy code 
COPY app ${CEDAR_TEMPLATE_EDITOR_HOME}/app/
COPY tests ${CEDAR_TEMPLATE_EDITOR_HOME}/tests/
COPY bower.json gulpfile.js karma.conf.js package.json protractor.config.js robots.txt ${CEDAR_TEMPLATE_EDITOR_HOME}

# Make CEDAR home the default work directory
WORKDIR ${CEDAR_TEMPLATE_EDITOR_HOME}

# Instead of following can simply copy the source node_modules directory. Gulp install still needed.

#Install npm, gulp
RUN yum -y install epel-release # Needed to install npm
RUN yum -y install npm
RUN npm install
RUN npm install -g gulp

# Run 
ENTRYPOINT gulp

# Expose ports main development port and live reload port
EXPOSE 4200 35729
