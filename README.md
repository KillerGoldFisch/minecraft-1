# minecraft

A docker repository for setting up a minecraft server with Remote Toolkit.


## Building

Running this will build you a docker image with the latest version of both
docker-minecraft and Minecraft itself.


    docker build -t centzilius/minecraft git://github.com/killergoldfisch/minecraft-1.git


## Running 

Running the first time will set your port to a static port of your choice so
that you can easily map a proxy to. If this is the only thing running on your
system you can map the port to 25565 and no proxy is needed. i.e.
`-p=25565:25565` . If you want to enable the query protocol you need
to add another -p=25565:25565/udp to forward the UDP protocol on the
same port as well. Same goes with the Telnet connection of the Toolkit
`-p=25561:25561`
Also be sure your mounted directory on your host machine is
already created before running `mkdir -p /mnt/minecraft`.

    docker run -d=true -e UID=1000 -e USER=user -e PASS=pass -p=25565:25565 -p=25561:25561 -v=/mnt/minecraft:/data killergoldfisch/minecraft /start

From now on when you start/stop docker-minecraft you should use the container id
with the following commands. To get your container id, after you initial run
type `sudo docker ps` and it will show up on the left side followed by the
image name which is `centzilius/minecraft:latest`.

    docker start <container_id>
    docker stop <container_id>

It might be safer to stop the minecraft server from console.

### Notes on the run command

 + `-v` is the volume you are mounting `-v=host_dir:docker_dir`
 + `centzilius/minecraft` is simply what I called my docker build of this image
 + `-d=true` allows this to run cleanly as a daemon, remove for debugging
 + `-p` is the port it connects to, `-p=host_port:docker_port`
