# Docker

Docker

commands: https://www.mygreatlearning.com/blog/top-essential-docker-commands/

docker run [image] >> pull image and run container

docker ps >> list executing contar (-a to list the stopped)

docker exec -it [id] bash >> execute iterative (-it) the command bash inside the container
*Note: With this command, you will "get inside" the container and execute a bash, that you can do anything. But, if for exemple,
you create a .txt file or anything like that, it will exist just inside the container because the docker isolation.

docker pause [id] >> to pause the container. You won't be abtle to do anything with the container, but  you can unpause later
it's a less agressive approach than just kill the processes with docker stop [id].

docker rm [id] >> remove container

docker run -d dockersamples/static-site >> run a static site from docker sample. USE -d TO NOT FREEZE THE PROMPT

docker run -d -P dockersamples/static-site >> -P will map docker port to some local port
docker run -d -p 8080:80 dockersamples/static-site >> same as before, but you choose the port (8080 is the host and 80 is the container)

docker port [id] >> see the container ports connection (you can localhost:port in browser to see the container)

docker run -it --name ubuntu2 ubuntu bash >> name container as ubuntu2
-------------------------------------------------------------------------------------------------------------------------------------------------
Create Image (Node exemple)

Create Dockerfile in project file

https://docs.docker.com/engine/reference/builder/ >> docker documentantion for instructions

Check on gitHub, but here is the exemple:
---------------------
FROM node:14             ## node version 14 from dockerHub
WORKDIR /app-node        ## defining the diretory in container
EXPOSE 3000              ## setting port to run  
COPY . .                 ## first point is the actual local diretory and second the workid (container)
RUN npm install          ## run dependencies
ENTRYPOINT npm start     ## start 
-----------------------

cd project file

docker build -t joao/app-node:1.0 . >> build image, -t to name "joao/..." and don't forget the point to show the actual directory

docker run -d -p 8081:3000 joao/app-node:1.0

defining port with the application:

create the variable in the application (for exemple PORT)
and in the docker file:
---------------------
FROM node:14
WORKDIR /app-node
ARG PORT=6000     ## inside image build
ENV PORT=$PORT    ## inside the container
EXPOSE $PORT
COPY . .
RUN npm install
ENTRYPOINT npm start
-----------------------

docker images  >> see all images

deploy on dockerhub: 

docker login -u joaofaquineli

docker tag joao/app-node:1.0 joaofaquineli/app-node:1.0

docker push joaofaquineli/app-node:1.0
---------------------------------------------------------------
Using volumes (persistence, connect your localhost with container)

bind (mount):

docker run -it -v C:/Docker/docker-volume:/app ubuntu bash >> select local path (C:/Docker/docker-volume)
cd app
touch test-file.txt >> create a file in container and localhost path

check docker file to see how to do it with --mount instead -v (recommended)

Volume (recommended):

docker volume create my-volume
docker run -it -v my-volume:/app ubuntu bash

the difference is that this volume is saved in some difficult place in SO :)

TMPFS (temporary volumes, just for linux if you wanna know more, search for it :) )

docker run -it -tmpfs=/app ubuntu bash
--------------------------------------------------------------------------------------------------
Networks

docker inspect [id] to inspect network, ipAdress and other informations




