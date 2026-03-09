# Kubernetes 
It is a container orchestration and an open-source platform designed to automate the deployment, scaling, and management of containerized applications. 

# Kubernetes Architecture : 
<img src="https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg" alt="Kubernetes Architecture Image">
<br>
A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes(Data plane), that run containerized applications. Every cluster needs at least one worker node in order to run Pods.
<br>
<b>Pod : </b>
<br>
Pod is the smallest and simplest deployable unit we can create and manage. 
A Pod encapsulates one or more containers (such as Docker) that are tightly coupled and need to share resources(network and volumes). 
<br>
To create a Pod, we define its configuration in a YAML file(pod.yaml) and then use the kubectl command-line tool to apply it to your cluster.
<br>
<b>Control Plane (Master Node) components </b>
<br>
<b>Kube-apiserver : </b>
<br>
The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.
<br>
Users interact with the Kube-apiserver. If user wants to create a pod then api-server intiate the request and store the pod information in etcd and it also checks which worker node is free and send this information to kube-schedular and then kube-schedular schedule the pod to worker node. 
<br>
<b>Scheduler : </b>
<br>
It watches for newly created Pods with no assigned node, and selects a node for them to run on. 
<br>
<b>etcd :</b> Refers to the standard Linux directory /etc and d: Stands for distributed. It serve as the primary distributed key-value store that holds all cluster data, including configuration, state, and metadata. 
<br>
<b> Controller Manager : </b>
<br>
It detects and run different type of controller like Replica set(for autoscaling), Node Controller. 
<br>
<b>Cloud Controller Manager : </b>
<br>
A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.
The cloud-controller-manager only runs controllers that are specific to your cloud provider. If you are running Kubernetes on your own premises, or in a learning environment inside your own PC, the cluster does not have a cloud controller manager. If user's kubernetes cluster has to create loadbalancer on cloud like aws then it will be handled by cloud-controller-manager. 
<br>
<b>Data Plane (Worker Node) components</b>
<br>
Kubelet : It is responsible for creation of pod and ensuring that the pod is always running.  If a container inside a pod crashes, the Kubelet sees this and restarts it automatically. If the entire pod is deleted or the node itself fails, the Kubelet cannot fix it. The Kubelet simply stops reporting a "Ready" status to the API Server. High-level controllers (like the Deployment or ReplicaSet controller) are the ones watching the API server. When they see the "actual state" (0 pods running) doesn't match the "desired state" (1 pod running), they are the ones that tell the API server to schedule a brand-new pod.
<br>
<b>CRI : </b> It Stands for Container Runtime Interface. It can be containrd, dockershim,etc which provide environment to run pods.
<br>
<b>Kube-proxy : </b> It provides networking, providing ip addresses and default load balancing capabilities.
<br>

Read More : https://kubernetes.io/docs/concepts/architecture/


# How to setup :
We need to install these packages on our machines:
<br>
kubeadm: the command to bootstrap the cluster.
<br>
kubelet: the component that runs on all of the machines in your cluster and does things like starting pods and containers.
<br>
kubectl: the command line util to talk to your cluster.
<br>
Learn More : https://kubernetes.io/docs/