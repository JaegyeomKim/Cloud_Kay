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





