FROM node:8.9
MAINTAINER lordsputnik+docker@metabrainz.org

# Avoid warnings during subsequent apt-get install
RUN apt-get update && apt-get install -y apt-utils

RUN apt-get install -y postgresql-client-9.4

WORKDIR /apps
RUN git clone --recursive https://github.com/bookbrainz/bookbrainz-site.git

ARG MB_OAUTH_CLIENT_ID
ARG MB_OAUTH_CLIENT_SECRET
ARG MB_OAUTH_CALLBACK_URL
ARG SESSION_SECRET
ARG ENABLE_INFLUX

COPY ./config.json /apps/bookbrainz-site/config/config.json
COPY ./scripts/RewriteConfig.sh /RewriteConfig.sh
WORKDIR /apps/bookbrainz-site/config
RUN /RewriteConfig.sh

WORKDIR /apps/bookbrainz-site

COPY ./scripts/CreateDB.sh /CreateDB.sh
COPY ./scripts/Start.sh /Start.sh
COPY ./scripts/Debug.sh /Debug.sh

CMD ["/Debug.sh"]
