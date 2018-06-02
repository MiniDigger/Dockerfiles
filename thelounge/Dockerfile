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
RUN apk update && \
    apk upgrade && \
    apk add --no-cache bash nano git openssh && \
    rm -rf /var/lib/apt/lists/*


# Install thelounge.
RUN git clone https://github.com/thelounge/thelounge.git . && \
    yarn install && \
    NODE_ENV=production yarn build && \
    npm cache clean --force && \
    yarn cache clean
