1 - How to create a cluster ? 

we can create it using yml file : eksctl create cluster --config-file=cluster.yml ( it will create ekscluster and nodes of my choice,spot or gpu of my choice)

We can also create it without a yml file : eksctl create cluster (it will create ekscluster and 2 node where the k8s default pod will run)

2 - How can i get instance type of my choice ?

Get the github link of instance selector - https://github.com/aws/amazon-ec2-instance-selector

Download it by curl :
curl -Lo ec2-instance-selector https://github.com/aws/amazon-ec2-instance-selector/releases/download/v2.4.1/ec2-instance-selector-`uname | tr '[:upper:]' '[:lower:]'`-amd64 && chmod +x ec2-instance-selector

Run it and get it the instance type - 
./ec2-instance-selector --vcpus=4 --memory=16 --cpu-architecture=x86_64 --gpus=0 --burst-support=false

3 - What is a node group ?

Any set of nodes in k8s called as nodegroup.
We can create it by eksctl create nodegroup (it will create the on-demand default nodes in the same cluster)
We can create it from cluster.yml file by adding a new nodegroup
(min (no of instance),max,instance type, gpu or spot can be configured here)

4 - How to add a new nodegroup ?
	how to create a cluster --> eksctl create cluster --config-file=cluster.yml (it will create the defined nodegroup in the yml file)
	how to add a new node group --> Add below lines in the existing yml file and run the last command )
  - name: gpu
    instanceTypes: [mention gpu instance type (refer to question no 2)]
    minSize: 1
    desiredCapacity: 1
    maxSize: 5
    volumeSize: 30
    ssh:
      allow: true                                       # will use ~/.ssh/id_rsa.pub as the default ssh key
	
eksctl create nodegroup --config-file=cluster.yml

Your GPU instance nodegroup successfully added to existing cluster
The minSize and maxSize is desiced by default threshold of k8s

5- How to delete an existing nodegroup?




######################################################################################################
Steps to create the cluster:

run this to create keygen so that we can login to the kubernetes node (password less)
ssh-keygen 

run this to create cluster
eksctl create cluster --config-file=cluster.yml



