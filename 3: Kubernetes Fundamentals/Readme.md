**Kubernetes Fundamentals**

### **Table of Contents**
1. **Installing Kubernetes (Minikube, K3s, Kind, Cloud-based K8s)**
2. **Kubernetes Architecture (Nodes, Pods, Services, API Server)**
3. **Understanding Kubernetes Objects (Pods, Deployments, Services)**
4. **Creating and Managing Pods (`kubectl run`, `kubectl get pods`)**
5. **ReplicaSets & Deployments (Scaling Applications)**
6. **Kubernetes Networking Model & Service Types**
7. **ConfigMaps & Secrets (Managing Configurations Securely)**
8. **Persistent Volumes & Storage Classes**
9. **Kubernetes Ingress & Load Balancing**
10. **Helm Charts (Managing Kubernetes Applications)**
11. **Monitoring & Logging in Kubernetes (Prometheus, Grafana, ELK Stack)**
12. **Kubernetes RBAC & Security Best Practices**
13. **Kubernetes Operators & Custom Resource Definitions (CRDs)**

---

### **1. Installing Kubernetes (Minikube, K3s, Kind, Cloud-based K8s)**
**Theory:**
Kubernetes can be installed in multiple ways depending on your use case:
- **Minikube**: Best for local development and testing. Runs a single-node Kubernetes cluster on your local machine.
- **K3s**: A lightweight Kubernetes distribution designed for IoT and edge computing.
- **Kind (Kubernetes in Docker)**: Runs Kubernetes clusters using Docker containers, useful for testing CI/CD pipelines.
- **Cloud-based Kubernetes**: Managed Kubernetes services such as **AWS Elastic Kubernetes Service (EKS)**, **Azure Kubernetes Service (AKS)**, and **Google Kubernetes Engine (GKE)** simplify cluster management.

**UI Steps (Minikube Example on Windows/Mac/Linux):**
1. Download Minikube from [Minikube’s official site](https://minikube.sigs.k8s.io/docs/start/).
2. Install a hypervisor (VirtualBox, Hyper-V, or Docker Desktop) if not already installed.
3. Open a terminal and start Minikube:
   ```sh
   minikube start --driver=docker
   ```
4. Verify the installation:
   ```sh
   kubectl get nodes
   ```

**CLI Steps:**
```sh
# Install Minikube (Linux Example)
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start Minikube
minikube start

# Check status
kubectl cluster-info
kubectl get nodes
```

---

### **2. Kubernetes Architecture (Nodes, Pods, Services, API Server)**
**Theory:**
Kubernetes follows a **master-worker architecture**, consisting of:
- **Control Plane (Master Node)**:
  - **API Server**: The entry point for all Kubernetes commands.
  - **Controller Manager**: Maintains cluster state and handles node failures.
  - **Scheduler**: Assigns workloads to worker nodes.
  - **etcd**: Stores all cluster configuration data.
- **Worker Nodes**:
  - **Kubelet**: Manages the node and communicates with the API server.
  - **Container Runtime (Docker, containerd, CRI-O)**: Runs containers.
  - **Kube Proxy**: Manages networking and load balancing.

**CLI Steps:**
```sh
kubectl cluster-info      # View cluster details
kubectl get nodes         # List all nodes
kubectl describe node <node-name>  # Get details of a node
```

---

### **3. Understanding Kubernetes Objects (Pods, Deployments, Services)**
**Theory:**
- **Pods**: The smallest deployable unit in Kubernetes, representing one or more containers.
- **Deployments**: Ensure that a specific number of identical Pods are running at all times.
- **Services**: Expose Pods to the network and enable load balancing.

**UI Steps:**
1. Open Kubernetes Dashboard.
2. Navigate to **Workloads** → **Pods**.
3. Navigate to **Workloads** → **Deployments**.
4. Navigate to **Networking** → **Services**.

**CLI Steps:**
```sh
kubectl get pods       # List all running pods
kubectl get deployments # List all deployments
kubectl get services   # List all services
```

---

### **4. Creating and Managing Pods (`kubectl run`, `kubectl get pods`)**
**CLI Steps:**
```sh
# Create a Pod with an Nginx container
kubectl run nginx-pod --image=nginx --restart=Never

# List all running pods
kubectl get pods

# Describe the Pod to see more details
kubectl describe pod nginx-pod
```

---

### **5. ReplicaSets & Deployments (Scaling Applications)**
**CLI Steps:**
```sh
# Create a deployment with 3 replicas
kubectl create deployment myapp --image=nginx --replicas=3

# Scale the deployment
kubectl scale deployment myapp --replicas=5

# Get deployment details
kubectl get deployments
```

---

### **6. Kubernetes Networking Model & Service Types**
**Theory:**
Kubernetes networking supports different service types:
- **ClusterIP** (default) - Internal communication within the cluster.
- **NodePort** - Exposes service on a static port.
- **LoadBalancer** - Uses cloud provider’s load balancer.

**CLI Steps:**
```sh
kubectl expose deployment myapp --type=LoadBalancer --port=80
kubectl get services
```

---

### **9. Kubernetes Ingress & Load Balancing**
**Theory:**
Ingress controllers manage external HTTP/S traffic and route it to services inside the cluster.

**CLI Steps:**
```sh
kubectl apply -f ingress.yaml
kubectl get ingress
```

---

### **12. Kubernetes RBAC & Security Best Practices**
**Theory:**
Role-Based Access Control (RBAC) ensures secure access control by granting permissions to users and services.

**CLI Steps:**
```sh
kubectl create role pod-reader --verb=get,list --resource=pods
kubectl create rolebinding pod-reader-binding --role=pod-reader --user=admin
```

---

### **13. Kubernetes Operators & Custom Resource Definitions (CRDs)**
**Theory:**
Operators automate complex Kubernetes tasks, while Custom Resource Definitions (CRDs) extend Kubernetes functionality beyond built-in objects.

**CLI Steps:**
```sh
kubectl apply -f myoperator.yaml
kubectl get crd
```

---

### **Next Steps:**
- Learn advanced Kubernetes concepts like **Service Mesh (Istio, Linkerd)**.
- Deploy containerized applications on **AWS EKS, Azure AKS, or Google GKE**.
- Explore **GitOps workflows with ArgoCD and Flux**.

