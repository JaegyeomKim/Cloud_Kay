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
















