# Docker
Docker is a software platform that allows you to build, test, and deploy applications quickly. Docker packages software into standardized units called containers that have everything the software needs to run including libraries, system tools, code, and runtime. Using Docker, you can quickly deploy and scale applications into any environment and know your code will run.

Docker enables developers to easily pack, ship, and run any application as a lightweight, portable, self-sufficient container, which can run virtually anywhere.

Docker provides the ability to package and run an application in a loosely isolated environment called a container.The isolation and security allows you to run many containers simultaneously on a given host. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work, and be sure that everyone you share with gets the same container that works in the same way.
# General Commands
- Start the docker daemon
```
docker -d
```
- Get help with Docker. Can also use –help on all subcommands
```
docker --help
```
- Display system-wide information
```
docker info
```
# Dockerfile
A Dockerfile contains the set of instructions for building a Docker Image. So, a Dockerfile is used to build a Docker Image which is then used as the template for creating one or more Docker containers. 

![IMG_256](images/001.png)

Image showing the steps to create a docker container. First you create the Dockerfile which is used to build the Docker Image which is finally used to run a Docker container.

It is a simple text file with a set of commands or instructions.

These commands/instructions are executed successively to perform actions on the base image to create a new docker image.

It will help you create custom Docker images.

Each instruction present in the docker file, represents a layer of the docker image.


# Docker images
Images are read-only templates containing instructions for creating a container. A Docker image creates containers to run on the Docker platform.

Docker images are a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

A Docker image is a file used to execute code in a Docker container. Docker images act as a set of instructions to build a Docker container, like a template.

The docker build command builds an image from a Dockerfile by reading the instructions from a Dockerfile.

Docker images act as a set of instructions to build a Docker container, like a template.

# Containers
Containers have everything that your code needs in order to run, down to a base operating system.

Containers are the structural units of Docker, which are used to hold the entire package that is needed to run the application.

Containers are packages of software that contain all of the necessary elements to run in any environment. In this way, containers virtualize the operating system and run anywhere, from a private data center to the public cloud or even on a developer's personal laptop.

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. 

**A container is a runtime instance of a docker image.** A container will always run the same, regardless of the infrastructure. 

These containers are compact, portable units in which you can start up an application quickly and easily.

# Containers v/s VMs OR Containerization v/s Virtualization
Containers and virtual machines are very similar resource virtualization technologies. Virtualization is the process in which a system singular resource like RAM, CPU, Disk, or Networking can be ‘virtualized’ and represented as multiple resources. The key differentiator between containers and virtual machines is that virtual machines virtualize an entire machine down to the hardware layers and containers only virtualize software layers above the operating system level.

![](images/002.png)

**Traditional Server Operations:**

- Before the advent of VMS (Virtual Machines) and containers, businesses operated by running applications on dedicated servers.
- Each server hosted only one application, leading to inefficiencies in resource utilization.

**Limitations of Traditional Approach:**

- Traditional servers had operating systems (Linux, Windows) that couldn't securely run multiple applications on a single server.
- Each new application required the purchase of a new server, resulting in wasted money and underutilized server capacity.

**Introduction of Virtual Machines:**

- Engineers developed virtual machines to address these issues.
- Virtual machines simulate hardware and software, allowing multiple applications to run on a single server securely.
- Hypervisors, such as VMware and Microsoft Hyper-V, enable the allocation and control of machine resources.

**Drawbacks of Virtual Machines:**

- Virtual machines can consume a significant amount of disk space, RAM, and CPU power.
- They are slow to start up, requiring time to boot, and each VM requires a separate operating system license.

**Introduction of Containers:**

- Containers are similar to VMS but differ in that they contain only the application, not an entire operating system.
- Containers package everything an application needs to run, making them highly portable across different computing environments.
- Docker is a leading software for creating, managing, and running containers.

**Advantages of Containers Over VMs:**

- Containers are lightweight, as they share the underlying operating system, leading to faster boot times.
- Containers consume less RAM and CPU power compared to virtual machines.
- Container files are smaller and more portable than VM files.

**Container Disadvantages:**

- Container files must be packaged to work with the same operating system as the server.
- If the underlying operating system crashes, all containers on that server are affected.

**Comparison of VMs and Containers:**

- VMs have larger file sizes, slower boot times, and can run any operating system.
- Containers are smaller, faster, but must match the server's operating system.

**Dual Usage of VMs and Containers:**

- Some organizations utilize both VMs and containers on the same server for maximum productivity.
- Servers run VMs, and within VMs, containers are used for specific applications.

## **Hypervisor** 
Hypervisor is a small layer that enables multiple operating systems to run alongside each other, sharing the same physical computing resources.

The software that enables the creation and management of virtual computing environments is called a hypervisor. It’s a software or firmware layer that sits between the physical hardware and the virtualized environments and allows multiple operating systems to run concurrently on a single physical machine. The hypervisor abstracts and partitions the underlying hardware resources, such as central processing units (CPUs), memory, storage, and networking, and allocates them to the virtual environments. 

Example

- Microsoft Hyper-V
- VMware
- Oracle VM VirtualBox

## OS Support and Architecture
![IMG_256](images/003.png)

VMs have the host OS and guest OS inside each VM. A guest OS can be any OS, like Linux or Windows, irrespective of the host OS. In contrast, Docker containers host on a single physical server with a host OS, which shares among them. Sharing the host OS between containers makes them light and increases the boot time. Docker containers are considered suitable to run multiple applications over a single OS kernel; whereas, virtual machines are needed if the applications or services required to run on different OS. 
# Docker Hub
Docker hub is the registry for docker images 

# Docker Extension for vs-code
![](images/004.png)
# Creating repository on docker hub and pushing a JS code on it
### **Step1: Create a docker file in the root directory of project**
![](images/005.png)

Must spell exactly same.
### **Step2: Add instruction in Docker-file to  package our application**
(1)
```
FROM node:alpine
```
- Typically we start from base images, this base image has bunch of file, we take those files and add additional files to it, we can start from Linux image and install node on top of it, as we have node.js project so we have to add it OR we can start from node image as this image is already build on top of Linux, these images are officially publish on docker hub

![](images/006.png)

- Docker hub is the registry for docker images.
- If you see docker hub, there are multiply node images, these node images are build on different distribution of Linux (different flavors of Linux). 

We can specify tag using colon(:) , to specify which Linux distribution we want to use, we are going to use **alpine** which is very small Linux distribution

(2)
```
COPY . /app
```
- Then we need to copy our application of program files
- COPY .(all the files) /app (into app directory) (into that image)
- Image have a file system, and in that file system we create app directory

(3)
```
CMD node app.js
```
- Command instruction to execute the command
- (node app.js) this command need to be executed to run the application but now this file is inside app directory so (/app/app.js)
- CMD node/app/app.js
- But we can set working directory so
```
WORKDIR /app
```
- After this instruction all the following instruction assume that we are currently inside app directory. So we don’t need to write /app every time

**All instructions**
```
FROM node:alpine

COPY . /app

WORKDIR /app

CMD node app.js
```
So, these instruction clearly documented the deployment process

### **Step3: Tell docker to package our application**
**.docker build -t**(tag) **hello-docker**(name) **.** (where are docker file is, as it is in same directory)
```
docker build -t hello-docker .
```
![](images/007.png)

**Note:** Docker should be running in the background

### **Step4: Where is the docker image which is build**
To see all the images on the computer
```
docker images
```
OR
```
docker image ls
```
![](images/008.png)
### **Step5: Run image**
Now we can run the images on any computer that have docker, we don’t need to take care of node environment etc.
```
docker run hello-docker
```
![](images/009.png)

It does not depend on which repository we are in, it will run as it contain all the things ro run the application

![](images/010.png)

### **Step6: Upload Image to docker hub (Creating repository in cmd) - way 1**

Run following commandc
```
docker tag nameOfImage username/repositoryName:version
```
Note: And name to repository should be in lowercase.
```
docker tag hello-docker muhammadnaqeeb/hello-docker:v1.0
```
![](images/011.png)

Run login command only first time
```
docker login
```

Push the image

```
docker push muhammadnaqeeb/hello-docker:v1.0
```
![](images/012.png)

![](images/013.png)


### **Step6: Upload Image to docker hub (Creating repository online) - way 2**
If you done this step on CMD, then there is no need for this step, only use one way

![](images/014.png)

All steps will be same as way 1

# Docker Play
<https://labs.play-with-docker.com/>

This website has virtual environment of Linux, it is a complete OS where you can pull your images and rum them. It has Linux and docker only

![](images/015.png)

![](images/016.png)

It don’t have node or anythink else

![](images/017.png)

# Pull Docker Image and Run it
**Pull**
```
docker pull muhammadnaqeeb/hello-docker:v1.0
```
**Run**

docker run muhammadnaqeeb/hello-docker:v1.0
# Delete an Image
```
docker rmi <image_name>
```
This will delete the repository, but if it is in running mode it will not get deleted

A container is a runnable instance of an image. which is why you cannot delete an image if there is a running container from that image. You just need to delete the container first.

|**docker ps -a**|Lists containers (and tells you which images they are spun from)|
| - | - |
|**docker images**| Lists images |
|**docker rm <container\_id>**| Removes a stopped container|
|**docker rm -f <container\_id>**| Forces the removal of a running container (uses SIGKILL)|
|**docker rmi <image\_id>**|<p> Removes an image </p><p>Will fail if there is a running instance of that image i.e. container</p>|
|**docker rmi -f <image\_id>** |<p> Forces removal of image even if it is referenced in multiple repositories, </p><p>i.e. same image id given multiple names/tags </p><p>Will still fail if there is a docker container referencing image</p>|

- As I am trying to delete image but it is giving me error

![](images/018.png)

- Fail because there is a running instance of that image i.e. container

Run ps command to see running containers

![](images/019.png)

- Stop the container

![](images/020.png)

- See we have one image

![](images/021.png)

- Delete image

![](images/022.png)

- No image left after delete

![](images/023.png)

