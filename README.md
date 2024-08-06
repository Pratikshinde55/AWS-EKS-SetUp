
kubernetes is Container cluster management tool.

 # Elastic Kubernetes Service(EKS):

Amazon EKS is Kubernetes management service. 

 Elastic Kubernetes Service(EKS) give fault tolerance(FT) means if something fail, Kubernetes master automatic launch Container.

 EKS give seamless facility.

 EKS also have multi master node setup.

- control plane:

 In Master node of Kubernetes there are differents program run (Kube-schedular, KubeAPI, etcd) which control the kubernetes cluster nodes is termed as 'Control plane'.

 - Master Node:

 Amazon EKS the master node is fully managed by aws cloud .

-  worker node:

 The worker node is not fully managed by aws.

- Note:

we can create EKS cluster :-
 1. webUI
 2. terraForm
 3. eksctl



# SetUp

we use "eksctl" to create eks cluster we need following things:
 1. AWS cli (on local laptop for aws Authentication)
 2. IAM user (Create IAM user to access AWS EKS)
 3. eksctl tool on local machine(Create Eks cluster).
 4. kubectl tool on local machine(Do work inside cluster).
 
    
 
 
