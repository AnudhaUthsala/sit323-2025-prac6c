
## **Project Overview**  
This repository contains the implementation of **Task 6.1C** which demonstrates:  
- ✅ Deployment of a containerized Node.js application to Kubernetes  
- ✅ Configuration of Kubernetes manifests (Deployment + Service)  
- ✅ Local cluster management using Minikube  
- ✅ Application access via port-forwarding and NodePort  

## **Prerequisites**  
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) v1.25+  
- [kubectl](https://kubernetes.io/docs/tasks/tools/) v1.24+  
- [Docker](https://docs.docker.com/get-docker/) v20.10+  
- Node.js v16+  

## **Quick Start**  
### **1. Start Minikube Cluster**  
```bash  
minikube start --memory=4096 --cpus=2  
```

### **2. Build & Deploy**  
```bash  
# Build Docker image  
eval $(minikube docker-env)  
docker build -t calculator-app .  

# Apply Kubernetes manifests  
kubectl apply -f manifests/deployment.yaml  
kubectl apply -f manifests/service.yaml  
```

### **3. Access Application**  
```bash  
# Method 1: Port Forwarding  
kubectl port-forward svc/calculator-service 8080:80  

# Method 2: Minikube Service URL  
minikube service calculator-service --url  
```

## **Repository Structure**  
```  
.  
# Kubernetes configuration  
├── deployment.yaml      # Pod deployment specs  
└── service.yaml         # Service exposure    
├── Dockerfile           # Container build instructions  
└── README.md            # This documentation  
```  

## **Key Features**  
- **Multi-replica Deployment**: 2 pod instances for fault tolerance  
- **NodePort Service**: External access to application  
- **Local Development**: Minikube-optimized configuration  

## **Troubleshooting**  
| Issue | Solution |  
|-------|----------|  
| `ImagePullBackOff` | Run `eval $(minikube docker-env)` before building |  
| Pods stuck in `Pending` | Increase Minikube resources: `minikube start --memory=4096 --cpus=4` |  
| Port conflicts | Change `targetPort` in service.yaml |  
.  

