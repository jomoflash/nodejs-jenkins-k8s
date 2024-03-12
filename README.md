
## Dockerize node.js app 
docker build . -t express-demo    

docker run -it -p 127.0.0.1:3002:3000 express-demo  

docker tag express-demo jomoflash/express-demo:latest  
docker push jomoflash/express-demo:latest  

## Launch k8s (minikube)
minikube start --driver=docker --container-runtime=docker --network-plugin=cni --cni=calico   
k create deployment node-app --image jomoflash/express-demo:latest --replicas 2  
k expose deployment node-app --port 5000 --target-port 3000 --type NodePort  


## Extra
minikube start --driver=docker --container-runtime=docker --network-plugin=cni --cni=calico  
minikube node add --worker  
alias k=kubectl  
k get nodes -owide  

k get po --all-namespaces   
k get po --all-namespaces -owide  

k get services  

k create namespace prod  
k create namespace dev  
k get namespace  
k config get-contexts  

k run node-app --image jomoflash/node-app  
k get po  
k delete po node-app  

k run node-app --image jomoflash/node-app --dry-run=client -oyaml  
k apply -f app.yml  

minikube delete --all

