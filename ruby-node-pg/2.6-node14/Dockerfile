# GENERATED FILE, DO NOT MODIFY!
# To update this file please edit the relevant template and run the generation
# task `rake generate:ruby-node-pg`

FROM instructure/ruby-passenger:2.6
MAINTAINER Instructure

USER root

# install postgres client
RUN apt-get update \
    && apt-get install -yqq postgresql-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && gem update --system

ENV YARN_VERSION latest

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list \
  && apt-get update \
  && apt-get install -y --no-install-recommends yarn \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/

COPY yarn-private /usr/local/bin

ENV NODE_VERSION 14
ENV NPM_VERSION latest

RUN mkdir -p /usr/src/app && chown docker:docker /usr/src/app
WORKDIR /usr/src/app

RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | apt-key add - && \
  echo "deb https://deb.nodesource.com/node_14.x bionic main" > /etc/apt/sources.list.d/nodesource.list && \
  apt-get update && \
  apt-get install -y --no-install-recommends nodejs && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/ && \
  npm install -g "npm@$NPM_VERSION" && \
  npm cache clean --force

COPY npm-private /usr/local/bin


USER docker
