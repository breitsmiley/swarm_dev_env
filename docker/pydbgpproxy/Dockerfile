FROM python:2.7.14-alpine3.7

ENV RD_VERSION="11.0.2" RD_BUILD="90813"

RUN wget -O PythonRemoteDebugging.tar.gz http://downloads.activestate.com/Komodo/releases/$RD_VERSION/remotedebugging/Komodo-PythonRemoteDebugging-$RD_VERSION-$RD_BUILD-linux-x86_64.tar.gz \
    && mkdir -p /usr/local/PythonRemoteDebugging \
    && tar -xzC /usr/local/PythonRemoteDebugging --strip-components=1 -f PythonRemoteDebugging.tar.gz \
    && rm PythonRemoteDebugging.tar.gz \
    && ln -s /usr/local/PythonRemoteDebugging/pydbgpproxy /usr/local/bin/pydbgpproxy
ENV PYTHONPATH /usr/local/PythonRemoteDebugging/pythonlib

EXPOSE 9000 9001

CMD ["pydbgpproxy", "-d", "127.0.0.1:9000", "-i", "0.0.0.0:9001"]


# FROM alpine:3.7

# LABEL "Maintainer"="THE ICONIC ENGINEERING TEAM <engineering@theiconic.com.au>"

# RUN apk --update --no-cache add \
#     python \
#     py2-pip

# RUN pip2 install --upgrade pip && \
#     pip2 install --upgrade komodo-python-dbgp

# ADD docker-dbgp-entrypoint.sh /usr/local/bin/docker-dbgp-entrypoint

# RUN chmod +x /usr/local/bin/docker-dbgp-entrypoint


# ENTRYPOINT ["docker-dbgp-entrypoint"]

# ENV IDE_PORT=0.0.0.0:9001
# ENV DEBUG_PORT=0.0.0.0:9000

# CMD pydbgpproxy -i ${IDE_PORT} -d ${DEBUG_PORT}

# EXPOSE 9000 9001


# A Light DBGp Proxy
# This is basically the same old Dbgpproxy as demonstrated by christian-blades-cb's repository, but redesigned to bring more flexibility delivered on a lighter Alpine image instead of the amazing Ubuntu image. Much like Christian's approach, this runs off the py-dbgpproxy. Please refer to The ActiveState Komodo DBGP server for more information.

# How to use
# By default, some running parameters are set and can be overwritten with environment variables if such need arises.

# Example:

# docker run -d -e IDE_PORT=0.0.0.0:9008 -e DEBUG_PORT=0.0.0.0:9000 theiconic/lite-dbgp-proxy
# Environment variables include:

# IDE_PORT: This represents socket on which DBGp service should listen for incoming requests
# DEBUG_PORT: This represents socket on which DBGp service sends out DBGp requests to DBGp servers. Eg. server running xDebug
# NOTE that XXXX_PORT values should always be given as socket values (ip:port)

# Usage in a docker compose could be:

# version: '2'
# services:
#     web:
#         image: php-with-xdebug
#         network:
#         networks:
#             web_net:
#                 ipv4_address: 172.19.111.20
#         # Other configs

#     dbgp-proxy:
#         image: theiconic/lite-dbgp-proxy
#         environment:
#             - IDE_PORT=172.16.0.0:9001
#             - DEBUG_PORT=172.19.0.0:9000
#         network:
#             - web_net
#             - local_net
# Point your IDE to 172.16.0.1:9001, assuming the IP address of dbgp-proxy is 172.16.0.1.
# Generally you'll allow this service to listen on 0.0.0.0:9001 and push to 0.0.0.0:9000. The example above just shows you can alter as required to avoid network overlapping.

# Contributors
# Yinka Asonibare - yinka
# License
# Released under the MIT License. See the license file for more details.