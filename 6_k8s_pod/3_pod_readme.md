
Any changes in the yml or new yml file will reflect after applying the below command
kubectl apply -f 2_httpd.yml 

How to get inside a pod
kubectl exec -ti $POD_NAME -- bash

How to watch pod live ?
kubectl get pod -w

how to get pod logs ?
kubectl get logs $POD_NAME

How to get details of any service in k8s ?
kubectl describe service_type service_name
eg - kubectl describe svc httpd-service-nautilus
     Kubectl describe pod jenkins

Describe in yml file details ?
apiVersion: v1
kind: Service #There are minimum 2 kinds required Service & Deployment/pod
metadata:
  name: httpd-service-nautilus
spec:
  type: NodePort #There are several types of services NodePort is used to map ports
  selector: #it always looks for labels (label is available in deployement)
    app: httpd_app_nautilus
  ports:
    - port: 80 #This is nodeport internal port
      targetPort: 80 #This is pod port
      nodePort: 30004 #Access this in browser (make sure your inbound port is open of the instance)
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deployment-nautilus
  labels: #without this service will not find this deployment even if both are in the same file
    app: httpd_app_nautilus
spec:
  replicas: 4 #This many pods will run simultaneously 
  selector:
    matchLabels:
      app: httpd_app_nautilus
  template:
    metadata:
      labels:
        app: httpd_app_nautilus
    spec:
      containers: #This is the container specification
        - name: httpd-container-nautilus
          image: httpd:latest #This is the image name, you can change the name of image to jenkins/jenkins:latest to run jenkins (pulled from dockerhub)
          ports:
            - containerPort: 80

How to terminate all kubernetes service in default namespace?
kubectl delete all --all -n default

How to terminate cluster in k8s ?

