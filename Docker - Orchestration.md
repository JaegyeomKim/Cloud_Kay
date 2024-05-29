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


