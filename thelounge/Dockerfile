FROM node:8

ENV NODE_ENV production

ENV THELOUNGE_HOME "/var/opt/thelounge"
VOLUME "${THELOUNGE_HOME}"

# Expose HTTP.
ENV PORT 9000
EXPOSE ${PORT}

CMD ["yarn", "start"]
WORKDIR /var/opt/thelounge-source/

# Install text editors and git
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install bash nano git && \
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

# install webpack
RUN npm install -g webpack yarn && \
    npm cache clean --force

# Install thelounge.
RUN git clone https://github.com/thelounge/thelounge.git . && \
    yarn install && \
    NODE_ENV=production yarn build && \
    npm cache clean --force && \
    yarn cache clean
