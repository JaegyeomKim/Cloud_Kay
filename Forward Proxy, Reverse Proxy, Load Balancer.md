1- Proxy
  
2- Forward Proxy

3- Reverse Proxy

4- Load Balancer


**1. Proxy**
  : agent, substitute

1-2. Proxy Server
  : Intermediary Server

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/0942c373-d833-4eb8-882d-e520384a6781)

A proxy server is an intermediary server that acts as a gateway between clients and other servers.
Proxy servers are commonly used for various purposes including 

  - improving security
  - enhancing privacy
  - caching content
  - controlling access to resources
  - optimizing network performance
  
1-3. Types of Proxy

  - Forward Proxy
  - Reverse Proxy

**2. Forward Proxy**

  - caching content

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/b537dc99-8f79-4f97-b58c-d0d54938cc50)

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/448d10d2-26de-4b08-b079-c5adc86bca5b)


  - Anonymity

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/9592bfe9-7b3f-4612-9403-2f70277b5fdf)

**  3. Reverse Proxy **

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/55da6b34-8d9b-4269-a7ea-7cef337e8db3)

  - caching content
      - same as forward proxy

  - Security
    - can hide server information from clients
    - The actual server IP is not exposed.
   
  ** 4. Load Balancer **
  
A load balancer is a device or software application that evenly distributes incoming network traffic across multiple servers to optimize resource utilization and ensure high availability of services.

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/9d168813-4467-4e0f-ab9a-33dfde8ad79f)

![image](https://github.com/JaegyeomKim/Cloud_Kay/assets/77129961/31054d17-1a44-4ec0-b5a9-3d64c5b744df)

L4 Load Balancer: Operates at the transport layer (Layer 4) of the OSI model, mainly focusing on routing and load balancing based on IP addresses and port numbers. It distributes traffic based on network-level information such as TCP/UDP data.

ex/ 

  https://github.com/JaegyeomKim 

  access 

  Server A, Server B


L7 Load Balancer: Operates at the application layer (Layer 7) of the OSI model, providing more advanced features such as content-based routing and SSL termination. It can inspect the application data and make routing decisions based on content, URLs, cookies, or other application-specific criteria.

  https://github.com/JaegyeomKim 

  access 

  /Cloud_Kay or /Profile
