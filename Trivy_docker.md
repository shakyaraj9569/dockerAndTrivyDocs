  # Trivy Installation and Usage

## Table of content

[1.Trivy](#trivy)

[2.Installation of Trivy](#step-1--installation-of-trivy-on-the-ubuntu)

[3.Docker](#docker)

[4.Installation of Docker](#installation-of-docker)

[5.Dockerhub](#dockerhub)

[6.How to pull images from docker hub](#how-to-pull-images-from-docker)

[7.How to Create your own docker image from dockerfile](#how-to-create-your-own-docker-image-from-dockerfile)

[8.Scan docker images using trivy](#step-2--scan-docker-images-using-trivy)




## Trivy
Trivy is a security scanning tool designed for container images, helping to identify vulnerabilities and security issues within the software components contained in those images. In simple terms, it's like a security guard that checks the packages inside a box (container image) to make sure they don't have any known security problems.

Here's a breakdown:

### Container Images: 
* When developers create software applications, they often package them into container images. These images are like pre-packaged boxes containing everything needed for the application to run.
  
### Security Scanning: 
* Trivy focuses on inspecting these container images for potential security risks. It looks at the individual pieces (libraries, frameworks, etc.) inside the image to see if they have any known vulnerabilities or weaknesses.
* 
### Vulnerability Detection: 
* Trivy uses a database of known vulnerabilities to compare against the components in the container image. If it finds any matches, it alerts the user, helping them identify and fix potential security issues before deploying the application.
  
  ___
## Prerequisite
```
Name:"Ubuntu"
Vesrion:"20.04.6"
```

## Step 1 : Installation of Trivy on the Ubuntu


**1: Install Trivy**
```
sudo dpkg -i trivy_0.21.0_Linux-64bit.deb
```
```
Output

rajshakya@thunder:~$ sudo dpkg -i trivy_0.21.0_Linux-64bit.deb
dpkg: warning: downgrading trivy from 0.47.0 to 0.21.0
(Reading database ... 178716 files and directories currently installed.)
Preparing to unpack trivy_0.21.0_Linux-64bit.deb ...
Unpacking trivy (0.21.0) over (0.47.0) ...
Setting up trivy (0.21.0) ...

```

**2: Install Dependencies**
```
sudo apt-get install -f
```
```
Output

rajshakya@thunder:~$ sudo apt-get install -f
Reading package lists... Done
Building dependency tree       
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
```

*This command will automatically install any dependencies that Trivy requires.*

**3: Verify Installation**
```
trivy --version
```
*If above command does not work you can use (sudo trivy --version)*
```
Output

rajshakya@thunder:~$ trivy --version
Version: 0.21.0
```

*This method directly installs the Trivy binary without relying on the package manager, and it might resolve the issue you encountered earlier. Remember to replace the download URL and filename with the correct version you want to install*


  ## Docker
  Docker is a platform that enables developers to package their applications and all their dependencies into a standardised unit called a "container." These containers can then be easily transported between different environments, ensuring that the application runs consistently, regardless of where it is deployed.
  
Here's a breakdown of the key concepts in Docker:

  #### 1: Containerization:

  Containers: Think of a container as a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools. Containers are isolated from the underlying system and from other containers, ensuring consistency and reproducibility.


#### 2: Docker Images:

 A Docker image is a snapshot or template of a container. It contains the application code and all its dependencies, organized in layers. Images serve as the blueprint for creating containers.

#### 3: Docker Engine:
The Docker engine is the software that enables the creation, management, and running of containers. It includes a server, a REST API, and a command-line interface (CLI) for interacting with containers.

#### 4: Docker Hub:

Docker Hub is a cloud-based registry where developers can share and distribute Docker images. It's a central repository for Docker images, and you can find both official and community-contributed images for various applications and services.

## How Docker Works:

**Development:** Developers build and test their applications inside Docker containers on their local machines. This ensures that the application runs consistently across different development environments.

**Deployment:** Once the application is ready, the same Docker container can be deployed to various environments, such as development, testing, staging, and production. This minimizes the "it works on my machine" problem.


**Isolation:** Containers provide process and filesystem isolation, allowing multiple applications to run independently on the same host. This isolation helps prevent conflicts between dependencies and ensures security.

**Resource Efficiency:** Containers share the host operating system's kernel, making them lightweight and efficient. They start quickly, use fewer resources, and can be easily scaled up or down based on demand.

## Benefits of Docker:
 Consistency: Docker ensures that the application runs the same way everywhere, reducing the "it works on my machine" problem.

**Portability:** Containers can be moved and executed on any system that supports Docker, providing a consistent environment.
Scalability: Docker allows for easy scaling of applications by running multiple instances of containers.

**DevOps Integration:** Docker is widely used in DevOps practices, enabling continuous integration, continuous delivery, and automation of the software development lifecycle.

In summary, Docker simplifies the process of developing, packaging, and deploying applications, providing a standardised and efficient way to manage software across different environments.

## Installation of docker

**1: Update the package database** 
```
sudo apt-get update
```

**2: Install necessary packages**
```
# Copy Command

sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
```
```
Output

rajshakya@thunder:~$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  python3-certifi python3-requests python3-requests-unixsocket
Suggested packages:
  python3-openssl python3-socks
The following NEW packages will be installed:
  apt-transport-https ca-certificates curl python3-certifi python3-requests
  python3-requests-unixsocket software-properties-common
0 upgraded, 7 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B/529 kB of archives.
After this operation, 1,769 kB of additional disk space will be used.
Preconfiguring packages ...
Selecting previously unselected package ca-certificates.
(Reading database ... 178216 files and directories currently installed.)
Preparing to unpack .../0-ca-certificates_20230311ubuntu0.20.04.1_all.deb ...
Unpacking ca-certificates (20230311ubuntu0.20.04.1) ...
Selecting previously unselected package apt-transport-https.
Preparing to unpack .../1-apt-transport-https_2.0.10_all.deb ...
Unpacking apt-transport-https (2.0.10) ...
Selecting previously unselected package curl.
Preparing to unpack .../2-curl_7.68.0-1ubuntu2.20_amd64.deb ...
Unpacking curl (7.68.0-1ubuntu2.20) ...
Selecting previously unselected package python3-certifi.
Preparing to unpack .../3-python3-certifi_2019.11.28-1_all.deb ...
Unpacking python3-certifi (2019.11.28-1) ...
Selecting previously unselected package python3-requests.
Preparing to unpack .../4-python3-requests_2.22.0-2ubuntu1.1_all.deb ...
Unpacking python3-requests (2.22.0-2ubuntu1.1) ...
Selecting previously unselected package python3-requests-unixsocket.
Preparing to unpack .../5-python3-requests-unixsocket_0.2.0-2_all.deb ...
Unpacking python3-requests-unixsocket (0.2.0-2) ...
Selecting previously unselected package software-properties-common.
Preparing to unpack .../6-software-properties-common_0.99.9.12_all.deb ...
Unpacking software-properties-common (0.99.9.12) ...
Setting up apt-transport-https (2.0.10) ...
Setting up ca-certificates (20230311ubuntu0.20.04.1) ...
Updating certificates in /etc/ssl/certs...
137 added, 0 removed; done.
Setting up python3-certifi (2019.11.28-1) ...
Setting up python3-requests (2.22.0-2ubuntu1.1) ...
Setting up curl (7.68.0-1ubuntu2.20) ...
Setting up python3-requests-unixsocket (0.2.0-2) ...
Setting up software-properties-common (0.99.9.12) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for dbus (1.12.16-2ubuntu2.3) ...
Processing triggers for ca-certificates (20230311ubuntu0.20.04.1) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
```


**3: Add the official GPG key for Docker**
```
sudo sh -c 'curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg'
```

```
Output

rajshakya@thunder:~$ sudo sh -c 'curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg'
```
**4: Set up the Docker stable repository**
```
echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
Output

rajshakya@thunder:~$ echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```


  *For a different distribution, replace $(lsb_release -cs) with the codename of your distribution.*

**5: Update the package database again**
```
sudo apt-get update
```
```
Output

rajshakya@thunder:~$ sudo apt-get update
Get:1 https://download.docker.com/linux/ubuntu focal InRelease [57.7 kB]
Get:2 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages [33.8 kB]          
Hit:3 http://packages.microsoft.com/repos/code stable InRelease                               
Hit:4 http://in.archive.ubuntu.com/ubuntu focal InRelease                                     
Hit:5 https://aquasecurity.github.io/trivy-repo/deb focal InRelease 
Hit:6 http://in.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:7 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:8 http://in.archive.ubuntu.com/ubuntu focal-backports InRelease
Fetched 91.5 kB in 1s (89.9 kB/s)
Reading package lists... Done
```

**6: Install Docker**
```
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```

```
Output

rajshakya@thunder:~$ sudo apt-get install docker-ce docker-ce-cli containerd.io -y
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  docker-buildx-plugin docker-ce-rootless-extras docker-compose-plugin pigz slirp4netns
Suggested packages:
  aufs-tools cgroupfs-mount | cgroup-lite
The following NEW packages will be installed:
  containerd.io docker-buildx-plugin docker-ce docker-ce-cli docker-ce-rootless-extras
  docker-compose-plugin pigz slirp4netns
0 upgraded, 8 newly installed, 0 to remove and 0 not upgraded.
Need to get 28.7 MB/114 MB of archives.
After this operation, 409 MB of additional disk space will be used.
Get:1 https://download.docker.com/linux/ubuntu focal/stable amd64 containerd.io amd64 1.6.25-1 [28.7 MB]
Fetched 28.7 MB in 17s (1,652 kB/s)                                                           
Selecting previously unselected package pigz.
(Reading database ... 178462 files and directories currently installed.)
Preparing to unpack .../0-pigz_2.4-1_amd64.deb ...
Unpacking pigz (2.4-1) ...
Selecting previously unselected package containerd.io.
Preparing to unpack .../1-containerd.io_1.6.25-1_amd64.deb ...
Unpacking containerd.io (1.6.25-1) ...
Selecting previously unselected package docker-buildx-plugin.
Preparing to unpack .../2-docker-buildx-plugin_0.11.2-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-buildx-plugin (0.11.2-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-ce-cli.
Preparing to unpack .../3-docker-ce-cli_5%3a24.0.7-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-ce-cli (5:24.0.7-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-ce.
Preparing to unpack .../4-docker-ce_5%3a24.0.7-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-ce (5:24.0.7-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-ce-rootless-extras.
Preparing to unpack .../5-docker-ce-rootless-extras_5%3a24.0.7-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-ce-rootless-extras (5:24.0.7-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-compose-plugin.
Preparing to unpack .../6-docker-compose-plugin_2.21.0-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-compose-plugin (2.21.0-1~ubuntu.20.04~focal) ...
Selecting previously unselected package slirp4netns.
Preparing to unpack .../7-slirp4netns_0.4.3-1_amd64.deb ...
Unpacking slirp4netns (0.4.3-1) ...
Setting up slirp4netns (0.4.3-1) ...
Setting up docker-buildx-plugin (0.11.2-1~ubuntu.20.04~focal) ...
Setting up containerd.io (1.6.25-1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Setting up docker-compose-plugin (2.21.0-1~ubuntu.20.04~focal) ...
Setting up docker-ce-cli (5:24.0.7-1~ubuntu.20.04~focal) ...
Setting up pigz (2.4-1) ...
Setting up docker-ce-rootless-extras (5:24.0.7-1~ubuntu.20.04~focal) ...
Setting up docker-ce (5:24.0.7-1~ubuntu.20.04~focal) ...
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.22) ...

```
**7: Start the Docker service**
```
sudo systemctl start docker
```
```
Output

rajshakya@thunder:~$ sudo systemctl start docker
```
**8: Enable Docker to start on boot**

```
sudo systemctl enable docker
```
```
Output

rajshakya@thunder:~$ sudo systemctl enable docker
```
**9: Verify the installation**
```
sudo docker run hello-world
```
```

Output

rajshakya@thunder:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete 
Digest: sha256:c79d06dfdfd3d3eb04cafd0dc2bacab0992ebc243e083cabe208bac4dd7759e0
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

rajshakya@thunder:~$ 
```
*This command should download a test image and run a container that prints a "Hello from Docker" message.*

## Dockerhub
Docker Hub is like a big online warehouse for software. Imagine you have a set of tools (software applications) that you want to share with others or use on different computers easily. Docker Hub helps with that.

Here's how it works:

**1:Containers** Think of containers as boxes that have everything a piece of software needs to run – the code, libraries, and settings. Docker helps pack all of this neatly into a container.


**2:Sharing Containers** Now, if you make a really useful container with, let's say, a cool website inside, you can share it with others. Docker Hub is where you upload (store) your containers so that anyone around the world can easily download and use them.


**3:Easy Access** When someone needs your cool website container, they just go to Docker Hub, search for it, and download it. It's like picking something from a digital store shelf.


**4:Versions and Updates** Docker Hub also keeps track of different versions of containers. So, if you improve your cool website and make version 2.0, people can choose which version they want.




## How to pull images from docker
To pull Docker images from Docker Hub, follow these steps:

**1: Open a Terminal** 

Open your terminal or command prompt on your system.


**2: Pull the Docker Image** 

Use the docker pull command followed by the name of the image you want to pull. Most images on Docker Hub follow the format repository:tag, where the tag is optional. If no tag is specified, Docker assumes the latest tag.

*For example, to pull the official redis image, you can use*  
```
docker pull redis.
```
```
Output

rajshakya@thunder:~$ sudo docker pull redis
Using default tag: latest
latest: Pulling from library/redis
1f7ce2fa46ab: Pull complete 
3c6368585bf1: Pull complete 
3911d271d7d8: Pull complete 
ac88aa9d4021: Pull complete 
127cd75a68a2: Pull complete 
4f4fb700ef54: Pull complete 
f3993c1104fc: Pull complete 
Digest: sha256:2976bc0437deff693af2dcf081a1d1758de8b413e6de861151a5a136c25eb9e4
Status: Downloaded newer image for redis:latest
docker.io/library/redis:latest

```
If you want a specific version, you can specify the tag, like:
```
docker pull redis:6.2.14-alpine3.18
```
```
Output

rajshakya@thunder:~$ sudo docker pull redis:6.2.14-alpine3.18
6.2.14-alpine3.18: Pulling from library/redis
96526aa774ef: Pull complete 
78d425aaa4a7: Pull complete 
f2eb244f70f4: Pull complete 
e25dbaa2aaa3: Pull complete 
d1c4499c2d96: Pull complete 
4f4fb700ef54: Pull complete 
a2e8e402a47a: Pull complete 
Digest: sha256:80cc8518800438c684a53ed829c621c94afd1087aaeb59b0d4343ed3e7bcf6c5
Status: Downloaded newer image for redis:6.2.14-alpine3.18
docker.io/library/redis:6.2.14-alpine3.18

```
Replace redis with the name of the image you want to pull.

**3: Check the Pulled Image** 

Once the image is pulled, you can check the list of locally available images using the following command: 
```
sudo docker images 
```
```
Output

rajshakya@thunder:~$ sudo docker images
REPOSITORY    TAG                 IMAGE ID       CREATED        SIZE
my-node-app   latest              3ded9c300ee4   22 hours ago   912MB
image2        2.0                 c8be5e8f2954   42 hours ago   159MB
myimage1      1.0                 ef6298b6d427   43 hours ago   124MB
redis         6.2.14-alpine3.18   c9052246611f   13 days ago    33.1MB
redis         7.2.3               961dda256baa   13 days ago    138MB
redis         latest              961dda256baa   13 days ago    138MB
ubuntu        latest              e4c58958181a   7 weeks ago    77.8MB
ubuntu        20.04               bf40b7bc7a11   7 weeks ago    72.8MB
hello-world   latest              9c7a54a9a43c   6 months ago   13.3kB

```
*This command will display a list of Docker images on your system.*

**4: Run a Container from the Pulled Image (Optional)**

If you want to run a container based on the pulled image, you can use the docker run command. For example: 
```
sudo docker run -it redis
```
```
Output

rajshakya@thunder:~$ sudo docker run -it redis:latest
1:C 24 Nov 2023 05:21:58.460 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
1:C 24 Nov 2023 05:21:58.460 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 24 Nov 2023 05:21:58.460 * Redis version=7.2.3, bits=64, commit=00000000, modified=0, pid=1, just started
1:C 24 Nov 2023 05:21:58.460 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 24 Nov 2023 05:21:58.461 * monotonic clock: POSIX clock_gettime
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 7.2.3 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                  
 (    '      ,       .-`  | `,    )     Running in standalone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     PID: 1
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           https://redis.io       
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

1:M 24 Nov 2023 05:21:58.462 * Server initialized
1:M 24 Nov 2023 05:21:58.462 * Ready to accept connections tcp



```

*This command will start an interactive shell session in a new container based on the redis image.*

Remember that pulling images requires an internet connection, as Docker downloads the images from Docker Hub or another specified registry.

Docker Hub is a popular registry for Docker images, and you can find a wide variety of images there. If you're pulling images from a different registry, you might need to log in using the docker login command before pulling the image. The login command typically requires your Docker Hub username and password.

For more detailed information on using Docker commands, you can always refer to the official Docker documentation.

# How to Create your own docker image from dockerfile
**1: Install Docker** 

Make sure Docker is installed on your Linux machine. You can follow the official Docker installation guide for your distribution.If you have already installed it so you can skip this step.

**2: Create a Dockerfile**

 A Dockerfile is a script that contains instructions for building a Docker image. Create a new file named Dockerfile in your project directory,Copy the whole steps as it is.
 
 **Step1:** Create Directory/Folder, using command
 ```
 mkdir Example_Dockerfile
 cd Example_Dockerfile/
 ```
 ```
 Output

rajshakya@thunder:~$ mkdir Example_Dockerfile
rajshakya@thunder:~$ cd Example_Dockerfile/
 ```

 **Step2:** create Dockerfile named Dockerfile 
```
touch Dockerfile
```
```
Output

rajshakya@thunder:~/Example_Dockerfile$ touch Dockerfile
```

**Step3:** Go into the dockerfile and copy the code given below
```
vim Dockerfile
```
```
# Copy Code

FROM ubuntu:20.04

# Set the working directory
WORKDIR /app

# Copy application files into the container
COPY . /app

# Install dependencies
RUN apt-get update && \
apt-get install -y python3

# Define the command to run your application
CMD ["python3", "app.py"]
```

```
Output

rajshakya@thunder:~/Example_Dockerfile$ vim Dockerfile

# Copy Code

FROM ubuntu:20.04

# Set the working directory
WORKDIR /app

# Copy application files into the container
COPY . /app

# Install dependencies
RUN apt-get update && \
apt-get install -y python3

# Define the command to run your application
CMD ["python3", "app.py"]
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
~                                                                              
-- INSERT --                                                 16,25         All
```

**NOTE:** This is a simple example for a Python application using Ubuntu 20.04 as the base image.

**3: Build the Docker Image** 

Open a terminal in the directory containing your Dockerfile and run the following command:
```
sudo docker build -t image2::2.0 .
```

```
Output

rajshakya@thunder:~/Dockerfile2$ sudo docker build -t image2:2.0 .
[+] Building 484.9s (9/9) FINISHED                                                 docker:default
 => [internal] load build definition from Dockerfile                                         0.0s
 => => transferring dockerfile: 303B                                                         0.0s
 => [internal] load .dockerignore                                                            0.0s
 => => transferring context: 2B                                                              0.0s
 => [internal] load metadata for docker.io/library/ubuntu:20.04                             43.7s
 => [1/4] FROM docker.io/library/ubuntu:20.04@sha256:ed4a42283d9943135ed87d4ee34e542f7f5a  329.9s
 => => resolve docker.io/library/ubuntu:20.04@sha256:ed4a42283d9943135ed87d4ee34e542f7f5ad9  0.0s
 => => sha256:ed4a42283d9943135ed87d4ee34e542f7f5ad9ecf2f244870e23122f703f9 1.13kB / 1.13kB  0.0s
 => => sha256:218bb51abbd1864df8be26166f847547b3851a89999ca7bfceb85ca9b5d2e95d 424B / 424B   0.0s
 => => sha256:bf40b7bc7a11b43785755d3c5f23dee03b08e988b327a2f10b22d01d5dc52 2.30kB / 2.30kB  0.0s
 => => sha256:96d54c3075c9eeaed5561fd620828fd6bb5d80ecae7cb25f9ba5f7d88 27.51MB / 27.51MB  328.6s
 => => extracting sha256:96d54c3075c9eeaed5561fd620828fd6bb5d80ecae7cb25f9ba5f7d88ea6e15c    1.1s
 => [internal] load build context                                                            0.0s
 => => transferring context: 303B                                                            0.0s
 => [2/4] WORKDIR /app                                                                       0.2s
 => [3/4] COPY . /app                                                                        0.0s
 => [4/4] RUN apt-get update && apt-get install -y python3                                 110.3s
 => exporting to image                                                                       0.6s
 => => exporting layers                                                                      0.6s
 => => writing image sha256:c8be5e8f2954bbed91eabeb47b94a025e4e14e05055f282ccb48084765e536d  0.0s 
 => => naming to docker.io/library/image2:2.0                                                0.0s 
rajshakya@thunder:~/Dockerfile2$ sudo docker images
REPOSITORY    TAG       IMAGE ID       CREATED             SIZE                                   
image2        2.0       c8be5e8f2954   38 seconds ago      159MB
myimage1      1.0       ef6298b6d427   About an hour ago   124MB
hello-world   latest    9c7a54a9a43c   6 months ago        13.3kB

```

**NOTE:** Replace your-image-name with the desired name for your image and tag with a version or label. The . at the end specifies the build context, which is the current directory.



*Now you've created your own Docker image. You can customize the Dockerfile based on your specific application and requirements.*

## Step 2 : Scan docker images using trivy

**1: Get docker images**

Run command :
```
Copy Command

sudo docker images
```
```
Output

rajshakya@thunder:~$ sudo docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
image2        2.0       c8be5e8f2954   5 hours ago    159MB
myimage1      1.0       ef6298b6d427   7 hours ago    124MB
redis         latest    961dda256baa   12 days ago    138MB
ubuntu        latest    e4c58958181a   6 weeks ago    77.8MB
hello-world   latest    9c7a54a9a43c   6 months ago   13.3kB

```
*From this you command you can get the docker image list.*

**2: Scan vulnerabilities of docker images using trivy**

Run command :
```
Copy Command

sudo trivy image --severity HIGH,CRITICAL (IMAGE ID)
```
```
rajshakya@thunder:~$ sudo trivy image --severity CRITICAL,HIGH 961dda256baa
2023-11-22T21:59:07.215+0530	INFO	Vulnerability scanning is enabled
2023-11-22T21:59:07.215+0530	INFO	Secret scanning is enabled
2023-11-22T21:59:07.215+0530	INFO	If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2023-11-22T21:59:07.215+0530	INFO	Please see also https://aquasecurity.github.io/trivy/v0.47/docs/scanner/secret/#recommendation for faster secret detection
2023-11-22T21:59:11.950+0530	INFO	Detected OS: debian
2023-11-22T21:59:11.950+0530	INFO	Detecting Debian vulnerabilities...
2023-11-22T21:59:11.993+0530	INFO	Number of language-specific files: 1
2023-11-22T21:59:11.993+0530	INFO	Detecting gobinary vulnerabilities...

961dda256baa (debian 12.2)

Total: 16 (HIGH: 15, CRITICAL: 1)

┌────────────────┬────────────────┬──────────┬──────────────┬───────────────────┬───────────────┬──────────────────────────────────────────────────────────────┐
│    Library     │ Vulnerability  │ Severity │    Status    │ Installed Version │ Fixed Version │                            Title                             │
├────────────────┼────────────────┼──────────┼──────────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libssl3        │ CVE-2023-5678  │ HIGH     │ affected     │ 3.0.11-1~deb12u2  │               │ openssl: Generating excessively long X9.42 DH keys or        │
│                │                │          │              │                   │               │ checking excessively long X9.42...                           │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-5678                    │
├────────────────┼────────────────┤          ├──────────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ linux-libc-dev │ CVE-2013-7445  │          │ will_not_fix │ 6.1.55-1          │               │ kernel: memory exhaustion via crafted Graphics Execution     │
│                │                │          │              │                   │               │ Manager (GEM) objects                                        │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2013-7445                    │
│                ├────────────────┤          ├──────────────┤                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-19449 │          │ fix_deferred │                   │               │ kernel: mounting a crafted f2fs filesystem image can lead to │
│                │                │          │              │                   │               │ slab-out-of-bounds read...                                   │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2019-19449                   │
│                ├────────────────┤          ├──────────────┤                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-19814 │          │ affected     │                   │               │ kernel: out-of-bounds write in __remove_dirty_segment in     │
│                │                │          │              │                   │               │ fs/f2fs/segment.c                                            │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2019-19814                   │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2021-3847  │          │              │                   │               │ low-privileged user privileges escalation                    │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2021-3847                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2021-3864  │          │              │                   │               │ descendant's dumpable setting with certain SUID binaries     │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2021-3864                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-2176  │          │              │                   │               │ Slab-out-of-bound read in compare_netdev_and_ip              │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-2176                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-35827 │          │              │                   │               │ race condition leading to use-after-free in ravb_remove()    │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-35827                   │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-3640  │          │              │                   │               │ Kernel: x86/mm: a per-cpu entry area leak was identified     │
│                │                │          │              │                   │               │ through the init_cea_offsets...                              │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-3640                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-46813 │          │              │                   │               │ kernel: SEV-ES local priv escalation                         │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-46813                   │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-5178  │          │              │                   │               │ kernel: use after free in nvmet_tcp_free_crypto in NVMe      │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-5178                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-5345  │          │              │                   │               │ kernel: use-after-free vulnerability in the smb client       │
│                │                │          │              │                   │               │ component                                                    │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-5345                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-5633  │          │              │                   │               │ kernel: vmwgfx: reference count issue leads to               │
│                │                │          │              │                   │               │ use-after-free in surface handling                           │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-5633                    │
│                ├────────────────┤          │              │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-5717  │          │              │                   │               │ kernel: A heap out-of-bounds write                           │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-5717                    │
├────────────────┼────────────────┤          │              ├───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ perl-base      │ CVE-2023-31484 │          │              │ 5.36.0-7          │               │ perl: CPAN.pm does not verify TLS certificates when          │
│                │                │          │              │                   │               │ downloading distributions over HTTPS...                      │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
├────────────────┼────────────────┼──────────┼──────────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ zlib1g         │ CVE-2023-45853 │ CRITICAL │ will_not_fix │ 1:1.2.13.dfsg-1   │               │ zlib: integer overflow and resultant heap-based buffer       │
│                │                │          │              │                   │               │ overflow in zipOpenNewFileInZip4_6                           │
│                │                │          │              │                   │               │ https://avd.aquasec.com/nvd/cve-2023-45853                   │
└────────────────┴────────────────┴──────────┴──────────────┴───────────────────┴───────────────┴──────────────────────────────────────────────────────────────┘

usr/local/bin/gosu (gobinary)

Total: 1 (HIGH: 1, CRITICAL: 0)

┌────────────────────────────────┬────────────────┬──────────┬────────┬───────────────────┬───────────────┬──────────────────────────────────────────────────┐
│            Library             │ Vulnerability  │ Severity │ Status │ Installed Version │ Fixed Version │                      Title                       │
├────────────────────────────────┼────────────────┼──────────┼────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────┤
│ github.com/opencontainers/runc │ CVE-2023-27561 │ HIGH     │ fixed  │ v1.1.0            │ 1.1.5         │ runc: volume mount race condition (regression of │
│                                │                │          │        │                   │               │ CVE-2019-19921)                                  │
│                                │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2023-27561       │
└────────────────────────────────┴────────────────┴──────────┴────────┴───────────────────┴───────────────┴──────────────────────────────────────────────────┘
```

```
Another example of scanning image through trivy

rajshakya@thunder:~$ sudo trivy image --severity CRITICAL,HIGH c8be5e8f2954
2023-11-22T21:55:02.024+0530	INFO	Vulnerability scanning is enabled
2023-11-22T21:55:02.024+0530	INFO	Secret scanning is enabled
2023-11-22T21:55:02.024+0530	INFO	If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2023-11-22T21:55:02.025+0530	INFO	Please see also https://aquasecurity.github.io/trivy/v0.47/docs/scanner/secret/#recommendation for faster secret detection
2023-11-22T21:55:05.747+0530	INFO	Detected OS: ubuntu
2023-11-22T21:55:05.747+0530	INFO	Detecting Ubuntu vulnerabilities...
2023-11-22T21:55:05.753+0530	INFO	Number of language-specific files: 0

c8be5e8f2954 (ubuntu 20.04)

Total: 0 (HIGH: 0, CRITICAL: 0)
k8i
```


