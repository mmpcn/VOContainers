FROM openjdk:8
RUN apt-get update; 
COPY . /usr/sampbridge
WORKDIR /usr/sampbridge
RUN mkdir bin
RUN wget -O bin/jsamp.jar  http://www.star.bristol.ac.uk/~mbt/jsamp/jsamp-1.3.7.jar
CMD ["/usr/sampbridge/sampbridge"]
