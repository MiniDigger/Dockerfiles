FROM java:8-alpine

ENV JAVA_ARGS "-Xmx2G"
ENV SPIGOT_ARGS ""
ENV PAPER_ARGS ""
VOLUME "/data"

ARG PAPER_URL=https://ci.destroystokyo.com/job/Paper/lastSuccessfulBuild/artifact/paperclip.jar

WORKDIR /data
ADD "${PAPER_URL}" /srv/paper.jar
RUN cd /srv &&\
	java -jar paper.jar --version &&\
	mv cache/patched*.jar paper.jar &&\
	rm -rf cache &&\
	chmod 444 /srv/paper.jar

ADD start.sh /usr/local/bin/paper
RUN chmod +x /usr/local/bin/paper

CMD ["paper"]
