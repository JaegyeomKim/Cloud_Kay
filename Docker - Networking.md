
# 🔥Overview of Docker Networking

Docker takes care of the netwroking aspects so that container can communicate with other containers and also with the Docker Host.

Docker netwroking subsystem is pluggable, using drivers.

There are several drivers available by default, and provides core netwroing functionality.

- bridge
- host
- overlay
- macvlan
- none

  ![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/ed928260-d681-4ba1-853d-15ffbc4ba632)


  Commends

      ipconfig
      docker network ls
      docker inspect bridge
      docker container run -dt --name myhost --network host ubuntu
      docker network inspect host


  1. Bridge
Description:

The default network driver used by Docker when starting containers.
Creates an isolated network that containers connect to, separate from the host's network.
Containers communicate with each other through the bridge network.
When to use:

When multiple containers running on a single host need to communicate with each other.
When network isolation is needed.
Commonly used in development and testing environments.
Usage example:

    docker network create --driver bridge my-bridge-network
    docker run -d --name container1 --network my-bridge-network my-image
    docker run -d --name container2 --network my-bridge-network my-image
2. Host
Description:

The container shares the host’s network namespace.
No network isolation between the container and the host.
When to use:

When network performance is crucial.
When the container needs to use the host's IP and ports directly.
Useful for running a single container.
Usage example:

    docker run --rm -d --network host my-image

3. Overlay
Description:

Enables containers running on different Docker hosts to communicate with each other.
Used with orchestration tools like Docker Swarm or Kubernetes.
When to use:

When you need communication between containers running on multiple hosts.
When deploying services in a clustered environment.
Usage example:

    docker network create --driver overlay my-overlay-network
    docker service create --name my-service --network my-overlay-network my-image
4. Macvlan
Description:

Assigns a MAC address to each container, making it appear as a physical device on the network.
Containers can communicate directly with the external network through the host's network interface.
When to use:

When the container needs to be perceived as a physical device on the network.
When legacy applications need direct network access.
Usage example:

    docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 my-macvlan-network
    docker run -d --name container1 --network my-macvlan-network my-image

5. None
Description:

The container does not get a network interface.
Maximizes network isolation as the container has no network connectivity.
When to use:

When running containers that do not require network access.
In highly secure environments where network isolation is paramount.
Usage example:

    docker run --rm -d --network none my-image
    
Summary
Bridge: When multiple containers on a single host need to communicate.
Host: When network isolation between container and host is unnecessary, and performance is critical.
Overlay: When communication is needed between containers on different hosts.
Macvlan: When containers need to act like physical devices on the network.
None: When running highly isolated containers that do not need network connectivity.


# 🔥Understanding Bridge Network Driver


A  bridge network uses a software bridge which allows containers connected to the same bridge network t communicate, while providing isolation from contatiners which are not connected to that bridge network. 


![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/69001622-9ae0-4d97-8f37-9a6f58fb361b)

    docker container  exec -it test1 bash
    apt-get update && apt-get install netool

    ifconfig 

    apt-get install iptils-ping

    ping 172.17.0.4

  Bridge is the default network driver for Docker.

  If we do not specify a driver, this is the type of network you are creating.

  When you start a Docker, a defalut bridge network(also called bridge) is created automatically, and newly-started containers connect 
  to it unless otherwise specified.

  We also can create User-Defined Bridge Network which are superior to the default bridge. 

