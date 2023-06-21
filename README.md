# Complete-Docker-Course---From-BEGINNER-to-PRO-Learn-Containers-

https://www.youtube.com/watch?v=RqTEHSBrYFw 

Part 1
History and Motivation

What is a container ?
A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application

Evolution of Virtualization

Host (Physical) Machine
Application #1    Application #2
Binaries / Libraries 
Operating System 
Physical Hardware

Bare Metal

Hellish dependencies conflicts 
Low utilization efficiency
Large blast radius
Slow start up and shut down speed ( minutes )
Very slow provisioning and decommissioning ( hours to days )

Virtual Machine

Host (Physical) Machine
Virtual Machine #1    Virtual Machine#2
Application #1    Application #2
Binaries / Libraries 
Operating System 
Virtual Hardware
Hipervisor 
Operating System ( “type 2” hypervisor ) 
Physical Hardware

Virtual Machines

No dependency conflicts
Better utilization efficiency 
Small blast radius
Faster start up and shutdown ( minutes ) 
Faster provisioning and decommissioning ( minutes ) 

Containers 

Physical System
Virtual Machine
Desktop Container Platforms
Container Runtimes
No dependency conflicts
Even better utilization efficiency 
Small blast radius
Even faster start up and shutdown ( seconds )
Lightweight enough to use in development 

Virtual Machines more Containers 

Host (Physical) Machine more Orchestrators 
Virtual Machine # 1                              Virtual Machine#2
Container # 1 Container # 2                 Container #3 Container #4
Application # 1    Application # 2          Application # 3   Application # 4
Binaries / Libraries                                Binaries / Libraries 
Container Runtime                                Container Runtime
Operating System                                 Operating System
Virtual Hardware                                  Virtual Hardware
                             Hipervisor 
                          Physical Hardware 
Kubernetes 
Docker
…

Part 2
Technology Overview

Linux Building Blocks
Namespaces
Control Groups 
Union Filesystem

Namespaces



cgroups

Union Filesystem



Docker Architecture



Part 3
Installation and Set up

https://docs.docker.com/engine/install/

Docker Image
“ Pull the image from dockerhub
Run an container from it 
Provider custom commands ”

Docker UI
MacOs Prompt
> docker
> docker run docker/whalesay cowsay “Hey Team”
> docker run - -env POSTGRES_PASSWORD=foobarbaz - -publish 5432:5432 postgres:15.1-alpine

pgadmin 4
docker database
Servers
docker
Databases
Schemas
Query Tool
Query         Query History
SELECT * FROM information_schema.tables
Data Output
table_catalog    table_schema    table_name    table_type
postgre              pg_catalog         pg_statistic  BASE TABLE  
…

Part 4
Using 3rd Party Containers

DockerHub
Container Regitry ( Docker )
https://hub.docker.com/

Understanding Data within Containers



Installing Dependencies 

Visual Studio Code
Terminal 
# Create a container from the ubuntu image
> docker run - -interactive - -tty - -rm ubuntu:22.04
#Try to ping google.com 
# ping google.com -c 1
root@ddc121160489:/# ping google.com -c 1
root@ddc121160489:/# 
# Install ping
apt update
apt install iputils - -ping
root@ddc121160489:/# apt update
root@ddc121160489:/# apt install iputils - -ping
Do you want to continue ? [Y/n] y
root@ddc121160489:/# ping google.com -c 1
root@ddc121160489:/# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run - -interactive - -tty - -rm ubuntu:22.04
root@6461f6598336:/# ping
bash: ping: command not found
root@6461f6598336:/# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run - -interactive - -tty - -name my-ubuntu-container ubuntu:22.04
root@6461f6598336:/# 
# Install and use Ping
apt update
apt install iputils - -ping - -yes
ping google.com -c 1
exit
root@6461f6598336:/# apt update
apt install iputils - -ping - -yes
root@6461f6598336:/# ping google.com -c 1
root@6461f6598336:/# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker ps -a
CONTAINER ID IMAGE           COMMAND CREATED STATUS PORTS   
12cca75102fb    ubuntu:22.04  “/bin/bash”   41s            Exited (0) 13s ago
NAMES
my-unbuntu-container
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> 
# Restart the container and attach to running shell
docker start my-ubuntu-container
docker attach my-ubuntu-container 
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker start my-ubuntu-container
my-ubuntu-container
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker attach my-ubuntu-container 
root@12cca75102fb:/# ping google.com -c 1
root@12cca75102fb:/# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
>
# Build a container image with ubuntu image as base and ping installed
docker build - -tag my-ubuntu-image -<<EOF
FROM ubuntu:22.04
RUN apt update && apt install iputils-ping - -yes
EOF
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker build - -tag my-ubuntu-image -<<EOF
FROM ubuntu:22.04
RUN apt update && apt install iputils-ping - -yes
EOF
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> 
# Run a container based on that image
docker run -it - -rm my-ubuntu-image
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm my-ubuntu-image
root@73e9e782b29c:/# ping google.com -c 1
root@73e9e782b29c:/# exit 
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> 
# Create a container from the ubuntu image
docker run -it - -rm ubuntu:22.04
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm ubuntu:22.04
root@290af65514ae:/# mkdir my-data 
root@290af65514ae:/#  
# Make a directory and store a file in it 
echo “Hello from the container” /my-data/hello.txt 
root@290af65514ae:/# echo “Hello from the container” /my-data/hello.txt 
root@290af65514ae:/# cat my-data/hello.txt
Hello from the container !
root@290af65514ae:/# exit 
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm ubuntu:22.04
root@eac4a4841a5c:/# cat my-data/hello.txt
cat: /my-data/hello.txt: No such file or directory 
root@eac4a4841a5c:/# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
>
# Create a named volume 
docker volume create my-volume 
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker volume create my-volume 
my-volume
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> 
# Create a container and mount the volume into the container filesystem 
docker run -it - -rm - -mount source=my-volume, destination=/my/data ubuntu:22.04
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm - -mount source=my-volume, destination=/my/data ubuntu:22.04 5
root@c5ec08e330ad:/# mkdir my-data
mkdir: cannot create directory ‘my-data’: File exists
root@c5ec08e330ad:/# ls
bin   dev home lib32  libx32 mnt        opt   root sbin sys  usr
boot etc  lib       lib64 media my-data proc run  srv   tmv  var
root@c5ec08e330ad:/# echo “Hello from the container” /my-data/hello.txt 
root@c5ec08e330ad:/# cat my-data/hello.txt
Hello from the container !
root@c5ec08e330ad:/# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm - -mount source=my-volume, destination=/my/data ubuntu:22.04 5
root@1fcb3e6baa63:/# ls 
bin   dev home lib32  libx32 mnt        opt   root sbin sys  usr
boot etc  lib       lib64 media my-data proc run  srv   tmv  var
root@1fcb3e6baa63:/# cd my-data
root@1fcb3e6baa63:/my-data# ls
hello.txt
root@1fcb3e6baa63:/my-data# cat hello.txt
root@1fcb3e6baa63:/my-data# 
Hello from the container !
root@1fcb3e6baa63:/my-data# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
>
# Create a container that can access the Docker Linux VM 
# Pinning to the image hash ensures it is this SPECIFIC image and not an updated one #helps minimize the potential of a supply chain attack 
docker run -it - -rm - -privileged - -pid=host
justincormarck/nsenter1@sha256:5af0be5e42ebd55eea2c593e4622f810065c3f45bb805eaacf43f08f3d06ffd8    
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm - -privileged - -pid=host
justincormarck/nsenter1@sha256:5af0be5e42ebd55eea2c593e4622f810065c3f45bb805eaacf43f08f3d06ffd8    
/ # cd /var/lib/docker/volumes
/var/lib/docker/volumes # ls
/var/lib/docker/volumes # cd my-volume 
/var/lib/docker/volumes/my-volume # ls
_data
/var/lib/docker/volumes/my-volume # cd _data
/var/lib/docker/volumes/my-volume/_data # ls
hello.txt
/var/lib/docker/volumes/my-volume/_data # cat hello.txt
Hello from the container ! 
/var/lib/docker/volumes/my-volume/_data # exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> 
# Create a container that mounts a directory from the host filesystem into the container
docker run -it - -rm - -mount type=bind,source=“${PwD}”/my-data, destination=/my-data ubuntu 22.04
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm - -mount type=bind,source=“${PwD}”/my-data, destination=/my-data ubuntu 22.04
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> ls
README.md my-data readme-assets sample-data
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> ls my-data
hello.txt
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> rm -my-data/hello.txt
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> ls my-data
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm - -mount type=bind,source=“${PwD}”/my-data, destination=/my-data ubuntu 22.04
root@f096adf3fcde:/# ls
bin   dev home lib32  libx32 mnt        opt   root sbin sys  usr
boot etc  lib       lib64 media my-data proc run  srv   tmv  var
root@f096adf3fcde:/# cd my-data
root@f096adf3fcde:/my-data# echo “Blah blah” > hello.tx
root@f096adf3fcde:/my-data# ls
hello.txt 
root@f096adf3fcde:/my-data# cat hello.txt
Blah blah
root@f096adf3fcde:/my-data# exit
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> ls
README.md my-data readme-assets sample-data
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> cat my-data/hello.txt 
Blah blah 
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> vi my-data/hello.txt
Blah blah blah
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> cat my-data/hello.txt
Blah blah blah
~/d/c/d/devops-directive-docker-course/04-using-3rd-party-containers main !2 ?1
> docker run -it - -rm - -mount type=bind,source=“${PwD}”/my-data, destination=/my-data ubuntu 22.04
root@23889a8a0f1c:/# cat my-data/hello.txt
Blah blah blah
root@23889a8a0f1c:/# 

Part 5 
Demo Application 

Minimal 3 Tier web Application
React Front End
Two API Implementations:
Node.js (interpreted)
golang(compiled)
PostgreSQL Database

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> make run postgres ( Database running in the container )
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker ps
CONTAINER ID   IMAGE                      COMMAND  CREATED STATUS  PORTS   NAMES
3fc506785462      postgres:15.1-alpine
…
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> cd api-node
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main 
> ls
README.md   package.lock.json   src
healthcheck      package.json          test
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main 
> nvm ls
~/d/c/d/devops-directive-docker-course/05/api-node main 
> npm install
~/d/c/d/devops-directive-docker-course/05/api-node main 
> cd ..
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> make run-api-node
Exemple app Listenning on port 3000

Web Browser
localhost:3000
{
       “now”: “2023-02-18T21:14:30.3742”,
       “api”: “node”
}

~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> cd api-golang
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main 
> ls
README.md       go-workspace     go.sum            main.go
database              go.mod                healthcheck    test
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main 
> export GOPATH=$PwD/go-workspace
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main 
> go mod download
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main 
> cd .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang/go-workspace/pkg main 
> .cd .. 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang/go-workspace main ?1
> cd..
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main 
> go version
go version go.19.1 darwin/amd64
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main 
> cd ..
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
> ls
Makefile README.md api-golang api-node client-react readme…
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
> make run-api-golang
…
[GIN-debug] Listening and serving HTTP on 8080 

Web Browser
localhost:8080 
{
       “api”: “golang”,
       “now”: “2023-02-18T16:19:11.242914-05:00” 
}

~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
> nvm use 19.4
Now using node v19.4.0 (npm v9.2.0)
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
>  ls
Makefile README.md api-golang api-node client-react readme…
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
> cd client-react 
~/d/c/d/devops-directive-docker-course/05/client-react main ?1
> npm install
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
> ls
README.md     node-modules          public
index.html          package-lock.json     src
nginx.conf          package.json            vite.config.js
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main
> npm run dev
VITE v.4.8.4 ready in 215 ms
local: http//localhost:5173/
…

Web Browser 
localhost:5173

Hey Team !
     - - -
API: golang
Time from DB: 2023-02-18T16:24:51.572126-05:00
     - - -
API: node
Time from DB: 2023-02-18T21:24:51.574Z

Part 6
Building Container Images

Dockerfile
“A text document that contains all the commands a user could call on the command line to assemble an image”

Application
Start with operating system
Install language runtime
Install application dependencies
Set up execution environment 
Run application

Docker build
Dockerfile             + Build context
                             Source   Source   Source 
                             File 1      File 2      File 3
                                     .dockerignor

https://docs.docker.com/engine/reference/builder/ 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM ubuntu

RUN apt update && apt install nodejs npm -y

Visual Studio Code
Terminal
> api-node
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
>  ls
Makefile README.md api-golang api-node client-react readme…
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
>  api-node
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
>  ls
Dockerfile        healthcheck       package-lock.json   package.json   test
README.md   node-modules   package.json          src
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM ubuntu

RUN apt update && apt install nodejs npm -y

COPY . . 

RUN npm install 

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build .

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM ubuntu

RUN apt update && apt install nodejs npm -y

COPY . . 

RUN npm install 

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:0
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker image list
REPOSITORY            TAG         IMAGE ID           CREATED     SIZE 
api-node                      0.             b303c8542bcc    54s ago         974MB
…

https://hub.docker.com/_/node/ 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node

COPY . . 

RUN npm install 

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:1 .

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

COPY . . 

RUN npm install 

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:2 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker image ls
REPOSITORY            TAG         IMAGE ID           CREATED     SIZE 
api-node                      2.            d6c3bb57b02a    9s ago           212MB
api-node                      1             65fe9a7aa8c7     2m ago         1.03GB
api-node                      0             b303c8542bcc    5m ago          974MB
…
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

COPY package*.json ./

RUN npm install 

COPY . . 

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:3 .

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install 

COPY ./src . 

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:4 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install 

COPY ./src . 

CMD [“node”, “index.js”] 


Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:5 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
>  

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install 

USER node

COPY - -chow=node:node ./src . 

CMD [“node”, “index.js”] 

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:6 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

WORKDIR /usr/src/app

ENV NODE_ENV production

COPY package*.json ./

RUN npm ci - -only=production

USER node

COPY - -chow=node:node ./src . 

CMD [“node”, “index.js”] 

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:7 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
06-building-container-images
api-node
Dockerfile

Dockerfile
FROM node:19.6-alpine

WORKDIR /usr/src/app

ENV NODE_ENV production

COPY package*.json ./

RUN - -mount=type=cache, target=/usr/src/app/.npm\
       npm set cache /usr/src/app/.npm && \ 
       npm ci - -only=production

USER node

COPY - -chow=node:node ./src . 

EXPOSE 3000

CMD [“node”, “index.js”] 

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker build -t api-node:8 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> docker image ls
REPOSITORY            TAG         IMAGE ID           CREATED     SIZE 
api-node                      2.            d6c3bb57b02a    9s ago           212MB
api-node                      1             65fe9a7aa8c7     2m ago         1.03GB
api-node                      0             b303c8542bcc    5m ago          974MB
…
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
>  docker image ls |grep api-node
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-node main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang

WORKDIR /app

COPY . .

RUN go mod download 

CMD [“go”, “run”, “./main-go”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker image ls | grep api-golang
api-golang        latest             e2cbd5854460        11s ago   926MB
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:0 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
>

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang:1.19-alpine

WORKDIR /app

COPY . .

RUN go mod download 

CMD [“go”, “run”, “./main-go”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:1 .
api-golang                                  1                   945c0e2f3d9a       6s ago                 502MB
api-golang                                  0                   e2cbd5054460      About a m ago    926MB
api-golang                                  latest            e2cbd5054460       About a m ago    926MB  
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang:1.19-alpine

WORKDIR /app

COPY . .

RUN go mod download 

RUN go build -o api-golang 

CMD [“/api-golang”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:2 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
>

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang:1.19-alpine

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download 

COPY . .

RUN go build -o api-golang 

CMD [“/api-golang”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:3 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> 
https://hub.docker.com/_/scratch 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang:1.19-buster as build

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download 

COPY . .

RUN go build \
      -ldflags=“-linknode external -extldflags -static” \
      -tags netgo \
      -o api-golang
###
FROM scratch 

COPY - -from=build /app/api-golang api-golang

CMD [“/api-golang”]

Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:4 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang:1.19-buster as build

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download 

COPY . .

RUN go build \
      -ldflags=“-linknode external -extldflags -static” \
      -tags netgo \
      -o api-golang
###
FROM scratch 

ENV GIN_MODE release 

COPY - -from=build /app/api-golang api-golang

EXPOSE 8080

CMD [“/api-golang”]

Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:5 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
api-golang
Dockerfile

Dockerfile
FROM golang:1.19-buster as build

WORKDIR /app

COPY go.mod go.sum ./

RUN - -mount=type=cache, target=/go/pkg/mod \
       - -mount=type=cache, target=/root/.cache/go-build \ 
       go mod download

COPY . .

RUN go build \
      -ldflags=“-linknode external -extldflags -static” \
      -tags netgo \
      -o api-golang
###
FROM scratch 

ENV GIN_MODE release 

COPY - -from=build /app/api-golang api-golang

EXPOSE 8080

CMD [“/api-golang”]

Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang:6 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM golang:1.19-buster as build

WORKDIR /app

RUN useradd -u 1001 nonroot

COPY go.mod go.sum ./

RUN - -mount=type=cache, target=/go/pkg/mod \
       - -mount=type=cache, target=/root/.cache/go-build \ 
       go mod download

COPY . .

RUN go build \
      -ldflags=“-linknode external -extldflags -static” \
      -tags netgo \
      -o api-golang
###
FROM scratch 

ENV GIN_MODE release 

COPY - -from=build /etc/passwd /etc/passwd

COPY - -from=build /app/api-golang api-golang

USER nonroot

EXPOSE 8080

CMD [“/api-golang”]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> docker build -t api-golang: .7
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/api-golang main :1 !3 ?3
> cd ..
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM node

COPY . .

RUN npm install

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker build -t client-react:0 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM node:19.4-bullseye

COPY . .

RUN npm install

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker build -t client-react:1 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM node:19.4-bullseye

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

CMD [“npm”, “run”, “dev”]

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker build -t client-react:2 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> 

https://hub.docker.com/_/nginx 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM node:19.4-bullseye as build 

WORKDIR /usr/src/app

COPY package*.json ./

RUN - -mount=type=cache, target=/usr/src/app/.npm \ 
       npm set cache /usr/src/app/.npm && \ 
       npm ci 

RUN npm install

COPY . .

RUN npm run build 

###
FROM nginx:1.22-alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY - -from=build usr/src/app/dist /usr/share/nginx/html

EXPOSE 80 

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker build -t client-react:3 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> 

https://hub.docker.com/r/nginxinc/nginx-unprivileged 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM node:19.4-bullseye as build 

WORKDIR /usr/src/app

COPY package*.json ./

RUN - -mount=type=cache, target=/usr/src/app/.npm \ 
       npm set cache /usr/src/app/.npm && \ 
       npm ci 

RUN npm install

COPY . .

RUN npm run build 

###
FROM nginxinc/nginx-unprivilegednginx:1.23-alpine-perl

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY - -from=build usr/src/app/dist /usr/share/nginx/html

EXPOSE 80 

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker build -t client-react:4 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> 

Visual Studio Code
Explorer
OPEN EDITORS
DEVELOPING
05-example-web-application
client-react
Dockerfile

Dockerfile
FROM node:19.4-bullseye as build 

WORKDIR /usr/src/app

COPY package*.json ./

RUN - -mount=type=cache, target=/usr/src/app/.npm \ 
       npm set cache /usr/src/app/.npm && \ 
       npm ci 

RUN npm install

COPY . .

RUN npm run build 

###
FROM nginxinc/nginx-unprivilegednginx:1.23-alpine-perl

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY - -from=build usr/src/app/dist /usr/share/nginx/html

EXPOSE 8080

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application main 
> docker build -t client-react:5 .
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> docker image ls | grep client-react
client-react       4        227200620755      about a m ago      76.4MB
client-react       3        991e0a2c7a3c       3m ago                 23.8MB
…

General Principles ( Part 1 )
Make it work, make it secure, make it fast

Pin specific versions 
Base images (either major+minor OR SHA256 hash) 
           System Dependencies 
Application Dependencies 
Use small + secure base images
Protect the layer cache
Order commands by frequency of change 
COPY dependency requirements file → install deps → copy remaining source code
Use cache mounts
Use COPY --link 
Combine steps that are always linked (use heredocs to improve tidiness) 
Be explicit 
General Principles ( Part 2 )
Make it work, make it secure, make it fast

            Set working directory with WORKDIR
Indicate standard port with EXPOSE
Set default environment variables with ENV 
Avoid unnecessary files
Use .dockerignore
COPY specific files
Use non-root USER 
Install only production dependencies 
Avoid leaking sensitive information 
Leverage multi-stage builds 


Additional Features 
Parser Directives 
1 # syntax=docker/dockerfile:1/.5
2 # spacape=\
ARG ( Available at building time )
Label ( Import metadata within the image manifest )
LABEL org.opencontainers.image.authors=“sid@devopsdirective.com”
Heredocs Syntax 
# Heredocs allow for specifying multiple commands to be run within a single step,
# across multiples lines without lots of && and \
RUN <<EOF
apt update 
apt install iputils-ping -y
EOF
Mounting Secret
RUN - -mount=type=secret, id=secret.txt, dst=/container-secret.txt \  
Entrypoint + CMD 
ADD vs COPY 
Buildx ( Multi-architecture-images ) 
Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/05-exemple-web-application/client-react main :1 !3 ?4 
> make build-sample
~/d/c/d/devops-directive-docker-course/06-building-container-images main :1 !3 ?4 
> make run-sample-entrypoint-cmd

https://hub.docker.com/r/sidpalas/multi-arch-test/tags 

~/d/c/d/devops-directive-docker-course/06-building-container-images main :1 !3 ?4 
> make build-multiarch
[ auth ] sidpalas/multi/arch/test:pull, push token for registry-1.docker.io  
~/d/c/d/devops-directive-docker-course/06-building-container-images main :1 !3 ?4 
> 

Part 7
Container Registries ( A repository or a collection of repositories used to store and access container images )



Authenticating to Container Registry
Docker CLI can use basic auth or leverage credentials helpers 

Visual Studio Code 
Terminal
~/d/c/d/devops-directive-docker-course/06-building-container-images main :1 !3 ?4 
> make build
echo “FROM scratch” > Dockerfile
docker build - -tag my-scratch-image .
~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
> 

Dockerhub UI ( Repository my-scratch-image )

Visual Studio Code
Terminal 
~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
> docker login 
Authenticating with existing credentials…
Login Succeed
~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
>  make push-dockerhub
The push refers to repository [ docker.io/sidpalas/my-scratch-image ]
abc-123: digest: sha256:adf10351062ad5351ac2e714e04a0afb020b9df650ac99a07cbf49c0e18f8e43 size: 313
 ~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
> 

Github UI

https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry 
Authenticating with a personal access token (classic)
https://github.com/settings/tokens/new?scopes=write:packages
( docker course creds )
write:packages
Generate Token 

Visual Studio Code
Terminal
 ~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
> export CR_PAT=ghp_KItI085fVtupSsWCqoyxqm7xFOK5s0j5X9J
 ~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 

Github UI
echo $CR_PAT | docker login ghcr.io -u USERNAME --password-stdin

Visual Studio Code
Terminal
> echo $CR_PAT | docker login ghcr.io -u USERNAME --password-stdin
Login Succeeded 
 ~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
> make push-github-packages 
The push refers to repository [ hgcr.io/sidpalas/my-scratch-image ]
abc-123: digest: sha…
 ~/d/c/d/devops-directive-docker-course/07-container-registry main : !2 ?1 
> 

Web Browser 
hgcr.io/sidpalas/my-scratch-image
Github
Install from the command line
$ docker pull ghcr/sidpalas/my-scratch-image:abc-123
my-scratch-image
Recent tagged image version
latest abc-123
Published 33m ago . Digest …
View and manage all versions 

Part 8 
Running Containers

There are two primary ways to run docker containers, with docker run and docker compose up.


Github UI
https://github.com/magicmark/composerize 

Dockerhub runtime flags 

Configuration Options 

-d
--entrypoint
--env, -e, --env-file
--init
--interactive, -i
--mount, --volume, -v
--name
--network, --net
--platform
--publish, -p
--restart
--rm
--tty, -t

-d
> docker run ubuntu sleep 5
~
> docker run -d ubuntu sleep 99
ID Container 
fe7bbe84eff47373fc4a178fe93d8c3905929193c94146602c78f346b8c3eb3
~
> docker ps ( background ) 
CONTAINER ID              IMAGE              COMMAND …
fe7bbe84eff4                   ubuntu               …
…
~
>

- -entrypoint 
> docker run - -entrypoint echo ubuntu hello
hello
~
> 

- -env, en - -env-file
> docker run - -env MY_ENV=hello ubuntu printenv
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin/bin
HOSTNAME=c3d11c14f1ec
MY_ENV=hello
HOME=/root
~
> 

- -init 
> docker run ubuntu ps
PID TTY                       TIME CMD
1 ?                                00:00:00 ps
~ 
> docker run - -init ubuntu ps
PID TTY                        TIME CMD
1 ?                                00:00:00 docker-init
7?                                 00:00:00 ps
~
> 

- -interactive, I, - -tty, -t
> docker run ubuntu
~
> docker run -it ubuntu ( Shell running in the container )
root@9102aa1332f:/# 
~

-- name
> docker run -d - -name my container ubuntu sleep 99
docker: Error response from daemon: …
> docker container rm my-container
my-container
> docker run -d - -name my container ubuntu sleep 99
3619e1b7e708ca5b39098bf34d300c38912d7b3b7af16ad45a9d382197db239
> docker ps
CONTAINER ID              IMAGE              COMMAND …    CREATED STATUS PORTS 
e619e1b7e708                ubuntu               …                           
NAMES
my-containers …
…
~
> docker logs my-container 
~
>  

-- network, - -net
> docker network ls
NETWORK ID         NAME       DRIVER            SCOPE
87cc89cf24a3          bridge       bridge                local
06a395a89482         host          host                   local
aeba26f558845        none         null                    local 
~
> docker network create my-network
13d47f2159e7c03c49abb7a4478ec1cef6feb2537b843a917a891b0a95a370be
~
> docker network ls
NETWORK ID         NAME              DRIVER            SCOPE
87cc89cf24a3          bridge               bridge               local
06a395a89482         host                  host                  local
13d4f21559e7          my-network      bridge               local
aeba26f58845          none                 null                   local
~
> docker run -d - -network my-network ubuntu sleep 99
6f724bdf16186701c969eb89dfbd743a529290353882588db4c9df7fe8343cbc
~
> docker ps
CONTAINER ID              IMAGE              COMMAND …    CREATED STATUS PORTS 
6f724bdf1618                  ubuntu               …                           
NAMES  
…
…
~
> docker container inspect 6f724bdf1618 | grep network
“NetworkMode”: “my-network”,
“my-network”: {
~
> 

- -platform ( Which architecture to run the container image )
> docker run - -platform linux/arm64/v8 ubuntu dpkg - -print-architecture 
Unable to find image…
latest: …
Digest …
Status: Download newer image for ubuntu:latest arm64
~
> docker run - -platform linux/amd64 ubuntu dpkg - -print-architecture
Unable to find image…
latest: …
Digest …
Status: Download newer image for ubuntu:latest arm64
~
> 

- -publish, -p
> docker run - -restart unless-stopped ubuntu
~ 

- -restart
> watch “docker ps”
# Exiting and Restarting
CONTAINER ID              IMAGE              COMMAND …    CREATED STATUS PORTS 
ab8a4d0c8f5e                 ubuntu               …                           
NAMES  
…
…
~
> 

- -rm
> docker run - -name this-one-will-be-there ubuntu
~
> docker run - -rm - -name this-one-will-be-gone ubuntu
~
> docker container ls -a | grep this-one
a11766a2a9f7    ubuntu    “/bin/bash”
23s ago
this-one-will-be-there
~
> 

Configuration Options 

--cap-add, --cap-drop
--cgroup-parent
--cpu-shares
--cpuset-cpus (pin execution to specific CPU cores)
--device-cgroup-rule,
--device-read-bps, --device-read-iops, --device-write-bps, --device-write-iops
--gpus (NVIDIA Only)
--health-cmd, --health-interval, --health-retries, --health-start-period, --health-timeout
--memory , -m
--pid, --pids-limit
--privileged
--read-only
--security-opt
--userns

- -cap-add, - -cap-drop ( capabilities ) Specify which linux capabilities should be accessible from the containers / security 
> 

--cgroup-parent ( Specify which cgroup id the container should be associated with )
> 

--cpu-shares ( Specify what percentage of the CPU cycle the container should have access ) 
> 

--cpuset-cpus (pin execution to specific CPU cores)
> 

--device-cgroup-rule ( Different devices the container should have access to )
> 

--gpus (NVIDIA Only)
>

--health-cmd, --health-interval, --health-retries, --health-start-period, --health-timeout ( Health check which the docker will use periodically pin the container )

--memory , -m ( Specify how much memory the container should have to )
>

--pid, --pids-limit ( Specify how many sub process the container should be allowed to manage )
>

--privileged ( Overwrite the security options and give privileges the container could have )
> 

--read-only ( Without read-only access to security ) 
> 

--security-opt ( Specify app armor or secam profiles available to use when the container is running )
> 

--userns ( At running docker engine, namespace remapping for the user namespaces, allow to map from an non root user to a root user inside the container ) 
>

Visual Studio Code
Terminal
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> make docker-build-all
Writing image sha…
> docker network ls
NETWORK ID         NAME       DRIVER            SCOPE
87cc89cf24a3          bridge       bridge                local
06a395a89482         host          host                   local
aeba26f558845        none         null                    local 
~
> docker network create my-network
~
> docker network ls
NETWORK ID         NAME          DRIVER            SCOPE
87cc89cf24a3          bridge          bridge                local
06a395a89482         host             host                   local
8d487fc8f542           my-network  bridge               local
aeba26f558845        none             null                    local 

https://www.composerize.com/ 

 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker run -d \
       - -name db \
       - -network my-network \
       - e POSTGRES_PASSWORD=foobarbaz \ 
       -v pgdata:/var/lib/postgresql/data \ 
      -p 5432:5432 \
      - -restart unless-stoped \ 
      postgres:15.1-alpine
> docker ps 
CONTAINER ID              IMAGE                      COMMAND …    CREATED STATUS PORTS 
2214f852d906               postgres:15.1-alpine              …                           
NAMES
…
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker logs 2214f852d906
PostgreSQL Database directory appears to contain a database: Skipping initialization …
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker run -d\
       - -name api-node \
       - -network my-network
      -e DATABASE_URL = $ { DATABASE_URL } \
      -p 3000:3000 \
      - -restart unless-stoped \
      - -link=db \
      api-node
> docker ps 
CONTAINER ID              IMAGE                      COMMAND …    CREATED STATUS PORTS 
b0e4d5e8e2be                api-node              …                           
NAMES
…
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker logs b0e4d5e8e2be
…
Node.js v19.6.1
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> 

Web Browser
localhost:3000

{
       “now”: “2023-02-20T19:15:13.737z”,
       “api”: “node”
}

Visual Studio Code
Terminal
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker run -d \
       - -name api-golang \
       - -network my-network \
       -e DATABASE_URL= $ { DATABASE_URL } \
       -p 8080:8080
       - -restart unless-stopped \
       - -lin=db
       api-goland
> docker ps 
CONTAINER ID              IMAGE                      COMMAND …    CREATED STATUS PORTS 
5300d395d22a                api-node              …                           
NAMES
…
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
>

Web Browser
localhost:8080

{
       “api”: “golang”,
       “now”: “2023:02:20T19:15:57.828392z”
}

Visual Studio Code 
Terminal
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker run -d \
       - -name client-react-vite \ 
       - -network my-network
       -v ${PwD}/client-react-vite.config.js:/usr/src/app/vite.config.js \ 
       -p 5173:5173
       - -restart unless-stopped \
       - -link=api-node \
       - -link=api-golang \
       client-react-vite
> docker ps 
CONTAINER ID              IMAGE                      COMMAND …    CREATED STATUS PORTS 
984eee11cd62               client-react-vite             …                           
NAMES
…
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> 

Web Browser
localhost:5173

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-20T19:18:01.387483Z
API: node
                                                           - - -
Time from DB: 2023-02-20T19:18:05.100Z
Visual Studio Code
Terminal
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker run -d \
       - -name client-react-nginx \
       - -network my-network \
       -p 80:8080 \
       - -restart unless-stopped \
       - -link=api-node \
       - -link=api-golang
       client-react-nginx
> docker ps 
CONTAINER ID              IMAGE                      COMMAND …    CREATED STATUS PORTS 
464ce8aee5c5               client-react-nginx             …                           
NAMES
…
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> 

Web Browser
localhost

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-20T19:19:44.798567Z
API: node
                                                           - - -
Time from DB: 2023-02-20T19:19:44.802Z

Visual Studio Code
Terminal 
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> make docker-stop
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> make docker-rm
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker ps 
CONTAINER ID              IMAGE                        COMMAND …    CREATED STATUS PORTS 
06c258e8aaea       moby/buildkit:buildx-stable-1             …                           
NAMES

 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker compose build
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker compe up -d
> docker ps 
CONTAINER ID              IMAGE                      COMMAND …    CREATED STATUS PORTS 
782fee714ec1                api-node              …                           
                                       api-golang
                                       client-react-vite
                                       client-react-nginx
                                       postgres:15.1-alpine

NAMES
running-containers-api-node-1
…
 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> docker compose stop
running-containers-api-golang-1                          Stopped
running-containers-client-react-nginx-1                Stopped
running-containers-client-react-vite-1                   Stopped
running-containers-api-node-1                             Stopped
running-containers-db-1                                       Stopped

 ~/d/c/d/devops-directive-docker-course/08-running-containers main : !1 ?1 
> 

Part 9
Container Security

Image Security
“What vulnerabilities exist in your image that an attacker could exploit ?
Software dependencies that are installed within your image

Runtime Security
If an attacker successfully compromises a container, what can they do ? How difficult will it be to move laterally ?
Stacky and confined within the container because the configuration of run time were configured improperly 

“What vulnerabilities exist in your image that an attacker could exploit?”
Keep attack surface area as small as possible:
Use minimal base images (multi-stage builds are a key enabler) https://www.chainguard.dev/ 
Don’t install things you don’t need (don’t install dev deps)
Scan images! ( https://snyk.io/ )
Use users with minimal permissions ( Linux user )
Keep sensitive info out of images
Sign and verify images ( Cryptography )
Use fixed image tags, either:
Pin major.minor (allows patch fixes to be integrated)
Pin specific image hash
Docker daemon (dockerd)
Start with --userns-remap option(https://docs.docker.com/engine/security/userns-remap/)
Individual containers:
Use read only filesystem if writes are not needed
--cap-drop=all, then --cap-add anything you need
Limit cpu and memory --cpus=“0.5” --memory 1024m
Use --security-opt
seccomp profiles (https://docs.docker.com/engine/security/seccomp/)
apparmor profiles (https://docs.docker.com/engine/security/apparmor/)

Part 10
Interacting with Docker Objects 

Images 
Container 
Volumes
Networks

Terminal 
> docker - -help
~
> docker image - -help

docker image COMMAND:
 build       Build an image from a Dockerfile (`docker build` is the same as `docker image   build`)
  history     Show the history of an image
  import     Import the contents from a tarball to create a filesystem image
  inspect    Display detailed information on one or more images
  load         Load an image from a tar archive or STDIN
  ls             List images
  prune      Remove unused images
  pull          Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rm            Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  tag          Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
> cat Dockerfile
FROM ubuntu:22.04
RUN echo hello
CMD [“echo” “goodbye”]
~
> docker build -t new-image- < Dockerfile
…
~
> docker image history new-image
IMAGE              CREATED       CREATED BY                   SIZE           COMMENT       
e30dca9ea67b  5m ago            CMD [“echo” “goodbye”]   0B               buildkit.dockerfile.v0
…
~
> docker image history ubuntu:22.04     
IMAGE              CREATED       CREATED BY                                    SIZE           COMMENT    
58db3edaf2be   3w ago            /bin/sh -c #(nop) CMD [“/bin/bash”]    0B
…
~
> docker image inspect new-image 
…
JSON file ( Metadata ) 
…
~
> docker image ls 
REPOSITORY            TAG            IMAGE ID          CREATED        SIZE 
<none>                        <none>       1dae48189382  6m ago             77.8MB
…
~
> docker image prune
WARNING ! This will remove all dangling images.
Are you sure you want to continue ? [y/N] N
Total reclaimed space: 0B
~
> docker image pull ubuntu:22.04
22.04: Pulling from library/ubuntu
Digest: sha256:9a0bd…
Status: Image is up to date for ubuntu:22.04
docker.io/library/ubuntu:22.04
~
> docker image rm new-image
Untagged: new-image: latest
Deletd: sha256:330dc1…
~
> docker image tag ubuntu:22.04 my-ubuntu-tag
~
> docker image ls | grep my-ubuntu
my-ubuntu-tag                                    latest          58db3edaf2be        3w ago          77.8MB
~
> docker scan ubuntu:22.04
Querying vulnerabilities database…
~
> 

Containers
docker container COMMAND:
 attach      Attach local standard input, output, and error streams to a running container
  commit   Create a new image from a container's changes
  cp           Copy files/folders between a container and the local filesystem
  create     Create a new container
  diff           Inspect changes to files or directories on a container's filesystem
  exec       Run a command in a running container
  export     Export a container's filesystem as a tar archive
  inspect    Display detailed information on one or more containers
  kill           Kill one or more running containers
  logs        Fetch the logs of a container
  ls            List containers
  pause     Pause all processes within one or more containers
  port         List port mappings or a specific mapping for the container
  prune      Remove all stopped containers
  rename   Rename a container
  restart     Restart one or more containers
  rm           Remove one or more containers
  run          Run a command in a new container
  start        Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top          Display the running processes of a container
  unpause Unpause all processes within one or more containers
  update    Update configuration of one or more containers
  wait         Block until one or more containers stop, then print their exit codes
> docker run ubuntu sleep 999
~
> docker ps 
CONTAINER ID      IMAGE      COMMAND      CREATED   STATUS         PORTS     602c625bb13bb2    ubuntu       “sleep 999”       27s ago       Up 26s                            
NAMES
elegant_kepler
~
> docker kill 602c625bb13bb2
602c625bb13bb2 
~ 
> exit
~
> docker logs 602c625bb13bb2
…
~
> docker container logs 602c625bb13bb2
…
~
> docker container logs 602c625bb13bb2 -f
…
~
> docker container ls
CONTAINER ID      IMAGE                 COMMAND      CREATED   STATUS         PORTS     
06c258e8aaea        moby/buildkit:...     “buildkit”           44h ago       Up 26s                            
NAMES
buildx_…
~
> docker container ls -a
…
~
> docker run -d ubuntu sleep 99
069c6…
~
> docker container top 069c6…
UID         PID           C            STIME            TTY          TYME      CMD         
…
~
> 
Volumes
docker volume COMMAND:
 create      Create a volume
 inspect     Display detailed information on one or more volumes
 ls              List volumes
 prune       Remove all unused local volumes
 rm            Remove one or more volumes
~
> docker volume create my-volume
my-volume
~
> docker volume inspect my-volume
[ 
       {
              “CreatedAt”: “2023-01-27T18:56:59Z”,
              “Driver”: “local”,
              “Labels”: “null”,
              “Mountpoint”: “/var/lib/docker/volumes/my-volume/data”,
              “Name”: “my-volume”,
              “Options”: “null”,
               “Scope”: “local”
       }
]
~
> docker volume ls
local        a08a0…
…
…
local        mongodata
…
~
> 
Networks
docker network COMMAND:
 connect       Connect a container to a network
 create         Create a network
 disconnect  Disconnect a container from a network
 inspect        Display detailed information on one or more networks
 ls                 List networks
 prune          Remove all unused networks
 rm               Remove one or more networks
~
> docker network ls
NETWORK ID           NAME          DRIVER        SCOPE
87cc89cf24a3            bridge          bridge            local
06a395a89482          host              host               local
13d47f2159e7           my-network  bridge            local
aeba26f58845           none             null                local 
~
> docker run -d ubuntu sleep 999
ce828…
~
> docker network connect my-network ce828…
~
> docker network inspect 13d47f2159e7 
“ConfigOnly”: false,
“Containers”: {
       “ce828…”: {
       “Name”: “awesome_brown”,
       “EndpointID”: “63507…”,
        “MacAddress”: “02:42:ac:1b:00:02”,
        “IPv4Address”: “172.27.0.2/16”,
        “IPv6Address”: “”
       }
} …
…
~
> docker ps
CONTAINER ID      IMAGE     COMMAND      CREATED   STATUS         PORTS     
ce82861bb7ff          ubuntu     “sleep 999”        48s ago      Up 47 ago       Up 26s                            
NAMES
awesome_brow
…
~
> 

Part 11
Development Workflow

Development Environment
Because we are running our application within containers, we need a way to quickly iterate and make changes to them. Some of our tactics in 06-building-container-images help here (e.g. protecting the layer cache) so that images build quickly, but we can do better.
We want our development environment to have the following attributes:
Easy/simple to set up: Using docker compose, we can define the entire environment with a single yaml file. To get started, team members can issue a single command make compose-up-build or make compose-up-build-debug depending if they want to run the debugger or not.
Ability to iterate without rebuilding the container image: In order to avoid having to rebuild the container image with every single change, we can use a bind mount to mount the code from our host into the container filesystem. For example:
     - type: bind
        source: ../05-example-web-application/api-node/
        target: /usr/src/app/
Automatic reloading of the application:
React Client: We are using Vite for the react client which handles this handles this automatically
Node API: We added nodemon as a development dependency and specify the Docker CMD to use it
Golang API: We added a utility called air (https://github.com/cosmtrek/air) within Dockerfile.dev which watches for changes and rebuild the app automatically.
Use a debugger:
React Client: For a react app, you can use the browser developer tools + extensions to debug. I did include react-query-devtools to help debug react query specific things. It is also viewed from within the browser.
Node API: To enable debugging for a NodeJS application we can run the app with the --inspect flag. The debug session can then be accessed via a websocket on port 9229. The additional considerations in this case are to specify that the debugger listen for requests from 0.0.0.0 (any) and to publish port 9229 from the container to localhost.
Golang API: To enable remote debugging for a golang application I installed a tool called delve (https://github.com/go-delve/delve) within ./api-golang/Dockerfile.dev. We then override the command used to run the container to use this tool (see: docker-compose-debug.yml)

These modifications to the configuration (overridden commands + port publishing) are specified in docker-compose-debug.yml. By passing both docker-compose-dev.yml AND docker-compose-debug.yml to the docker compose up command (See: make compose-up-debug-build) Docker combines the two files, taking the config from the latter and overlaying it onto the former.
Both ./api-golang/README.md and ./api-node/README.md show a launch.json configuration you can use to connect to these remote debuggers using VSCode. The key setting is substitutePath such that you can set breakpoints on your local system that get recognized within the container.
Executing tests: We also need the ability to execute our test suites within containers. Again, we can create a custom docker-compose-test.yml overlay which modifies the container commands to execute our tests. To build the api images and execute their tests, you can execute make run-tests which will use the test compose file along with the dev compose file to do so.
Visual Studio Code 
Terminal  
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !2 ?2
 >  male compose-up-build
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !5 ?2
 >

Web Browser 
localhost:5173

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-20T00:47:14.766891Z
API: node
                                                           - - -
Time from DB: 2023-02-20T00:47:14.903Z

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !5 ?2
> make compose-up-build

Web Browser 
localhost:5173

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-22T00:51:19.194751Z
API: node
                                                           - - -
Time from DB: 2023-02-22T00:51:14.903Z

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !5 ?2
> 

Visual Studio Code
Explorer
OPEN EDITORS
06-building-container-images
api-node
Dockerfile.9

# Pin specific version for stability




# Use slim for reduced image size


FROM node:19.6-alpine AS base


















# Specify working directory other than /


WORKDIR /usr/src/app






# Copy only files required to install


# dependencies (better layer caching)


COPY package*.json ./

FROM base as dev

RUN mount=type=cache,target=/usr/src/app/.npm \
       npm set cache /usr/src/app/.npm && \
       npm install

COPY . .

CMD [ “npm”, “run”, “dev” ]

FROM base as production

# set NODE_ENV
ENV NODE_ENV production 






# Install only production dependencies


# Use cache mount to speed up install of existing dependencies


RUN --mount=type=cache,target=/usr/src/app/.npm \


npm set cache /usr/src/app/.npm && \


npm ci --only=production






# Use non-root user


# Use --chown on COPY commands to set file permissions


USER node






# Copy the healthcheck script


COPY --chown=node:node ./healthcheck/ .






# Copy remaining source code AFTER installing dependencies.


# Again, copy only the necessary files


COPY --chown=node:node ./src/ .






# Indicate expected port


EXPOSE 3000






CMD [ "node", "index.js" ]

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
>

Visual Studio Code
Explorer
OPEN EDITORS
06-building-container-images
api-golang
Dockerfile.8 


# Pin specific version for stability




# Use separate stage for building image


# Use debian for easier build utilities


FROM golang:1.19-bullseye AS build-base






WORKDIR /app






# Copy only files required to install dependencies (better layer caching)


COPY go.mod go.sum ./






# Use cache mount to speed up install of existing dependencies


RUN --mount=type=cache,target=/go/pkg/mod \


--mount=type=cache,target=/root/.cache/go-build \


go mod download






FROM build-base AS dev






# Install air for hot reload & delve for debugging


RUN go install github.com/cosmtrek/air@latest && \


go install github.com/go-delve/delve/cmd/dlv@latest






COPY . .






CMD ["air", "-c", ".air.toml"]






FROM build-base AS build-production






# Add non root user


RUN useradd -u 1001 nonroot






COPY . .






# Compile healthcheck


RUN go build \


-ldflags="-linkmode external -extldflags -static" \


-tags netgo \


-o healthcheck \


./healthcheck/healthcheck.go






# Compile application during build rather than at runtime


# Add flags to statically link binary


RUN go build \


-ldflags="-linkmode external -extldflags -static" \


-tags netgo \


-o api-golang






# Use separate stage for deployable image


FROM scratch






# Set gin mode


ENV GIN_MODE=release






WORKDIR /






# Copy the passwd file


COPY --from=build-production /etc/passwd /etc/passwd






# Copy the healthcheck binary from the build stage


COPY --from=build-production /app/healthcheck/healthcheck healthcheck






# Copy the app binary from the build stage


COPY --from=build-production /app/api-golang api-golang






# Use nonroot user


USER nonroot






# Indicate expected port


EXPOSE 8080






CMD ["/api-golang"]


Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> make compose-up-build

Web Browser 
localhost:5173

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-22T01:09:42.889152Z
API: node
                                                           - - -
Time from DB: 2023-02-22T09:51:14.903Z

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> 

https://github.com/sidpalas/devops-directive-docker-course/blob/main/11-development-workflow/docker-compose-debug.yml 

Visual Studio Code
Explorer
OPEN EDITORS
011-devops-directive-docker-course
docker-compose-debug.yml

docker-compose-debug.yml
version: “3.9
services:
       api-node:
              commands:
                      -“npm”
                      - “run”
                      - “debug-docker”
               ports:
                      - “3000:3000”
                      - “9229:9229”
       api-golang:  
              commands:
                      - “div”
                      - “debug”
                      - “/app/main.go”
                      - “- -listen:4000”
                      - “- -headless=true”
                      - “- -log=true”
                      - “- -log-output=debugger,debuglineerr,gdbwire,lldbout,rpc”
                      - “- -accept-multiclient”
                      - “- -continue”
                      - “api-version=2”
               ports:
                      -  “8080:8080”
                      -  “4000:4000”
              
Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> make compose-up-debug-build

Web Browser 
localhost:5173

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-22T01:20:41.588213Z
API: node
                                                           - - -
Time from DB: 2023-02-22T20:51:14.903Z

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> 

Visual Studio Code
Docker Debug
Docker: Attach to Node
Docker: Attach to Golang
…

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> 

Web Browser 
localhost:5173

Hey Team ! 
- - -
API: golang
Time from DB: 2023-02-22T01:20:41.588213Z
API: node
                                                           - - -
Time from DB: 2023-02-22T20:51:14.903Z
                                                                                                                               Actions
fresh ( 0 ) fetching ( 0 ) paused ( 0 ) stale ( 2 ) inactive ( ) Bottom        Refresh Invalidate Reset Remove 
…

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> 

Visual Studio Code
Explorer
OPEN EDITORS
011-devops-directive-docker-course
docker-compose-test.yml

docker-compose-test.yml
version: “3.9
services:
       api-node:
              commands:
                      -“npm”
                      - “run”
                      - “test”
       api-golang:  
              commands:
                      - “go”
                      - “test”
                      - “-v”
                      - “./…”

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> make run-tests
…
Run all test suites.
~/d/c/d/devops-directive-docker-course/011-devops-directive-docker-course/11-development-workflow main : !6 ?2
> 

Continuous Integration
See .github/workflows/image-ci.yml for a basic GitHub Action workflow that builds, scans, tags, and pushes a container image.
It leverages a few publicly available actions from the marketplace:
https://github.com/marketplace/actions/docker-metadata-action (generates tags for the container images)
https://github.com/marketplace/actions/docker-login (logs into DockerHub)
https://github.com/marketplace/actions/build-and-push-docker-images (builds and pushes the images)
https://github.com/marketplace/actions/aqua-security-trivy (scans the images for vulnerabilities)
If you want to build out more advanced CI workflows I recommend looking at Bret Fisher's Automation with Docker for CI/CD Workflows repo (https://github.com/BretFisher/docker-cicd-automation). It has many great examples of the types of things you might want to do with Docker in a CI/CD pipeline!

GitHub UI

image-ci.yml
name: image-ci

on:
  push:
    branches:
      - 'github-action'
    tags:
      - 'v*'

jobs:
  build-tag-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Docker meta
        id: meta
        uses: docker/metadata-action@v4
        with:
          images: |
            sidpalas/devops-directive-docker-course-api-node
          tags: |
            type=raw,value=latest
            type=ref,event=branch
            type=ref,event=pr
            type=semver,pattern={{version}}
            type=semver,pattern={{major}}.{{minor}}
            type=raw,value={{date 'YYYYMMDD'}}-{{sha}}

      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Build and push
        uses: docker/build-push-action@v4
        with:
          file: ./06-building-container-images/api-node/Dockerfile.8
          context: ./05-example-web-application/api-node/
          push: true
          tags: ${{ steps.meta.outputs.tags }}

      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: 'sidpalas/devops-directive-docker-course-api-node:latest'
          format: 'table'
          exit-code: '1'
          ignore-unfixed: true
          vuln-type: 'os,library'
          severity: 'CRITICAL'

https://github.com/docker/metadata-action 

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/11-development-workflow github-action merge ~2 +71 ?2
> git commit - m “empty” - -allow-empty
~/d/c/d/devops-directive-docker-course/11-development-workflow github-action merge ~2 +71 ?2
> git push

https://github.com/sidpalas/devops-directive-docker-course/actions 
https://github.com/sidpalas/devops-directive-docker-course/actions/runs/4238565584 

Shipyard 
https://www.shipyardapp.com/ ( Add
https://github.com/sidpalas/devops-directive-docker-course/blob/main/08-running-containers/docker-compose.yml ) 

Visual Studio Code
Source Control
docker-compose-yml
+
add shipyard labels
commit

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/11-development-workflow github-action merge ~2 +71 ?2
> git push
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course main *2 ?1
> 

Shipyard UI 
Reload latest commit
Add environment variables 
Create application 
1 - creating building definitions 
2 - prepare building
3 - queueing build

GitHub 
return (
    <QueryClientProvider client={queryClient}>
      <h1>Hey Team from Shipyard ! </h1>
      <CurrentTime api="/api/golang/"/>
      <CurrentTime api="/api/node/"/>
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  );
https://github.com/sidpalas/devops-directive-docker-course/blob/main/05-example-web-application/client-react/src/App.jsx 

Visual Studio Code 
Terminal 
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course main *2 ?1
> git checkout -b shipyard demo
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo main *2 ?1
> 

Source Control
+
change message
commit

~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
> git push

Github UI
https://github.com/sidpalas/devops-directive-docker-course 
Create and Pull Request
Demo shipyard environment 
Create Pull Request

Shipyard UI
Applications
Base environment
Pull Request 
Build Details Dashboard
Services Overview
api-golang
db
api-node
client-react-nginx
Build logs
Deploy logs
api-golang
db
api-node
client-react-nginx
Run logs

Web Browser 
shipyard host

Hey Team from Shipyard ! 
- - -
API: golang
Time from DB: 2023-04-18T18:48:13.693344Z
                                                           - - -
                                                     API: Node
Time from DB: 2023-04-18T18:48:13.733Z

Shipyard UI
Applications      >_ Terminal 
Pods                                                   Resources 
Name                          Status                Age
client-react-nginx …
db …
api-golang …
api-node …


                             Namespaces
      sidpalas/devops-directive-docker-course | main

Logs [ api-golang ] Running
2023/04/18 18:28:11 DATABASE CONNECTED
[ GIN ] 2023/04/18 - 18:41:03 | 200 | 244.663us | 10.1.32.1 | GET  “/”

Shipyard-app-build-a3a72…
node@api-node-5b4d8c598-mkrwp:/usr/src/app$ ls
db.js   index.js   node_modules   package-lock.json   package.json 
node@api-node-5b4d8c598-mkrwp:/usr/src/app$ exit

https://docs.shipyard.build/docs/shipyard-cli/ 
Sidpalas ( User )
Profile 

Visual Studio Code 
Terminal 
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
> shipyard get environments
APP                                                UUID           READY     REPO                     PR#      URL 
devops-directive-docker-course      e8cc8…       true           devops-directive…           https://..
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
> shipyard logs - -env  e8cc8… - -service api-node
Example app listening on port 3000
GET / 200 47 - 47.996ms
…
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
> shipyard 
A tool to manage Ephemeral Environment on the Shipyard platform
Usage:
       shipyard [ command ]

Environments 
       cancel
       exec
       get
       logs 
       …

Additional commands:
       completion 
       help 
       set

Flags 
       - -config string 
 -h  - -help
…

Use “shipyard [ command ] - -help” for more information about a command. 
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
>  shipyard port-forward - -env  e8cc8… - -service api-node - -port 3000
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
> 

Web Browser 
localhost:3000

{
       “now”: “2023-04-18T18:59:46.807z ”, 
       “api”: “node”
}

GitHub UI
Repository
https://github.com/sidpalas/devops-directive-docker-course
Pull Request
https://github.com/sidpalas/devops-directive-docker-course/pulls 
Demo Shipyard Environment 
https://github.com/sidpalas/devops-directive-docker-course/pull/5 
Conversation 
sidpalas comment on Apr 18
No description provided.
change message
shipyard-app bot comment on Apr 18 
Your Shipyard environment was successfully built and is running
You can access it here: https://devops-directive-docker-course-devops-directive-doc-pr5.dev.sidpalas.shipyard.host/
See latest build details here: https://shipyard.build/application/b7e1778e-1864-44b0-8660-a58f3559d3f6/latest-build-detail

Part 12
Deploying Containers ( To production ) 

What do we care about ?
Security
Ergonomics / developer experience 
How easy is it to get your configuration working ?
How easy is it to deploy new versions ? Can you do it without downtime ?
Observability ( logging, monitoring, tracing )
Scalability
Is there enough CPU/GPU/etc… to run your application ?
If you need to run across multiples hosts, how do services communicate ?
Persistent storage configuration
Cost 

Let's Deploy on Docker Swarm !

Docker Swarm
https://docs.docker.com/engine/swarm/swarm-tutorial/ 

Deploy to a Single Node Swarm
Create Virtual Machine
Ensure firewall allows inbound traffic
Install docker https://get.docker.com/  
Use DOCKER_HOST to connect
Docker swarm init
Docker compose mods:
Add health checks
Add deployment strategy 
Add secrets ( + read secrets from file )
Build + push images to docker hub
Deploy stack

Civo UI
Virtual Machine 
Create a new Instance 
https://www.civo.com/docs/compute/create-an-instance 
1 - Hostname ( docker-course-swarm )
2 - How many instances ? ( 1 ) 
3 - Select size  ( Small machine type )
4 - Select image ( Ubuntu 22.04 LTS )
5 - Initial User ( Ubuntu )
6 - Network ( Default )
7 - Public IP Address ( Create )
8 - Firewall ( Default )
9 - SSH Key ( Sid-macbook )
Create  

Network
Name            Network         Instances           Clusters           Actions  
docker-test    default           docker-test                                 > rules
Manage
Inbound Rules
Protocols               Port ( s )            CIDR             Type          Label                         Action
UDP                      1-65535                                                     AII UDP ports open 
TCP                       22                                                             SSH
TCP                       80                                                             HTTP
TCP                       443                                                           HTTPS
TCP                       3000
TCP                         8080

Compute 
docker-course-swarm 
This instance is running
Public IP:212.244.152          Private IP: 192.1681.7
OS:           Ubuntu 22.04       Small                                    Reverse DNS  Default host…
Network:   default                  1 CPU / 2GB / 25GB
Firewall:    docker-test >       Upgrade                               View SSH Information    

Install Docker Engine 
SSH 
Copy and Past ( Public IP:212.244.152 ) on Visual Studio Code Terminal

Visual Studio Code 
Terminal
~/d/c/d/devops-directive-docker-course/devops-directive-docker-course shipyard-demo *2 ?1
> ssh ubuntu@212.244.152 
Are you sure you want to continue connecting ? ( yes / no [ fingerprint ] ) ? yes
ubuntu@docker-course-swarm-4f05-c14aa4:~$ docker
command docker not found…
ubuntu@docker-course-swarm-4f05-c14aa4:~$ curl https://get.docker.com/ | sh
ubuntu@docker-course-swarm-4f05-c14aa4:~$ docker ps
permission denied while trying to connect to the Docker daemon socket at unix:///var…
ubuntu@docker-course-swarm-4f05-c14aa4:~$ sudo chown $USER /var/run/docker.sock
ubuntu@docker-course-swarm-4f05-c14aa4:~$ docker ps
CONTAINER ID   IMAGE   COMMAND   CREATED    STATUS     PORTS    NAMES
ubuntu@docker-course-swarm-4f05-c14aa4:~$ exit 
logout 
Connection to 212.244.152 closed.
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> export DOCKER_HOST=ssh://ubuntu@212.244.152
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> docker ps
CONTAINER ID   IMAGE   COMMAND   CREATED    STATUS     PORTS    NAMES
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> docker swarm init ( swarm running on remote host )
Swarm initialized: current node ( hzvs4p88wj884tkl46csr4jdd ) is now a manager 
To add a work to this swarm, run the following command:
       docker swarm join - -token
To add a manager to this swarm , run ‘docker swarm join-token manager’ and follow the instructions.
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> 

Visual Studio Code
Explorer
DEVOPS-DIRECTIVE-DOCKER-COURSE
12-deploying-containers
docker-compose.yml

docker-swarm.yml
version: ‘3.7’
services:
    client-react-nginx:
     image: sidpalas/devops-directive-docker-course-client-react-nginx:5
      init: true
    networks:
      - frontend
    ports:
      - 80:8080
  api-node:
    labels:
      shipyard.route: '/api/node/'
      shipyard.route.rewrite: true
    image: sidpalas/devops-directive-docker-course-api-node:9
    init: true
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://postgres:foobarbaz@db:5432/postgres
    networks:
      - frontend
      - backend
    ports:
      - 3000:3000
  api-golang: 
    image: sidpalas/devops-directive-docker-course-api-golang:8
    init: true
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://postgres:foobarbaz@db:5432/postgres
    networks:
      - frontend
      - backend
    ports:
      - 8080:8080
  db:
    image: postgres:15.1-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=foobarbaz
    networks:
      - backend
    ports:
      - 5432:5432
volumes:
  pgdata:
networks:
  frontend:
  backend:

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> make swarm-deploy-stack
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> docker ps 
CONTAINER ID      IMAGE                                                                                            b6fdbcd3f5b2         sidpalas/devops-directive-docker-course-api-golang:8
…
COMMAND     CREATED      STATUS    PORTS   NAMES
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> 

Web Browser 
212.244.152

Hey Team ! 
- - -
API: golang
Time from DB: 2023-03-17T15:31:03.84429ZZ
                                                           - - -
                                                     API: Node
Time from DB: 2023-03-17T15:31:03.920Z

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> docker secret ls
ID      NAME     DRIVER      CREATED        UPDATED
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> make create-secret
echo -n “foobarbaz” | DOCKER_HOST=“ssh://ubuntu@212.244.152” docker secret created postgres-passwd - iqslf70nsy7fuvxm56s7gd2d
echo -n “postgres://postgres:foobarbaz@db:5432/postgres” | DOCKER_HOST=“ssh://ubuntu@212.244.152” docker secret created database-url - noexl5yv48fcbpatj5ufik484
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> docker secret ls
ID                                           NAME            DRIVER  CREATED        UPDATED
noexl5yv48fcbpatj5ufik484    database-url                  3s ago               3s ago
iqslf70nsy7fuvxm56s7gd2d     postgres-passwd            4s ago             4s ago
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !2 ?2 
> 

Visual Studio Code
Explorer
DEVOPS-DIRECTIVE-DOCKER-COURSE
12-deploying-containers
docker-compose.yml

docker-swarm.yml
version: ‘3.7’
services:
    client-react-nginx:
     image: sidpalas/devops-directive-docker-course-client-react-nginx:5
      init: true
    networks:
      - frontend
    ports:
      - 80:8080
  api-node:
    labels:
      shipyard.route: '/api/node/'
      shipyard.route.rewrite: true
    image: sidpalas/devops-directive-docker-course-api-node:9
    init: true
    depends_on:
      - db
    environment:
      - DATABASE_URL_FILE=/run/secrets/database-url
   secrets:
database-url
    networks:
      - frontend
      - backend
    ports:
      - 3000:3000
  api-golang: 
    image: sidpalas/devops-directive-docker-course-api-golang:8
    init: true
    depends_on:
      - db
    environment:
      - DATABASE_URL_FILE=/run/secrets/database-url
   secrets:
database-url
    networks:
      - frontend
      - backend
    ports:
      - 8080:8080
  db:
    image: postgres:15.1-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD_FILE=/run/secrets/postgres-passwd
    secrets:
 postgres-passwd
    networks:
      - backend
    ports:
      - 5432:5432
volumes:
  pgdata:
networks:
  frontend:
  backend:
secrets: 
   database-url:
      external: true
   postgres-passwd: 
      external: true

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> make swarm-deploy-stack
DOCKER_HOST“://ubuntu@212.2.244.152” docker stack deploy -c docker-swarm.yml example app
updating service example-app-api-golang ( id: o9e5gerx0ascb7gahue1t15pj )
updating service example-app-db ( id: … )
…
…
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> docker ps
CONTAINER ID  IMAGE                      STATUS   PORTS    NAMED   COMMAND CREATED
f869be582921    postgres:15.1-alpine
…
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> make swarm-ls
DOCKER_HOST=“ssh://@212.2.244.152” docker service ls
ID                        NAME                               MODE         REPLICAS  
o9e5gerx0asc      example-app-api-golang  replicated    0/1               
IMAGE                                                                                 PORT
sidpalas/devops-directive-docker-course-api-golang:8        *:8080->8080/tcp
…
…
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> 

Web Browser 
212.244.152

Hey Team ! 
- - -
API: golang
Time from DB: 2023-03-17T15:51:16.272696ZZ
                                                           - - -
                                                     API: Node
Time from DB: 2023-03-17T15:51:16.245Z


Visual Studio Code
Explorer
DEVOPS-DIRECTIVE-DOCKER-COURSE
12-deploying-containers
docker-compose.yml

docker-swarm.yml
version: ‘3.7’
services:
    client-react-nginx:
     image: sidpalas/devops-directive-docker-course-client-react-nginx:5
     deploy:
        mode: replicated
        replicas: 1
        update_config:
        order: start-first
      init: true
    networks:
      - frontend
    ports:
      - 80:8080
   healthcheck:
      test [ “CMD”, “curl”, “-t”, “http://localhost:8080/ping/”
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 10s 
  api-node:
    labels:
      shipyard.route: '/api/node/'
      shipyard.route.rewrite: true
    image: sidpalas/devops-directive-docker-course-api-node:9
   deploy:
        mode: replicated
        replicas: 1
        update_config:
        order: start-first
    init: true
    depends_on:
      - db
    environment:
      - DATABASE_URL_FILE=/run/secrets/database-url
   secrets:
database-url
    networks:
      - frontend
      - backend
    ports:
      - 3000:3000
  healthcheck:
      test [ “CMD”, “node”, “/usr/src/app/healthcheck.js”
      timeout: 5s
      retries: 3
      start_period: 10s 
  api-golang: 
    image: sidpalas/devops-directive-docker-course-api-golang:8
   deploy:
        mode: replicated
        replicas: 2
        update_config:
        order: start-first
    init: true
    depends_on:
      - db
    environment:
      - DATABASE_URL_FILE=/run/secrets/database-url
   secrets:
database-url
    networks:
      - frontend
      - backend
    ports:
      - 8080:8080
  healthcheck:
      test [ “CMD”, “/healthcheck” ]
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 10s 
  db:
    image: postgres:15.1-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD_FILE=/run/secrets/postgres-passwd
    secrets:
 postgres-passwd
    networks:
      - backend
    ports:
      - 5432:5432
volumes:
  pgdata:
networks:
  frontend:
  backend:
secrets: 
   database-url:
      external: true
   postgres-passwd: 
      external: true

Visual Studio Code
Terminal
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> make swarm-deploy-stack
DOCKER_HOST“://ubuntu@212.2.244.152” docker stack deploy -c docker-swarm.yml example app
updating service example-app-client-react-nginx ( id: n7e693cbfm99uxwnimzpqk2dt )
updating service example-app-db ( id: … )
…
…
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> make swarm-ls
DOCKER_HOST=“ssh://@212.2.244.152” docker service ls
ID                        NAME                               MODE         REPLICAS  
o9e5gerx0asc      example-app-api-golang  replicated    1/2               
IMAGE                                                                                 PORT
sidpalas/devops-directive-docker-course-api-golang:8        *:8080->8080/tcp
…
…
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
> docker ps
CONTAINER ID  IMAGE                      COMMAND   CREATED    STATUS       f869be582921    postgres:15.1-alpine                                             Up 15s ( health: starting )
PORTS NAMES
…
~/d/c/d/devops-directive-docker-course/12-deploying-containers/docker-swarm main *1 !3 ?2 
>

Web Browser 
212.244.152

Hey Team ! 
- - -
API: golang
Time from DB: 2023-03-17T15:58:16.7884191Z
                                                           - - -
                                                     API: Node
Time from DB: 2023-03-17T15:58:16.788Z

https://www.cloudflare.com/ 
Cloudflare
devopsdirective.com
…
DNS
…
DNS 
Records
Type      Name                               Content             Proxy status     TTL     Actions 
              docker-course-swarm      212.2.244.152                                        Edit
Save

Web Browser
docker-course-swarm.devopsdirective.com

Hey Team ! 
- - -
API: golang
Time from DB: 2023-03-17T16:00:27.20967Z
                                                           - - -
                                                     API: Node
Time from DB: 2023-03-17T16:00:27.213Z
Cloudflare
devopsdirective.com
…
SSL/TLS
Overview
Your SSL/TLS encryption mode is Flexible
…

1 - History and Motivation
2 - Technology Overview
Containers
Docker Architecture 
3 - Installation/Set Up and Hello World
4 - Using 3rd party containers
5 - Demo Application
6 - Building Container Images
Dockerfile Basics
Dockerfile Optimization
Build and more multi-architecture
7 - Container Registry
8 - Running Containers
9 - Container Security
10 - Interacting with Docker Objects 
11 - Development Workflow
12 - Deploying Containers 

https://courses.devopsdirective.com/docker-beginner-to-pro/lessons/06-building-container-images/07-additional-dockerfile-features 
