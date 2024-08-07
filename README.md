
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

![Screenshot 2024-08-06 173007](https://github.com/user-attachments/assets/7bf66c1f-c926-4cdf-b680-2faf1e626732)

-  SetUp:

we use "eksctl" to create eks cluster we need following things:
 1. AWS cli (on local laptop for aws Authentication)
 2. IAM user (Create IAM user to access AWS EKS)
 3. eksctl tool on local machine(Create Eks cluster).
 4. kubectl tool on local machine(Do work inside cluster).
 
    
# Step 1: (Create IAM user on aws)

 Go to aws console and create IAM user which is used for Authentication 

 ![Screenshot 2024-08-06 173532](https://github.com/user-attachments/assets/154dc5ed-359e-4cef-b7d1-60b22f2080f4)

Now attach policy and create new user:

![Screenshot 2024-08-06 173631](https://github.com/user-attachments/assets/2cffdb97-a6f4-4485-be21-9fedf99d9bd7)

Now click on created user 

![Screenshot 2024-08-06 173654](https://github.com/user-attachments/assets/013a3297-fbae-45b5-be09-87ef0e5f23c0)

Now click " security credentials" and creare access key

![Screenshot 2024-08-06 173727](https://github.com/user-attachments/assets/5a5c7c92-c5f3-435e-b498-5774cf4e3cc9)

![Screenshot 2024-08-06 173751](https://github.com/user-attachments/assets/4d92bc58-e998-4961-8852-62413dc336bb)

Retrieve access key:

![Screenshot 2024-08-06 173818](https://github.com/user-attachments/assets/5a4925c5-abf9-4af8-86d5-6c2098ff0b21)


# Step 2: (AWS CLI on local laptpton/ Authentication)

Search on google -->> "aws cli install window" -->> download AWS CLI for window (64-bit)

on command prompt/ GitBash

    #  aws --version

paste access key of IAM user:

    # aws configure

![image](https://github.com/user-attachments/assets/5809837a-b043-4564-9521-06d81cbd5d90)


# Step 3: (Download eksctl tool)

Search on browser "eksctl" open link and right side of link give GitHub repo link click ,

(link- https://github.com/eksctl-io/eksctl/releases/tag/v0.188.0)

![Screenshot 2024-08-06 175713](https://github.com/user-attachments/assets/ab03f6fb-8236-445c-89ae-dc47e9844472)

Now on GitHub there is option -->> "Release" click: (Download:- eksctl window amd64.zip)

![image](https://github.com/user-attachments/assets/d823fc7d-b54e-434f-82ae-f40199d2523c)

- Note:

  After Download eksctl tool we extract because we download zip file .

  After extract eksctl tool we need to add path of eksctl tool to system -->>"Edit environment variable"

 Go to "User variable for__"  --> click "path" -->> Click "Edit"  and here Add New path for extracted eksctl tool location:

 ![image](https://github.com/user-attachments/assets/c0d7a1ef-cf20-4343-9899-460ded63d20e)


Now on command prompt/ GitBash we can check by using command :

    # eksctl
    # eksctl version
  
![image](https://github.com/user-attachments/assets/ad8304c4-65ce-442f-87e6-923db56edd57)

- Note:

"eksctl" command for only create and delete cluster but not for doing cluster inside activities or for worker node.

# Step 4: (Download Kubectl on loptop)

Search on browser 'kubectl install window' -->> 'Install kubectl binary with curl on Windows '  -->> copy command and paste on local system .

(link-https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/ )


    #  curl.exe -LO "https://dl.k8s.io/release/v1.30.0/bin/windows/amd64/kubectl.exe"




# Step 5: (Create EKS Cluster)

For creating Cluster we use "eksctl" command and for doing anything inside cluster we use "kubectl" command.

Create kubernetes cluster we use help command for showing option:

    # eksctl create cluster --help


Now create cluster using option:

    # eksctl create cluster  --name pscluster  --region ap-south-1  --version 1.30  --nodegroup-name psnodegp  --nodes 3 
      --nodes-min 3  --nodes-max 6  --node-volume-size 8  --node-volume-type gp3  --ssh-access   --enable-ssm --instance-name psworkernode  --managed
