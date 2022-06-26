* Local development => minikube. It only creates a *single-node cluster* which doesn't quite demonstrate all of the aspects of a complete kubernetes cluster.
* Hence it's recommended to start with cloud-based solutions.
* Beta project: Docker-in-Docker cluster, which can spin up a multi-node cluster on a single machine. 

**Installing Kubernetes on a Public Cloud Provider**
* AWS, Azure, GCP.

* **Google Kubernetes Engine**
    * GCP offers GKE - A hosted Kubernetes-as-a-service.
    * You need a GCP account with billing enabled and the gcloud tool installed.
    * *Setting a default zone*
        gcloud config set compute/zone us-west1-a

* **Installing Kubernetes on AWS** 
    * EKS => Elastic Kubernetes Service.
    * https://eksctl.io/
    * eksctl create cluster --help

**Running Kubernetes in Docker**
* This approach uses docker containers to simulate multiple kubernetes nodes instead of running eveything in virtual machine.
* kind(kubernetes in docker)
    kind create cluster --wait 5m \ 
    export KUBECONFIG="$(kind get kubeconfig-path)"
    kubectl cluster-info
    kind delete cluster

* Option in Docker desktop: Start a Kubernetes single-node cluster when starting Docker Desktop.

**The Kubernetes Client**
* kubectl: The command-line tool for interacting with the kubernetes API.
* It can be used to manage most kubernetes objects such as Pods, ReplicaSets and Services.

**Checking Cluster Status**
    * kubectl get componentstatuses
    *Component that make up the Kubernetes cluster*.
    Error from server (Forbidden): componentstatuses is forbidden: User "gagandeep.ahuja@razorpay.com" cannot list resource "componentstatuses" in API group "" at the cluster scope

    * kubectl get nodes

    * kubectl cluster-info
    * kubectl config -h
    * kubectl get pods -n kube-system

**To change cluster**
    * kubectl config use-context docker-desktop
    * kubectl get componentstatuses

* *Controller manager (controller-manager)*
    * Responsible for running various controllers that regulate behavior in the cluster. Eg. ensuring all of the replicas of a service are available and healthy.

* *scheduler*
    * Responsible for placing different pods onto different nodes in the cluster.

* *etcd*
    * Etcd server is the storage of the cluster where all API objects are stored.
    
**Listing Nodes in A Cluster**
* **kubectl get nodes**
* In Kubernetes, nodes are separated into:
    * *Master nodes*: They contain containers like the API server, scheduler, etc which manage the cluster.
    * *Worker nodes*: Nodes where our containers will run.
* Kubernetes won't generally schedule work on master nodes to ensure that user workload don't harm the overall operation of the cluster. 
* **kubectl describe nodes docker-desktop**
* Non-terminated Pods:  etcd, controller-manager, scheduler, apiserver.
* We can see the pods on the node, the CPU and memory that each pod is requesting from the node, as well as the total resources requested.
* Kubernetes tracks both the requests and upper limits for resources for each pod that runs on a machine.

**Cluster Components**
* One of the interesting aspects of kubernetes is that many of the components that make up the kubernetes cluster are deployed using kubernetes itself.
* All of these components run in the kube-system namespace.
* Namespace: An entity for organizing kubernetes resources. You can think of it like a folder in a filesystem.

**Kubernetes Proxy**
* Routes network traffic to load-balanced services in the kubernetes cluster.
* To do its job, the proxy must be present on every node in the cluster.
* K8s has an API object named DaemonSet that is used in many clusters to accomplish this.
* **kubectl get daemonSets -n kube-system kube-proxy**