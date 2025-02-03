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
Containers itself an isolated environment.  
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


