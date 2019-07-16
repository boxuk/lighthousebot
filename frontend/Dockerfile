FROM node:10-slim

RUN apt-get update --fix-missing && apt-get -y upgrade
RUN apt-get -y install vim

ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 /usr/local/bin/dumb-init
RUN chmod +x /usr/local/bin/dumb-init

COPY package.json .
RUN npm i --production

COPY lighthouse-ci.js /
COPY server.js /
RUN chmod +x /server.js

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

RUN groupadd --system lighthouse && \
    useradd --system --create-home --gid lighthouse lighthouse && \
    chown --recursive lighthouse:lighthouse /home/lighthouse

USER lighthouse

EXPOSE 8080

ENTRYPOINT ["dumb-init", "--", "/entrypoint.sh"]
