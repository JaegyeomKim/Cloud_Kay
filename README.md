# 🔥 Connect Secure Shell to Azure VM

- Save the private key as docker-key.pem or it can be log-in 
- Ensure the permissions for the private key are restricted to the admin user, otherwise, an error will occur.

  ![explorer_MF0veGAAdE](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/7306312f-7a7a-4e0e-a483-8a20e626e86f)

- The terminal should be in the directory where docker-key.pem is located.
***

      ssh -i docker-key.pem <root>@<ip-address>

  - i: Specifies the identity file (private key) to be used.
  - root: Azure VM admin username.
  - ip-address: Azure VM public IP address.

# 🔥 Linux Commands

- This command is used to display the status of a systemd service on a Linux system. It provides information about whether the service is running, stopped, or encountering any issues, along with additional details such as its process ID (PID), memory usage, and recent log entries.

        systemctl status <docker>
***

- This command utilizes the curl tool to send an HTTP HEAD request to the specified <publicIp:port>. It retrieves the headers of the response from the server without downloading the actual content. This is often used to check the availability and configuration of a web server running at the specified IP address and port.

        curl -I <publicIp:port>
***

- This command is used to display a list of active network connections on a Linux system. Specifically, it shows TCP connections (-t), numeric addresses instead of resolving hostnames (-n), and listening ports (-l). The -p option additionally displays the process ID (PID) and name of the program associated with each connection.

        netstat -ntlp
***

# 🔥 Docker Commands

    sudo docker rm $(sudo docker ps -aq)

- sudo docker ps -aq: This command lists all Docker container IDs, regardless of their running status. The -a flag ensures that both running and stopped containers are included, and the -q flag ensures that only the IDs are displayed, without any additional formatting.
- $(...): This is command substitution in Bash. It allows the output of one command to be used as an input for another command.
- sudo docker rm: This command is used to remove one or more Docker containers. When followed by a list of container IDs, it removes the specified containers.
When combined, $(sudo docker ps -aq) provides a list of all container IDs, which is then passed as arguments to sudo docker rm, effectively removing all Docker containers on the system, whether they are running or stopped.
***

    sudo docker run --name docker-rm-test --rm -d -p <host port>:<container port> <image>

- sudo docker run: This command is used to create and run a Docker container.
- --name docker-rm-test: This option assigns the name "docker-rm-test" to the container.
- --rm: This option automatically removes the container when it exits. So, when the container is stopped (exits), it will be automatically deleted.
- -d: This option runs the container in detached mode, meaning it runs in the background.
- -p <host port>:<container port>: This option specifies the port mapping between the host and the container. You need to replace <hostport> with the desired host port number and <container port> with the port number inside the container.
- <image>: This is the name or ID of the Docker image from which the container is created.
***

      docker run --restart=POLICY <image>
  
      docker run --restart=no nginx
      docker run --restart=on-failure nginx
      docker run --restart=unless-stopped nginx
      docker run --restart=always nginx

- no: This restart policy indicates that the container should not be automatically restarted if it exits for any reason. It's essentially a manual restart policy, where the container will only restart if someone explicitly starts it again.

- on-failure: With this restart policy, the container will automatically restart if it exits with a non-zero exit status. This is useful for services that are expected to run continuously, but may encounter occasional failures.

- unless-stopped: This policy ensures that the container restarts automatically unless it is explicitly stopped by the user (using the docker stop command or similar). It will restart if it crashes, or if the Docker daemon is restarted.

- always: This restart policy ensures that the container always restarts automatically, regardless of the exit status. It will restart if it crashes, or if the Docker daemon is restarted. It's useful for critical services that need to be running continuously.

***

    sudo docker system df

- displays a summary of Docker's disk usage. It shows the usage of each disk type (containers, images, volumes) and the total usage. This provides useful information for monitoring and managing disk space in a Docker environment.
***






















