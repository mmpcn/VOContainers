# VOContainers

Testing docker containers for VO Applications.
Ideas to improve it are welcome.

To build the containers:

docker build -t splat splat_docker
docker build -t topcat topcat_docker
docker build -t sampbridge sampbridge_docker

To make the GUI run (in a Mac. Needs info/testing for Linux and Windows):

install XQuartz
install scout
run socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:"$DISPLAY"

To be able to access files from and save to the host machine (config, datafiles to open, ...)

mkdir <path-to-splathome>

put data you want to access there; from the container, save data in /root/

How to run SPLAT, TOPCAT in Docker:

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 -t mmpcn/splat:splat

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 -t mmpcn/splat:topcat
How to make them communicate through SAMP:

the containers have to be in the same network:

docker network create samp-network
Run SPLAT, TOPCAT in this network

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0  --network samp-network -t mmpcn/splat:splat

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 --network samp-network -t mmpcn/splat:topcat
Run sampbridge container in same network (it has to be started after Topcat and SPLAT):

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 --network samp-network -t mmpcn/splat:sampbridge
Using a sampbridge (jsamp) to make possible for the application containers to
communicate via SAMP

Docker repository: https://hub.docker.com/r/mmpcn/splat

TOPCAT link: http://www.star.bris.ac.uk/~mbt/topcat/
SPLAT-VO link: http://www.g-vo.org/pmwiki/About/SPLAT
JSAMP link: http://www.star.bristol.ac.uk/~mbt/jsamp/



To make it the GUI run (in a Mac):

install XQuartz

install scout

run socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:"$DISPLAY"

To be able to access files from and save to the host machine (config, datafiles to open, ...)

mkdir

put data you want to access there; from the container, save data in /root/

How to run SPLAT, TOPCAT in Docker:

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 -t mmpcn/splat:splat

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 -t mmpcn/splat:topcat
How to make them communicate through SAMP:

the containers have to be in the same network:

docker network create samp-network
Run SPLAT, TOPCAT in this network

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0  --network samp-network -t mmpcn/splat:splat

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 --network samp-network -t mmpcn/splat:topcat
Run sampbridge container in same network (it has to be started after Topcat and SPLAT):

docker run -v /tmp/.X11-unix:/tmp/.X11-unix -v path-to-splathome:/root -e DISPLAY=$(ipconfig getifaddr en0):0 --network samp-network -t mmpcn/splat:sampbridge
