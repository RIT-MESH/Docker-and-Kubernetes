**Docker & Kubernetes Together**

### **Table of Contents**
1. **Running Docker Containers on Kubernetes**
2. **Deploying a Dockerized App to Kubernetes**
3. **Docker Compose vs Kubernetes Manifests**
4. **Converting Docker Compose to Kubernetes (kompose)**
5. **Kubernetes Deployment Strategies (Rolling Updates, Canary, Blue-Green)**
6. **Kubernetes Auto-scaling (HPA & Cluster Autoscaler)**
7. **Service Mesh & Microservices with Kubernetes (Istio, Linkerd)**
8. **CI/CD with Docker & Kubernetes (Jenkins, ArgoCD, GitOps)**
9. **Disaster Recovery & Backup Strategies for Kubernetes**
10. **Cloud-Native Development with Docker & Kubernetes (AWS EKS, Azure AKS, GCP GKE)**

---

### **1. Running Docker Containers on Kubernetes**
**Theory:**
- Kubernetes uses container runtimes like **Docker** to run applications in a distributed environment.
- A **Pod** in Kubernetes is the smallest deployable unit, which runs one or more Docker containers.
- Kubernetes replaces Docker Compose in production environments by providing **orchestration, scaling, and automation**.

**UI Steps (Minikube Example):**
1. Start Minikube:
   ```sh
   minikube start
   ```
2. Deploy a simple Docker container as a pod:
   ```sh
   kubectl run myapp --image=nginx --port=80
   ```
3. Expose the pod to external traffic:
   ```sh
   kubectl expose pod myapp --type=NodePort --port=80
   ```
4. Retrieve the service URL:
   ```sh
   minikube service myapp --url
   ```
5. Open the displayed URL in a browser to access the running container.

---

### **2. Deploying a Dockerized App to Kubernetes**
**Theory:**
- A **Dockerized application** is an app packaged with all its dependencies in a container.
- Kubernetes allows us to **deploy, scale, and manage** these applications using **Deployments, Services, and ConfigMaps**.

**UI Steps:**
1. Build a Docker image of the application:
   ```sh
   docker build -t myapp:v1 .
   ```
2. Push the image to a container registry (Docker Hub, AWS ECR, etc.):
   ```sh
   docker tag myapp:v1 mydockerhubusername/myapp:v1
   docker push mydockerhubusername/myapp:v1
   ```
3. Create a Kubernetes deployment:
   ```sh
   kubectl create deployment myapp --image=mydockerhubusername/myapp:v1
   ```
4. Expose the deployment as a service:
   ```sh
   kubectl expose deployment myapp --type=LoadBalancer --port=80
   ```
5. Get the external IP of the service:
   ```sh
   kubectl get services
   ```

---

### **3. Docker Compose vs Kubernetes Manifests**
**Theory:**
- **Docker Compose** is used to define and run **multi-container** Docker applications.
- **Kubernetes Manifests** define Pods, Deployments, Services, and other Kubernetes resources in **YAML format**.

**Example of Docker Compose (`docker-compose.yml`):**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

**Equivalent Kubernetes Manifest (`deployment.yaml`):**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```

**CLI Steps to Deploy Kubernetes Manifest:**
```sh
kubectl apply -f deployment.yaml
kubectl get deployments
```

---

### **4. Converting Docker Compose to Kubernetes (Kompose)**
**Theory:**
- **Kompose** is a tool that converts Docker Compose files into Kubernetes manifests.

**CLI Steps:**
1. Install Kompose:
   ```sh
   curl -L https://github.com/kubernetes/kompose/releases/latest/download/kompose-linux-amd64 -o /usr/local/bin/kompose
   chmod +x /usr/local/bin/kompose
   ```
2. Convert a Docker Compose file:
   ```sh
   kompose convert -f docker-compose.yml
   ```
3. Deploy the generated Kubernetes manifests:
   ```sh
   kubectl apply -f .
   ```

---

### **5. Kubernetes Deployment Strategies (Rolling Updates, Canary, Blue-Green)**
**Theory:**
- **Rolling Updates**: Gradually updates pods to the new version.
- **Canary Deployments**: Releases a small percentage of traffic to new deployments before full rollout.
- **Blue-Green Deployments**: Runs both old and new versions simultaneously and switches traffic.

**CLI Steps (Rolling Update Example):**
```sh
kubectl set image deployment myapp myapp-container=mynewimage:v2
kubectl rollout status deployment myapp
```

---

### **6. Kubernetes Auto-scaling (HPA & Cluster Autoscaler)**
**CLI Steps:**
```sh
kubectl autoscale deployment myapp --cpu-percent=50 --min=2 --max=10
kubectl get hpa
```

---

### **7. Service Mesh & Microservices with Kubernetes (Istio, Linkerd)**
**CLI Steps:**
```sh
kubectl apply -f istio.yaml
kubectl get pods -n istio-system
```

---

### **8. CI/CD with Docker & Kubernetes (Jenkins, ArgoCD, GitOps)**
**CLI Steps (ArgoCD Deployment Example):**
```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

---

### **9. Disaster Recovery & Backup Strategies for Kubernetes**
**CLI Steps:**
```sh
velero install --provider aws --bucket my-bucket --secret-file ./credentials-velero
velero backup create my-cluster-backup --include-namespaces=default
```

---

### **10. Cloud-Native Development with Docker & Kubernetes (AWS EKS, Azure AKS, GCP GKE)**
**CLI Steps (Creating a Cluster on AWS EKS):**
```sh
eksctl create cluster --name my-cluster --region us-east-1 --nodegroup-name my-nodes
```

---

### **Next Steps:**
- Learn advanced Kubernetes tools like **Knative for Serverless**.
- Implement **observability with OpenTelemetry**.
- Explore **multi-cloud Kubernetes deployments** with Terraform and Helm.

