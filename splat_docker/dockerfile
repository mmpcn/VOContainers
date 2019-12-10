FROM openjdk:8
RUN apt-get update; apt-get -y install libxrender1 libxtst6 libxi6
COPY . /usr/splat
WORKDIR /usr/splat 
RUN mkdir bin
RUN wget -O /tmp/splat-vo-for-docker.tgz http://soft.g-vo.org/splat-beta/splat-vo-for-docker.tgz
RUN tar xzf /tmp/splat-vo-for-docker.tgz 
RUN rm /tmp/splat-vo-for-docker.tgz 
CMD ["/usr/splat/startsplat"]
