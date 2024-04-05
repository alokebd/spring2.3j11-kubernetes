# Springboot-Microservice-Kubernetes
Springboot-Microservice in Kubernetes Orchestration 
1. podname-{replica-index}.{serviceName}.default.svc.cluster.local 


# Docker Command
a) By maven:
mvn clean package dockerfile:push


b) By manual:
docker build --pull --rm -f "Dockerfile" -t cloud-config-server:latest "."

docker build --pull --rm -f "Dockerfile" -t cloud-gateway:latest "."

docker build --pull --rm -f "Dockerfile" -t department-service:latest "."

docker build --pull --rm -f "Dockerfile" -t hystrix-dashboard:latest "."

docker build --pull --rm -f "Dockerfile" -t service-registry:latest "."

docker build --pull --rm -f "Dockerfile" -t user-service:latest "."

# Kubernetes (google -sclability and high abiliity)
************INFO*************
Cluster
-Master Node
--kubelet (runs on master node)
--api server
--controller
--exed server
--scheduler
-Virtual Node (combine Master and worker)
-Worker Node
--containers (app will deploy )
---pod (smallest unit of k8s, IP, App)
-----Ing(res) - 
-----Config map 
----- vol (db but it is better to externalize)
----- secret (password)
--kubelet agent
--Service (attach multiple pods - Internal & External IP)
--deployment (app. scalibility - loadbalancing with workers)
************
# MiniKUBE - for deployment in dev (single node) and MiniCLI
1. In windows Powershell - run chocolatey.
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

2. Install MiniCli (if you have already Docker latest, you don't need it).
type command: choco install kubernetes-cli

3. Install MiniCube (by using choco 
type command: choco install minikube
4. Check your system Hyper-v enalble or not
type command: systeminf (last line shows it is dected)

5. Enable Hyper-v in windows
Open Windows Sart menu (command box) and type features
Select Turn Windows features on of off

6. start MiniKube
type command minikube start --driver=hyperv or just minikube start
minikube start --driver=docker

7. important commands
minikube dashboard
minikube start (make sure local docker is running)
minikube service list

kubectl get node
kubectl get all
kubectl cluster-info
kubectl describe

#Kubernetes config deployment (windows powershell for windows OS)
a. Go to k8s directory 
b. type kubectl apply -f ./

# DEV environment port forwarding 
 kube-forwader (https://github.com/pixel-point/kube-forwarder) in dev environment for port forwarding
https://github.com/pixel-point/kube-forwarder?tab=readme-ov-file (for windows)

--> Add your cluster info
1) cluster name: minikube -> namespance: default
2) Kind: Service -> eureka-lb
3) Ports Forwarding
   a) Local Port: 8761 --> Resource Port:80
4) Click Add and Start 

5) Test on browser: localhost:8761


#Test Application (in postman)
1. POST: http://localhost:9191/deparments/
{
  "departmentId": 1,
  "departmentName": "IT",
  "departmentAddress": "Toronto",
  "departmentCode": "25",

}
2. GET: http://localhost:9191/deparments/1

3. POST: http://localhost:9191/users
{
  "userId": 1,
  "firstName": "A",
   "lastNamme: "Das",
   "email": "alokebd@gmail.com",
   "departmentId": 1
}



