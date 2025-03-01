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

# About Docker Basic Commands :

Dockers is an isolated environment in which we are running images in the container.
<br>
An docker image also contains the smaller version of os which is used to run the main application we want to run.
<br>
Learn more about Docker Commands :
<br>
https://www.geeksforgeeks.org/docker-instruction-commands/
<br>

```bash

docker run -it ubuntu

-it: It is short form of interactive which means don't exit out from it.


when we write commands like :


"docker container exec -t <containerID> bash"


It means bash is attached to that container.


This commands only works when the specific container is running.


"docker container prune -f": It will delete all the stopped containers.


Alpine Images: The Alpine Linux image is a minimal, security-oriented, and lightweight Linux distribution. I It's commonly used in Docker images because of its small size and efficient nature.


Once we have pulled this image we can use the Linux based commands.


When we want to run an image in the background then we can run in the detatch mode :


"docker run -d alpine ping www.google.com"


Here after alpine "ping www.google.com" will go to the alpine terminal to execute it.


Any image that is running in docker container for that container base is linux kernel.


command : " docker run -d -p 8080:80 nginx"

Here this commands means forwards all the request to the "localhost://8080" that we are making on the containers port 80.

Here -p means publish

This command runs the nginx server 


We can find the logs of all the container by their id.

"docker logs <first four numbers or complete container id >"


we can also find the logs of last n seconds:

"docker logs --since 5s <container ID>"

We can also check the live logs on the terminal by :

"docker attach <container ID>"
this commands attach the container terminal to our terminal shows all the live logs.

we can remove all the images by using commands :
docker rmi (docker images -q)



# we can also use the mysql in the docker 
For this  : first of all we need to pull the "mysql" image . 

docker pull mysql 

Then run the mysql :

docker run  -e MYSQL_ROOT_PASSWORD='root' mysql 

Here -e means an environment variable which is used to store the mysql password.
As mysql is database so we need to pass the password to run the mysql. 

We can also run the mysql in the detached mode(In the background). 

Once the mysql is running in the detached mode we can enter into the mysql container by run the command : 

docker exec -it "Container ID or image name" bash 

After running this command : a bash shell will be visible. 
Then by entering the username and password we can enter into it. 

mysql -u root -p 
Then enter password : 

Then we can use msyql.  

# We can exit from any bash shell or mysql by running command :
exit 

```

<br>

# How to create our own images :

```bash

1. First of all create a file named Dockerfile.

2. Write some code like :

FROM ubuntu
CMD ["echo", "Hello world"]

// here ubuntu is base image 

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

# How to write DockerFile : 
Writing Dockerfile for a java application :
<br>
```bash 

# pull a base image which gives all required tools and libraries 
FROM openjdk:17-jdk-alpine 

# create a folder where app code will be stored 
WORKDIR /app 

# Copy the source code from host machine to your container folder  
COPY src/Main.java /app/Main.java 

# Compile the application code 
RUN javac Main.java 

# all the above line of code is an intermediate layer which builds the image. 

# Run the application 
CMD ["java","Main"] 

# Here CMD is not used for the building the image but it will execute when the image is run and it can be override while running the image. 

# We can also use "ENTRYPOINT" instead of "CMD" but it cannot be overrided 

```

<br>
Important Point : 
<br>
When we update our code on host system then we need to update the image and we can update the image in the same way which is used for creating the image : 
<br>

```bash 
docker build  -t <imagename>: <version> . 

// here "." denotes Dockerfile present in current directory. 

```

# 