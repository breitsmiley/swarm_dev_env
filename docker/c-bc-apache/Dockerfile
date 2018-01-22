FROM httpd:2.4.29-alpine

# for docker-compose mode
# COPY /docker/c-bc-apache/httpd.conf  /usr/local/apache2/conf/httpd.conf
# COPY /docker/c-bc-apache/httpd-default.conf  /usr/local/apache2/conf/extra/httpd-default.conf
# COPY /docker/c-bc-apache/app-sf.conf  /usr/local/apache2/conf/extra/app-sf.conf


# Copy project files as late as possible
WORKDIR /usr/src/bc/public
COPY /apps/book-collector/public ./