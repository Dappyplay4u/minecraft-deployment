# EKS-Blueprint-for-minecraft
docker build -t minecraft-server .


# RUN Docker Container
docker run -d -p 25565:25565 --name minecraft-container minecraft-server



# push to Docker Hub.
docker push dappyplay4u/minecraft:minecraft





Amazon EKS cluster (Elastic Kubernetes Service) and interacting with Kubernetes once the configuration is set. 

#####updates the kubeconfig file in your local environment to enable communication with  eks-cluster located in the us-east-1 region.
aws eks --region us-east-1 update-kubeconfig --name eks-cluster


#### kubectl command retrieves information about the Kubernetes services It lists the services and their respective details.
kubectl get svc

This kubectl command lists all namespaces (logical clusters) within the Kubernetes cluster
kubectl get ns


This kubectl command displays the nodes (individual compute instances) that form the Kubernetes cluster.
kubectl get nodes

#####create the refrence file for secret so to be able to refrence it
copy secret.yml to the OS
kubectl apply -f secret.yml

kubectl get secret

#######create deployment and deploy it 
copy mongodb-deployment.yml to the OS
kubectl apply -f mongodb-deployment.yml

#######create service and deploy it 
copy service.yml to the OS
kubectl apply -f service.yml


######to get PODS
kubectl get all
kubectl get pod
kubectl get all | grep mongodb

#####create the refrence file for secret so to be able to refrence it
copy mongoepressconfig.yml to the OS
kubectl apply -f mongoepressconfig.yml

##########create mogoexpress deployment use the mongoepressconfig to link
copy mongoexpress-deployment.yml to the OS
kubectl apply -f mongoexpress-deployment.yml


#######create service loadbalancer  using node port deploy it 
copy mongo-expressservice.yml to the OS
kubectl apply -f mongo-expressservice.yml


ingress >> mongo-express External service >> mongoexpress POD >> Mongodb internal service >> Mongodb POD

####to access application
http:<Loadbalancer_dns>/30000
