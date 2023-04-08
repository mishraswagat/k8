chmod +x ec2-instance-selector

How to get list of instances with the list of selective CPU and Memory: 

always use --burst-support=false

./ec2-instance-selector --vcpus=4 --memory=16 --cpu-architecture=x86_64 --gpus=0 --burst-support=false
