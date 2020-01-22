# VOContainers

Testing docker containers for VO Applications, 
using a sampbridge (jsamp) to make possible for the application containers to
communicate via SAMP

Docker repository: 

https://hub.docker.com/r/mmpcn/splat

https://hub.docker.com/r/mmpcn/topcat

https://hub.docker.com/r/mmpcn/sampbridge



TOPCAT link: http://www.star.bris.ac.uk/~mbt/topcat/

SPLAT-VO link: http://www.g-vo.org/pmwiki/About/SPLAT

JSAMP link: http://www.star.bristol.ac.uk/~mbt/jsamp/

Ideas to improve it are welcome.

To build the containers:

	docker build -t splat splat_docker

	docker build -t topcat topcat_docker

	docker build -t sampbridge sampbridge_docker


* To be able to access files from and save to the host machine (config, datafiles to open, ...)

	mkdir <path-to-common-directory>

put data you want to access there; from the container, save data in /root/


* To make the GUI run:
in a MacOs machine, you need to install a X server (XQuartz)
install XQuartz
Open XQuartz Preferences -> Security, check ‘Allow connections from network clients’
on a shell window, type 
        xhost + 127.0.0.1
You'll need to pass the ip address of the host machine to the container when you run it.
Depending on the OS, there are several ways to get the ip address:

MAC: HOST_IP=$(ipconfig getifaddr en0)
LINUX: HOST_IP=$(hostname -I | awk '{print $1}')
WINDOW: ??

How to run SPLAT, TOPCAT in Docker:

To communicate using SAMP, they need to be in the same network (needs to be done only once):

	docker network create samp-network

Run SPLAT, TOPCAT in this network

	docker run -v <path-to-common-directory>:/root  -e DISPLAY=$HOST_IP:0  --network samp-network -t splat

	docker run -v <path-to-common-directory>:/root  -e DISPLAY=$HOST_IP:0  --network samp-network -t topcat

 Run sampbridge container in same network (it has to be started after Topcat and SPLAT):

	docker run -v <path-to-common-directory>:/root --network samp-network -t sampbridge
