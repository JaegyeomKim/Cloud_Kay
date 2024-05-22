# 🔥 Connect Secure Shell to Azure VM

- Save the private key as docker-key.pem or it can be log-in 
- Ensure the permissions for the private key are restricted to the admin user, otherwise, an error will occur.

  ![explorer_MF0veGAAdE](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/7306312f-7a7a-4e0e-a483-8a20e626e86f)

- The terminal should be in the directory where docker-key.pem is located.

      ssh -i docker-key.pem <root>@<ip-address>

  - i: Specifies the identity file (private key) to be used.
  - root: Azure VM admin username.
  - ip-address: Azure VM public IP address.

  # 🔥 Linux Commands

- This command is used to display the status of a systemd service on a Linux system. It provides information about whether the service is running, stopped, or encountering any issues, along with additional details such as its process ID (PID), memory usage, and recent log entries.

        systemctl status <docker>

- This command utilizes the curl tool to send an HTTP HEAD request to the specified <publicIp:port>. It retrieves the headers of the response from the server without downloading the actual content. This is often used to check the availability and configuration of a web server running at the specified IP address and port.

        curl -I <publicIp:port>

- This command is used to display a list of active network connections on a Linux system. Specifically, it shows TCP connections (-t), numeric addresses instead of resolving hostnames (-n), and listening ports (-l). The -p option additionally displays the process ID (PID) and name of the program associated with each connection.

        netstat -ntlp

# 🔥 Docker Commands

    sudo docker rm $(sudo docker ps -aq)

- sudo docker ps -aq: This command lists all Docker container IDs, regardless of their running status. The -a flag ensures that both running and stopped containers are included, and the -q flag ensures that only the IDs are displayed, without any additional formatting.
- $(...): This is command substitution in Bash. It allows the output of one command to be used as an input for another command.
- sudo docker rm: This command is used to remove one or more Docker containers. When followed by a list of container IDs, it removes the specified containers.

When combined, $(sudo docker ps -aq) provides a list of all container IDs, which is then passed as arguments to sudo docker rm, effectively removing all Docker containers on the system, whether they are running or stopped.
































