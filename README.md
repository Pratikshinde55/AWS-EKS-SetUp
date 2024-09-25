# Elastic Kubernetes Service(EKS):
kubernetes is Container cluster management tool.

**Amazon EKS is Kubernetes cluster management service.** 

**Elastic Kubernetes Service(EKS) give fault tolerance(FT) means if something fail, Kubernetes master automatic launch Container.**

**EKS give seamless facility.**

EKS also have multi master node setup.

#### Control plane:
*In Master node of Kubernetes there are differents program run (Kube-schedular, KubeAPI, etcd) which control the kubernetes cluster nodes is termed as 'Control plane'.*

#### Master Node:
*Amazon EKS the master node is fully managed by AWS Cloud.*

#### worker node:
*The Worker node is not fully managed by AWS.*

- Note:

We can create EKS cluster :-
 1. webUI
 2. terraForm
 3. eksctl

![Screenshot 2024-08-06 173007](https://github.com/user-attachments/assets/7bf66c1f-c926-4cdf-b680-2faf1e626732)

-  SetUp:

Use "eksctl" to create eks cluster we need following things:
 1. IAM user (Create IAM user to access AWS EKS)
 2. AWS cli (on local laptop for aws Authentication)
 3. eksctl tool on local machine(Create Eks cluster).
 4. kubectl tool on local machine(Do work inside cluster).
 5. eksctl create cluster (Create cluster from local laptop).
 6. AWS Console check(Cluster is created checking on aws console-->>EKS)
 
    
### Step-1: [Create IAM user on aws]
Go to aws console and create IAM user which is used for Authentication:

 ![Screenshot 2024-08-06 173532](https://github.com/user-attachments/assets/154dc5ed-359e-4cef-b7d1-60b22f2080f4)

Now **attach policy** and create new user:

![Screenshot 2024-08-06 173631](https://github.com/user-attachments/assets/2cffdb97-a6f4-4485-be21-9fedf99d9bd7)

Now click on created user:

![Screenshot 2024-08-06 173654](https://github.com/user-attachments/assets/013a3297-fbae-45b5-be09-87ef0e5f23c0)

Now click **"security credentials"** and creare access key:

![Screenshot 2024-08-06 173727](https://github.com/user-attachments/assets/5a5c7c92-c5f3-435e-b498-5774cf4e3cc9)

![Screenshot 2024-08-06 173751](https://github.com/user-attachments/assets/4d92bc58-e998-4961-8852-62413dc336bb)

Retrieve **access key**:(Copy key)

![Screenshot 2024-08-06 173818](https://github.com/user-attachments/assets/5a4925c5-abf9-4af8-86d5-6c2098ff0b21)


### Step-2: [AWS CLI on local laptpton/ Authentication]

Search on google -->> "AWS CLI install window" -->> download AWS CLI for window (64-bit)

Command for checking AWS CLI work on prompt/ GitBash:

    aws --version

Paste access key of IAM user:

    aws configure

![image](https://github.com/user-attachments/assets/5809837a-b043-4564-9521-06d81cbd5d90)

**This AWS CLI tool help us to connect with AWS and use AWS Services from laptop/Local machine.
  
### Step 3: [Download eksctl tool]

**eksctl is third party tool to manage EKS.**

Search on browser "eksctl" open link and right side of link give GitHub repo link click ,

[eksctl-download-link](https://github.com/eksctl-io/eksctl/releases/tag/v0.188.0)

![Screenshot 2024-08-06 175713](https://github.com/user-attachments/assets/ab03f6fb-8236-445c-89ae-dc47e9844472)

Now on GitHub there is option -->> "Release" click: (Download:- eksctl window amd64.zip)

![image](https://github.com/user-attachments/assets/d823fc7d-b54e-434f-82ae-f40199d2523c)

- Note:

  After Download eksctl tool we extract because we download zip file .

  After extract eksctl tool we need to add path of eksctl tool to system -->>"Edit environment variable"

 Go to "User variable for__"  --> click "path" -->> Click "Edit"  and here Add New path for extracted eksctl tool location:

 ![image](https://github.com/user-attachments/assets/c0d7a1ef-cf20-4343-9899-460ded63d20e)


Now on command prompt/ GitBash we can check by using command :

      eksctl
      eksctl version
  
![image](https://github.com/user-attachments/assets/ad8304c4-65ce-442f-87e6-923db56edd57)

- Note:

"eksctl" command for only create and delete cluster but not for doing cluster inside activities or for worker node.

"eksctl" tool helps to connect with master through "kubeAPI" but we Master node is fully managed by aws.


### Step-4: [Download Kubectl on loptop]

Search on browser 'kubectl install window' -->> 'Install kubectl binary with curl on Windows '  -->> copy command and paste on local system.

[Kubectl-download-link](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/ )
    
    curl.exe -LO "https://dl.k8s.io/release/v1.30.0/bin/windows/amd64/kubectl.exe"

We can check using command:
    
    kubectl version
      
![image](https://github.com/user-attachments/assets/3de88275-e6cd-4816-9890-45e82d4bccc6)


### Step-5: [Create EKS Cluster]

**For creating Cluster we use "eksctl" command and for doing anything inside cluster we use "kubectl" command.**

Create kubernetes cluster we use help command for showing option:

      eksctl create cluster --help

Create eks cluster using option command:

      eksctl create cluster  --name pscluster  --region ap-south-1  --version 1.30  --nodegroup-name psnodegp --instance-types t2.micro --nodes 3  --nodes-min 3  --nodes-max 6 --node-volume-size 8  --node-volume-type gp3  --ssh-access   --enable-ssm --instance-name psworkernode  --managed


![image](https://github.com/user-attachments/assets/f081c271-e3bc-467a-ab9b-e33d7d6247d6)


### Step-6: [Create pod using Docker image]

If we want to launch OS, Server, App then that entire Software we bundle in one box or software called as "Image"  and that image in Container world called as 
"Container Image".

**If we want to launch app/container/pod with help of image we use term as "deployment" in K8S world.**

Command for create deployment/container in AWS EKS:
     
    kubectl create deployment psapp --image=vimal13/apache-webserver-php

We can check pods using kubectl command:

    kubectl get pods 
     
![image](https://github.com/user-attachments/assets/b4f836b2-97ec-4346-9cfd-a5d3ee6e78fa)

We can check entire info of pods using command:

    kubectl get pods -o wide

We can also direct connect to POD (Container) from laptop:

    kubectl exec -it psapp bash

- Note:

  Master node keeps on monitoring "pod" because there is a program running in "worker node" who communicates with master that program is known as "kubelet", 
  This is also managed by EKS.

  If we delete pod or any fault occures and pod goes down then Master node automatically launch same pod at any node, at any node means master kube-schedular 
  program keep 
  on monitoring on worker node which is free, that node use for launch pod.

  ![image](https://github.com/user-attachments/assets/8e9ac95d-d0b9-4162-9870-fd033a096589)


### Step-7: [use Load balancer and access Webapp from outside world]

- Note:
Kubernetes have their own load balancer, but if we want to use other load balancer then plugin need for "vanilla kubernetes" but while using "amazon EKS" give 
precreated plugin for using aws services like Load balancer(ELB).

Command for get Load Balancer list:
    
    kubectl get svc

![image](https://github.com/user-attachments/assets/997d958f-fddb-4105-9888-8d3f8583e2a8)

Command for check create load balancer/expose deployment option:

    kubectl expose deployment --help

Command for Create LB:

    kubectl expose deployment psapp --name pslb --type=LoadBalancer --port 80

 ![image](https://github.com/user-attachments/assets/2d468bb1-0de9-4adb-9065-da9919386bfa)

After creating load balancer we get "EXTERNAL-IP" that we can use as link on browser:

    kubectl get svc

- Note:
     
Kubernetes give us fantastic option that "Scale", by using horizontal Scaling we can scale-out and scale-in our deployment:

    kubectl scale deployment psapp --replicas=4
       
![image](https://github.com/user-attachments/assets/90ef6965-6e34-4e5f-8317-1c80a0d325df)

we can also see on which "node" our pod from CLI:

       kubectl get pods -o wide

![image](https://github.com/user-attachments/assets/6169c8c3-390a-4df8-a463-b102976c0e69)
       
we can see our Elastic Load balancer "EXTERNAL-IP" to access our psapp(pod/container):

Paste "EXTERNAL-IP" that get from "kubectl get svc" command and we access our psapp through loadBalancer:

- Note:

From below screenshoot we can see that our load balancer work, every time we connect new pod: 

![image](https://github.com/user-attachments/assets/370e8407-98d7-416a-bfbb-90e83f172d95)

![image](https://github.com/user-attachments/assets/9620f945-6bad-4045-bb85-c3bdb8b75bee)

![image](https://github.com/user-attachments/assets/6cb0c55e-7844-4c54-acdc-ea125167ee14)

![image](https://github.com/user-attachments/assets/da55b55e-01f7-4e8c-a0d6-144a261540d6)




### Step-8: [AWS console check]

now check on aws console our cluster creates: aws Dashbord-->> EKS

![image](https://github.com/user-attachments/assets/49c48de1-8b2c-4904-a9c3-a1a01182196a)


EC2 worker node also created:

  - Note:

  Here we can see that our instances lanuch at different " availability zones" because we use "nodegroup" while creating Cluster, EKS is very intelligent, every node launch in differnt AZ 
  because i any AZ goes down then our other AZ our app work:

![image](https://github.com/user-attachments/assets/b75e062c-a2db-4789-8588-b5607a4c0665)


Here, for worker node our local laptop Public key is attached because we use  "--ssh-access" and i can access Cluster node instance from local machine and manage.

     ssh ec2-user@(Public_IP)

![Screenshot 2024-08-09 135718](https://github.com/user-attachments/assets/697b3fef-1ad3-462f-b2f4-361203db57b6)


![image](https://github.com/user-attachments/assets/d1de79b5-565b-45fd-82bd-ab4c26c3369e)


- Load Balancer created:


![image](https://github.com/user-attachments/assets/58e25c91-309f-4a82-84d1-5ed13acd3e0f)

- VPC also created by EKS automatic(VPC give IP range subnet for our node,pod):

  AWS has its own personal plugin called "VPC" that is used for K8S by EKS.

  every VPC has subnets and every subnet gives IP adress range.

![image](https://github.com/user-attachments/assets/98a080c8-4a88-4360-b1cc-a3c91ad0467a)

### Step-9: [Delete entire cluster in one command]
AWS EKS master node all monitoring activity ,If we want delete entire cluster then we use only one following command:
     
     eksctl delete cluster --name pscluster  --region ap-south-1

![image](https://github.com/user-attachments/assets/9bc33310-8975-4384-af36-758ca140b460)
