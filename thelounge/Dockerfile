FROM node:9

ENV NODE_ENV development

ENV THELOUNGE_HOME "/var/opt/thelounge"
VOLUME "${THELOUNGE_HOME}"

ENV PORT 9000
EXPOSE ${PORT}

ENTRYPOINT ["yarn", "start"]
WORKDIR /var/opt/thelounge-source/

# Install text editors and git
RUN apt-get update && \
    apt-get install -y vim nano git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install thelounge and my theme
RUN git clone https://github.com/thelounge/thelounge.git . && \
    yarn install && \
    yarn build && \
    node index install thelounge-theme-mininapse