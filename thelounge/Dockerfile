FROM node:8-alpine

ENV NODE_ENV production

ENV THELOUNGE_HOME "/var/opt/thelounge"
VOLUME "${THELOUNGE_HOME}"

# Expose HTTP.
ENV PORT 9000
EXPOSE ${PORT}

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["thelounge", "start"]
WORKDIR /var/opt/thelounge-source/

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

# Install text editors and git
RUN apt-get update && \
    apt-get install -y vim nano git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# install webpack
RUN yarn add --dev webpack webpack-dev-server && \
    yarn cache clean

# Install thelounge.
RUN git clone https://github.com/thelounge/thelounge.git . && \
    yarn install && \
    NODE_ENV=production yarn build && \
    rm -rf node_modules
