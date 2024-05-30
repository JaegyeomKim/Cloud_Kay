Container orchestration is all about managing the life cycles of containers, especiallty in large, dynamic environments. 

Requirements:
Monitor the Specific Web Server Container:
There should be a script to monitor the web server container.
Event-Driven Mechanism for Container Management:
If the web server container goes down, the script should attempt to restart it.
If the container fails to restart, the script should automatically start a new web server container on VM3.
Objective:
To ensure the continuous operation of a web server container by monitoring it and handling failures with automatic restarts or by deploying a new container if necessary.

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/f89fce9b-2b77-430e-b380-d313db4055a2)

Container Orchestration can be used to perfrorm lot of tasks, some of them includes:

- Provisioning and deployment of containers
- Scaling up or removing containers to spread app load evenly
- Movement of containers from one host to antoher if there is a shortage of resources.
- Load balancing of service discovery between containers
- Health monitoring of containers and hosts


🔥Docker Swarm & Building Labs

Docker Swarm is a container orchesration tool which is natively supported by Docker.

Lab Setup

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/ee10ed48-5c0d-4042-b59d-453d670430c3)


Document - Docker Script

Step 1: Open a text file named docker-install.sh via the vi editor

    nano docker-install.sh

Step 2: Paste the following script within the text file and save it

    #!/bin/bash
    
    # Install Docker dependencies
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
    
    # Add Docker GPG key
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    
    # Add Docker repository
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    
    # Install Docker
    sudo apt-get update
    sudo apt-get install -y docker-ce docker-ce-cli containerd.io
    
    # Start Docker service
    sudo systemctl start docker
    
    # Enable Docker service to start on boot
    sudo systemctl enable docker
    
Step 3: Make the script executable:

    chmod +x docker-install.sh

Step 4: Run the script:

    ./docker-install.sh

🔥Initializing Docker Swarm 

- A node is an instance of the Docker Engine participating in the swarm.
- To deploy your application to a swarm, you submit a service definition to a manager node.
- The manager node dispatches units of work called tasks to worker node.

1. Manager Node Command:

        docker swarm init --adverties-addr <MANAGER-IP>


   To add a worker to this swarm, run the following command:

        docker swarm join --token <something secrec>

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

3. Worker Nodes Command:
     
        docker swarm join --token <something secrec>



azureuser@vm2:~$ sudo docker node ls

ID                            HOSTNAME   STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
sle0f5mxinq1be3iesehv19x1 *   vm2        Ready     Active         Leader           26.1.3
r25ar6ws9xvluxou44ym8f2ea     vm3        Unknown   Active                          26.1.3
o8qijayebdwl7phbijk4vngmq     vm4        Unknown   Active                          26.1.3


🔥Services, Tasks and Containers

A service is the definition of the tasks to execute on the manager or worker nodes.

docker service create --name webserver --replicas 1 nginx

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/dbeeab0b-0230-4d97-b60a-4fae1b52aa3b)

    sudo docker service create --name webserver --replicas 1 nginx

  overall progress: 1 out of 1 tasks. 
  1/1: running
  
    sudo docker service ls
    
  ID             NAME        MODE         REPLICAS   IMAGE          PORTS
  6cgolzdgz3eq   webserver   replicated   1/1        nginx:latest


    sudo docker service ps webserver
    
  ID             NAME          IMAGE          NODE      DESIRED STATE   CURRENT STATE                ERROR     PORTS
  o8bktcbgx1ga   webserver.1   nginx:latest   vm2       Running         Running about a minute ago

    azureuser@vm2:~$ sudo docker ps
    
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
347dac6782d6   nginx:latest   "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    webserver.1.o8bktcbgx1gad0t16rwj3b2a9

    azureuser@vm2:~$ sudo docker stop 347dac6782d6
347dac6782d6

    azureuser@vm2:~$ sudo docker service ps webserver
ID             NAME              IMAGE          NODE      DESIRED STATE   CURRENT STATE             ERROR     PORTS
z7mxmd5t4lwl   webserver.1       nginx:latest   vm2       Running         Running 32 seconds ago
o8bktcbgx1ga    \_ webserver.1   nginx:latest   vm2       Shutdown        Complete 37 seconds ago

    azureuser@vm2:~$ sudo docker service rm webserver
webserver

    azureuser@vm2:~$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

  
🔥Scaling Service in Swarm

Once you have deployed a service to a swarm, you are ready to use the Docker CLI to scale the number of containers in the service.

Containers running in a service are called "tasks."

    azureuser@vm2:~$ sudo docker service create --name webserver --replicas 1 nginx
    
0poowau5ikqw170odc5svs9bw
verify: Service 0poowau5ikqw170odc5svs9bw converged

    azureuser@vm2:~$ sudo docker service scale webserver=5
    
webserver scaled to 5
overall progress: 5 out of 5 tasks
1/5: running   [==================================================>]
2/5: running   [==================================================>]
3/5: running   [==================================================>]
4/5: running   [==================================================>]
5/5: running   [==================================================>]
verify: Service webserver converged


    azureuser@vm2:~$ sudo docker service scale webserver=1
webserver scaled to 1
overall progress: 1 out of 1 tasks
1/1: running   [==================================================>]
verify: Service webserver converged

    azureuser@vm2:~$ sudo docker service ps webserver
ID             NAME              IMAGE          NODE      DESIRED STATE   CURRENT STATE             ERROR     PORTS
zhb1zvj4gwod   webserver.1       nginx:latest   vm4       Running         Running 10 minutes ago
21lun1znyqtb    \_ webserver.1   nginx:latest   vm2       Shutdown        Complete 10 minutes ago
xpplw4x9pebs   webserver.2       nginx:latest   vm3       Shutdown        Shutdown 4 minutes ago
i2zdd6njm0pj    \_ webserver.2   nginx:latest   vm2       Shutdown        Complete 10 minutes ago
os2sqbf5g71v   webserver.4       nginx:latest   vm2       Shutdown        Complete 10 minutes ago
i7297ijqg59y   webserver.5       nginx:latest   vm3       Shutdown        Shutdown 4 minutes ago
vxh3e0dimq8k    \_ webserver.5   nginx:latest   vm2       Shutdown        Complete 10 minutes ago

    azureuser@vm4:~$ sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
80e6410acde4   nginx:latest   "/docker-entrypoint.…"   11 minutes ago   Up 11 minutes   80/tcp    webserver.1.zhb1zvj4gwod7g5ulejsbs7e3

