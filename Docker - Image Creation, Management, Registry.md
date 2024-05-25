# 🔥Working With Docker Images

- docker Image file

      From ubuntu
      Run apt-get update
      Run apt-get -y install nginx
      CMD ["nginx", "-g", "daemon off;"]

- the terminal should be in hte directory where the DockerFile is located ex.root@docker-demo dockerImage
  
      docker build .

  High Level Overview

  ***

# 🔥Overview of DockerFile

Some commends

      apt-get update
      apt-get install -y nginx
      apt-get install nano
      echo "Welcome to Kay's Cloud World" > index.html
***

# 🔥COPY vs ADD

COPY taks in a sources and destination. It only lets you copy in a local file or directory from your host

ADD lwts you do that toom but it also supports 2 other sources.

- First, you can use a URL instead of a local file / directory.
- Secondly, you can extract a tar file from the source directly into the destination. 

**Use CURL and WGET whenever possible**

Using ADD to fetch packages from remote URLs is strongly discouraged; you should use curl or wget instead.

***
      ADD http://example.com/big.tar.xz /user/src/things/
      RUN tar -xjf /user/src/things/big.tar.xz -C /usr/src/things
      RUN make -C /use/sec/things all

Should avoid ⬆️ kind of a scenario because this will add multiple layers to the image which will increase the size.
***

      RUN mkdir -p /usr/src/thing \
            && curl -SL http://example.com/big/tar/xz \
            | tar -xJC /usr/src/things \
            && make -C /usr/src/things all



Can make use of curl and you can make use of the and an instruction over here.⬆️
So if you basically make use of the and an instruction not only it will help you have the lower layers

***
      sudo docker inspect <containerUUID>

This is the Docker command used to display detailed information about Docker objects, such as containers, images, volumes, or networks.
***

# 🔥Dockerfile - HEALTHCHECK

HEALTHCHECK instruction Docker allows us to tell the platform on how to test that our app is health. 

When the docker starts a container, it monitors the process that the conatiner runs. If the process ends, the container exits.

That's just a basic check and does not necessarily tell the detail about the app.

Can specify certain options before the CMD operation, these includes:

      HEALTHCHECK --interval=5s CMD ping -c 1 172.17.0.2
      
      --interval = DURATION (default: 30s)
      --timeout = DURATION (default: 30s)
      --start-period=DURATION (default: 0s)
      --retries=N (default:3)

https://docs.docker.com/reference/dockerfile/#healthcheck


# 🔥Dockerfile - ENTRYPOINT

The best use for ENTRYPOINT is to set the image's main command

ENTRYPOINT doesn't allow you to override the command. 

It's important to understand distinction between CMD and ENTRYPOINT

# 🔥Dockerfile - WORKDIR

The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile

DockerFile

      FROM busybox
      RUN mkdir /root/demo
      WORKDIR /root/demo
      RUN touch file01.txt # This instruction will run under the /root/demo 
      CMD ["/bin.sh"]  # This instruction will run under the /root/demo 


Important Pointer: The WORKDIR instruction can be used multiple times in a Dockerfile

Sample Snnippet:

      WORKDIR /a
      WORKDIR b
      WORKDIR c
      RUN pwd

OutPut = /a/b/c

# 🔥Dockerfile - ENV

The ENV instruction sets the env variable <key> to the value <value>.

Example Snippet:

      ENV NGINX 1.2
      RUN touch web-$NGINX.txt
      CMD ["/bin/sh"]

result = web-1.2.text

***
**Setting Env var from CLI**

You can use the -e, --env, and --env-file flags to set simple env var in the container you're runninb, or overwrite var that are defined in the DOckerfile of the image you're running.

Example

ENV Instruction used in Dockerfile:

      FROM busybox
      ENV NGINX 1.2
      RUN touch web-$NGINX.txt
      CMD ["/bin/sh"]

Using ENV in CLI:

      docker run -dt --name env02 --env USER=ADMINUSER busybox sh

      docker exec -it env02 sh
      echo $USER 
***

# 🔥DockerCommit

Whenever you make changes inside the contaner, it can be useful to commit a container's file changes ot settings into a new image.

By default, the conatainer being committed and its processes will be paused while the image is committed. 


Syntax:

      docker conatiner commit CONtainer-ID myimage01

The --change option will apply Dockerfile instructions to the images that is created.

Supported Dockerfile instructions:
- CMD | ENTRYPOIN | ENY | EXPOSE
- LABEL | ONBUILD | USER | VOLUME | WORKDIR


Whenever you make changes inside the container, it can be useful to commit a container's gile changes or setting into a new image.

By default, the container being committed and its processes will ve paused while the image is committed. 

Syntax:

      docker container commit CONTAINER-ID myimage01


# 🔥Layers of Docker Image

A Docker Images is built up from a series of layers.
Each layer represents an instruction in the image's Dockerfile.

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/76e4e3b6-091c-4091-8097-5dcb2fe53618)


The major difference between a container and an image is top writable layer.

All writes to the container that add new or modify existing data are stored in this writable layer. 

Docker Script

      FROM ubuntu
      RUN dd if =/dev/zero of=/root/file1.text bs =1m count=100
      RUN dd if =/dev/zero of=/root/file2.text bs =1m count=100
      RUN rm -f /root/file1.text
      RUN rm -f /root/file2.text


Has five layers but the side of image will be same even if the layer4 and 5 are triggered. 
So even though I'm removing it, the file still exists in the layer two, although it might not in the layer four, it might be de-linked, but the file still exists here.

Docker Script

      FROM ubuntu
      RUN dd if =/dev/zero of=/root/file1.text bs =1m count=100 && rm -f /root/file1.text
      RUN dd if =/dev/zero of=/root/file2.text bs =1m count=100&& rm -f /root/file2.text


**Having fewer layers can result in smaller Docker image sizes and improved build speeds. Thus, the second Dockerfile provides a more efficient build.
**


# 🔥Managing Images with CLI

Docker CLI can be used to manage various aspects related to Docker Images which includes building, removing, saving, tagging and others.

We should be familiar with the docker image child-commands. 

- docker image build
- docker image history
- docker image import
- docker image inspect
- docker image load
- docker image ls
- docker image prune
- docker image pull
- docker image push
- docker image rm
- docker image save
- docker image tag

# 🔥Inspecting Docker Image

A Docker Image contains lots of informaion, some of these include:

- Creation Date
- Command
- Environment Variables
- Architecture
- OS
- Size

Docker Image inspect command allows us to see all information associated with a docker image.


docker image inspect nginx | grep Config
docker image inspect nginx | grep Os

docker image inspect nginx --format='{{.Id}}'
docker image inspect nginx --format='{{json .Config}}'
docker image inspect nginx --format='{{.Config.Hostname}}'

# 🔥Docker Image Prune

Docker image prune command allows us to clean up unused images.

By default, the above command will only clean up dangling images. 

Dangling Images = Image without Tags and Image not referenced by any container

# 🔥Flattening Docker Images

In a generic scenerio, the more the layers an image has, the more the size of the imamge.

Some of the image size goes from 5GB to 10GB.

Flattrning an image to signle layer can help reduce the overall size of the image. 


 ** Modify Image to Single Layer **

      docker export myubuntu > myubuntudemo.tar

***

azureuser@LinuxUbuntuServerVM:~$ ls -la

total 121396
drwxr-xr-x 7 azureuser azureuser      4096 May 23 22:27 .
drwxr-xr-x 3 root      root           4096 May 21 16:41 ..
-rw------- 1 azureuser azureuser     11304 May 23 18:06 .bash_history
-rw-r--r-- 1 azureuser azureuser       220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 azureuser azureuser      3771 Feb 25  2020 .bashrc
drwx------ 2 azureuser azureuser      4096 May 21 17:22 .cache
drwx------ 3 azureuser azureuser      4096 May 22 20:56 .docker
drwxrwxr-x 3 azureuser azureuser      4096 May 22 20:51 .local
-rw-r--r-- 1 azureuser azureuser       807 Feb 25  2020 .profile
drwx------ 2 azureuser azureuser      4096 May 21 16:41 .ssh
-rw-r--r-- 1 azureuser azureuser         0 May 21 18:24 .sudo_as_admin_successful
drwxrwxr-x 2 azureuser azureuser      4096 May 23 17:09 demo
**-rw-rw-r-- 1 azureuser azureuser 124254720 May 23 22:27 myubuntudemo.tar**

***
      ls -l myubuntudemo.tar

-rw-rw-r-- 1 azureuser azureuser 124254720 May 23 22:27 myubuntudemo.tar

***

      sudo cat myubuntudemo.tar | sudo docker import - myubuntu:latest
sha256:5aa75958e3da75428a42bae96710b2f2fb482a7b02c285caca0970018b8b5e02

***

      sudo docker images

REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
**myubuntu     latest    5aa75958e3da   35 seconds ago   121MB**
myimage      v1.0      601541c312cd   24 hours ago     122MB
mysql        latest    e9387c13ed83   3 weeks ago      578MB
      
***

      sudo docker image history myubuntu

IMAGE          CREATED              CREATED BY   SIZE      COMMENT
5aa75958e3da   About a minute ago                121MB     Imported from -

Only one layer! 


# 🔥Understanding Docker Registry

A Registry a stateless, highly scalable server side application that stores and lets toy distribute Docker images.

Docker Hub is the simplest example that all of us must havbe used.

There are various types of registry available, which includes:

- Docker Registry
- Docker Trusted Registry
- Private Repositoty (AWS ECR)
- Docker Hub

***
      docker run -d -p 5000:5000 --restart always --name registry registry:2

- pull docker registry and run with tag of 2
- listening on 5000 

      docker pull ubuntu

      docker tag ubuntu:latest localgost:5000/myububtu
  
- Add image name: localhost:5000/myububtu

        docker push localhost:5000/myububtu
  
- it is pushing the image to docker registory

        docker pull localhost:5000/myububtu

- the image pulling from registry
