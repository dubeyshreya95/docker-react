# Docket notes
challenges with running s/w
searching for helpful documentation
where it is ? Path?
Starting/Stoping
service registration
licenses
installing and running dependencies
security and sandboxing
breaking changes: Os updates , shared library updates

## Docker vs. VM – where is the difference?

They are similar in that they both provide isolated environments – they can both be used to package up and distribute software. However, containers are typically much smaller and faster, which makes them a much better fit for fast development cycles and microservices. The trade-off is that containers don’t do true virtualization; you can’t run a windows container on a Linux host for example. It’s also worth pointing out that several companies are trying to create tooling around slimmed down VMs to try to get the best of both worlds e.g. hyper.sh, Intel Clear Containers and vSphere Integrated Containers.

 VM’s are built for applications that are usually more static and don’t change very often. Whereas containers are more flexible and make it possible to easily and frequently update your containers. 

 
Containers provide:
process isolation,
file system isolation,1
network isolation, there is virtual network adapter affiliated with each container
In windows container, the registry is isolated each container has its own
On linus there are namespaces that provide isolation


## Generating a react app:
   ### `npx create-react-app frontend`

It is a good practice to use two docker files Dockerfile.dev for developemnt and testing while Dockerfile for production .

Building a docker image:     `docker build .`  this command will look for Dockerfile in the project but if we want to run image from a custom dockerfile use command: `docker build -f Dockerfile.dev .`

To run image: `docker run image-id`

To map port to container port: `docker run -p port1:port2 image-id`

Setting up the volumes:  `docker run -p -v /app/node-modules -v $(pwd):/app`
through this command we are mapping all the files and folder in current directory with app folder inside the container. With this any changes made on our local will get prpagated to our running container without rebuilding the image.

docker-compose.yml: whole pupose of docker compose is to make docker run easier. Docker run command can beacome really bulky as we keep on adding all the setting needed ro run an image. like port mapping, setting up volumes etc. WIth this file we will only need to run : `docker-compose up`

COPY ./ ./   this is not needed if we are setting up the volume.


To run tests: `docker run -it image-id npm run test`

`-it` : to attach terminal to the created container to pass inputs

`npm run test` : override command

`docker-compose up --build`   to rebuild

`docker exec -it image-id new command` : exec command is used to execute a second command inside the container other than the default command.

by default we only connect  to stdout of the docker container but to provide any inputs we will need to attch stdin, we can do so by appendind   `-it`

`docker ps` to get list of all running containers

`-it`  to add terminal to a container(add this if you want to run containers on the foreground and want to stop the container when done)

`--name` to give a name to container

`docker stop (container-id)`  some cases even after we stop the container we will still see it when we docker ps specially in case of web server beacuse there is a primary application running inside web server so we will need to syop that too.we can sue command: `docker run -p p1:p2 -it imageid `. -it will allow to stop the processes running inside the container.

`docker ispect container-name/id` gives a whole bunch of info about a container including ip address.


Traditinal sw/ docker

downloading s/w zip file, msi installer - docker pull image
installing - docker create
start s/w - docker start
stop s/w - docker stop
uninstall s/w - docker rm
              - docker run (do all the above steps with one command)


















