In old days(Before Docker), only one application is running on server. 
<br>
IBM solves this problem by creating virtual machine. This machine allows multiple applications on the same server. But there was a problem that we need to download different os for different application in virtual machine. 
And another problem is dependency problems. 
<br>
Read more about Container and Docker: 
https://www.techwithkunal.com/blog/getting-started-with-docker
<br>

# Containers 
Containers allows multiple application to run on the same os inside containers using container engine. 
<br>
Container itself is an isolated environment.  
<br>
Download docker : https://docs.docker.com 
<br>
# Archietecture of Docker :
<img src="./d1.jpg" alt="docker">
<br>
<img src="./d2.jpg" alt="docker">
<br>
<img src="./d3.jpg" alt="docker">

# About Docker
<img src="./d4.jpg" alt="docker">
<br>
As there are many container runtime like runc,containerd and many more.So we are confused that we should use. 
<br>
For this there is a solution that is called "Open Container Intiative"
<br>
It is basically a project under the linux foundation.
<br>
The Open Container Initiative is an open governance structure for the express purpose of creating open industry standards around container formats and runtimes.
<br>
The OCI currently contains three specifications: the Runtime Specification (runtime-spec), the Image Specification (image-spec) and the Distribution Specification (distribution-spec)
<br>
OCI Runtime Specification : It defines how a container is started and run (e.g., runc, containerd).
<br>
OCI Image Specification : It  defines the format of container images (e.g., Docker and Podman images).
<br>
Distribution Specification : The OCI Distribution Specification defines how container images are stored, retrieved, and distributed across different container registries. It is based on Docker's registry HTTP API V2 and ensures interoperability between different container image registries.
<br>
A container registry is a centralized repository where container images are stored, managed, and distributed.
<br>
Interoperability : It allows different tools (e.g., Docker, Podman, containerd) to interact with OCI-compliant registries.
<br>
Read more at : https://opencontainers.org/about/overview/
<br>
# About Docker Basic Commands : 
Dockers is an isolated environment in which we are running images in the container.
<br>
An docker image also contains the smaller version of os which is used to run the main application we want to run.
<br>
-it: It is short form of interactive which means don't exit out from it.
<br>
Learn more about Docker Commands :
https://www.geeksforgeeks.org/docker-instruction-commands/
<br>
when we write commands like :
<br>
docker container exec -t <containerID> bash
<br>
It means bash is attached to that container.
<br>
This commands only works when the specific container is running.
<br>
docker container prune -f: It will delete all the stopped containers.
<br>
Alpine Images: The Alpine Linux image is a minimal, security-oriented, and lightweight Linux distribution. I It's commonly used in Docker images because of its small size and efficient nature.
<br>
Once we have pulled this image we can use the Linux based commands.
<br>
When we want to run an image in the background then we can run in the detatch mode :
<br>
"docker run -d alpine ping www.google.com"
<br>
Here after alpine "ping www.google.com" will go to the alpine terminal to execute it.
<br>
Any image that is running in docker container for that container base is linux kernel.
<br>
command : " docker run -d -p 8080:80 nginx"
<br>
Here this commands means forwards all the request to the localhost://8080 that we are making on the containers port 80.
<br>
We can find the logs of all the container by their id
<br>
docker logs <first four numbers or complete container id >
<br>
we can also find the logs of last n seconds:
<br>
docker logs --since 5s <container ID>
<br>
we can remove all the images by using commands :
```bash
docker rmi (docker images -q)
```
<br>
# How to create our own images :
```bash

1. First of all create a file named Dockerfile.

2. Write some code like :

FROM ubuntu
CMD ["echo", "Hello world"]

3. run the command: docker build  -t <imagename>: <version>

4. push the image to docker registry :

First of login using command: docker login

Then push the image using command: docker push <imagename>: <tag> 
here tag is also called version of the images. 
```

# Important Point from Docker engine: 
<img src="./de.jpg" alt="docker engine">
<br>
Explaination : 
<br>
when the client run commmand like "docker run hello world" on the terminal then it goes to the "docker daemon" ("docker daemon" is responsible for the networking job like pulling images and dealing with api etc). Then the command goes to "containerd" through "grpc"(a kind of remote procedural call) . "containerd" is not the one who is creating container out of images. "runc" is responsible for start/create or stop the containers. Once the containers starts then "shim" takesover all the responsibility from the runc and runc will go out of scope. Now "shim" manages how the containerd talks to running containers.
These are called daemon-less containers because once the daemon is down, the containers will still be running. 
