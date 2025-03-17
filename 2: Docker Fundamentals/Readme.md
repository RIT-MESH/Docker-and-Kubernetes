**Docker Fundamentals**

### **Table of Contents**
1. **Installing Docker on Windows/Mac/Linux**
2. **Docker Architecture (Docker Engine, Daemon, CLI)**
3. **Docker Images vs Containers**
4. **Working with Docker Hub & Private Registries**
5. **Creating & Running Containers (`docker run`)**
6. **Managing Containers (`docker ps`, `docker stop`, `docker rm`)**
7. **Building Docker Images (`Dockerfile` Basics)**
8. **Tagging & Pushing Images (`docker tag`, `docker push`)**
9. **Networking in Docker (`bridge`, `host`, `overlay`)**
10. **Docker Volumes & Persistent Storage**
11. **Docker Compose (Managing Multi-Container Applications)**
12. **Docker Security Best Practices**
13. **Docker Swarm (Basics of Container Orchestration)**

---

### **1. Installing Docker on Windows/Mac/Linux**
**Theory:** Docker can be installed on Windows, macOS, and Linux. It provides a containerized environment to run applications efficiently. Windows and Mac users typically install **Docker Desktop**, which includes an easy-to-use UI and built-in Kubernetes support, while Linux users install **Docker Engine** directly for lightweight and efficient container execution.

**UI Steps (Windows/Mac):**
1. Download Docker Desktop from [Docker’s official site](https://www.docker.com/).
2. Install Docker following the setup wizard and restart the system.
3. Open Docker Desktop and verify installation using the dashboard.

**CLI Steps (Linux - Ubuntu Example):**
```sh
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
```

---

### **2. Docker Architecture (Docker Engine, Daemon, CLI)**
**Theory:** Docker consists of multiple components working together:
- **Docker Engine:** The core of Docker that enables containerization.
- **Docker Daemon:** A background service that manages containers and images.
- **Docker CLI:** A command-line tool to interact with Docker Daemon.
- **Docker API:** Provides programmatic access to Docker features.
- **Container Runtime:** The low-level component responsible for running containers.

Docker follows a **client-server architecture**, where the **Docker CLI** communicates with the **Docker Daemon** to execute container-related tasks.

---

### **3. Docker Images vs Containers**
**Theory:**
- **Docker Image:** A lightweight, stand-alone, and executable software package that includes everything needed to run a piece of software.
- **Docker Container:** A running instance of a Docker Image, which is isolated from the host system.
- **Difference:** Images are immutable, while containers are instances of images that can be modified during runtime.

**Example CLI Commands:**
```sh
docker pull nginx   # Download Nginx image
docker run nginx    # Run a container from the image
docker ps          # List running containers
```

---

### **4. Working with Docker Hub & Private Registries**
**Theory:** Docker Hub is the default public repository for Docker images. Organizations can also use private registries such as **Amazon ECR**, **Google Container Registry**, and **Azure Container Registry** for secure image storage and management.

**UI Steps:**
1. Navigate to [Docker Hub](https://hub.docker.com/).
2. Sign in and create a repository.
3. Use `docker push` to upload images to the repository.

**CLI Steps:**
```sh
docker login        # Authenticate with Docker Hub
docker pull ubuntu  # Pull an image
docker tag ubuntu myrepo/ubuntu:v1  # Tag the image
docker push myrepo/ubuntu:v1  # Push to registry
```

---

### **5. Creating & Running Containers (`docker run`)**
**Theory:** The `docker run` command is used to start a new container from an existing image. Options like `-d` (detached mode) and `-p` (port mapping) help manage container execution.

**UI Steps:**
1. Open Docker Desktop.
2. Navigate to "Containers" and click "Run a new container".
3. Choose an image, configure settings, and start the container.

**CLI Examples:**
```sh
docker run -d -p 80:80 nginx  # Run Nginx in detached mode on port 80
docker run --name mycontainer ubuntu sleep 100  # Run a named container
```

---

### **6. Managing Containers (`docker ps`, `docker stop`, `docker rm`)**
**Theory:** Docker provides commands to list, stop, restart, and remove containers.

**UI Steps:**
1. Open Docker Desktop and go to "Containers".
2. Select a running container and click "Stop".
3. Click "Remove" to delete the container.

**CLI Steps:**
```sh
docker ps         # List running containers
docker stop mycontainer  # Stop a container
docker rm mycontainer  # Remove a stopped container
```

---

### **7. Building Docker Images (`Dockerfile` Basics)**
**Theory:** Docker images are created using a **Dockerfile**, which is a script containing a series of commands.

**UI Steps:**
1. Open Docker Desktop and navigate to "Images".
2. Click "Build new image" and select a directory with a `Dockerfile`.
3. Build and tag the image.

**Example `Dockerfile`:**
```dockerfile
FROM ubuntu:latest
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

**CLI Steps:**
```sh
docker build -t myimage .  # Build an image from Dockerfile
docker images  # List images
```

---

### **12. Docker Security Best Practices**
**Theory:** Security is a critical aspect of containerization. Key security practices include:
- **Running Containers as Non-Root Users**: Prevents privilege escalation.
- **Using Read-Only Filesystems**: Reduces attack surface.
- **Scanning Images for Vulnerabilities**: Identifies outdated dependencies.
- **Limiting Capabilities**: Drops unnecessary privileges.

**UI Steps:**
1. Open Docker Desktop.
2. Navigate to "Settings" → "Security".
3. Enable security features like rootless mode and read-only filesystems.

**Example CLI Commands:**
```sh
docker scan myimage  # Scan image for security issues
docker run --read-only nginx  # Run container in read-only mode
```

---

### **Next Steps:**
- Learn **Kubernetes** for advanced orchestration.
- Implement **CI/CD with Docker**.
- Deploy applications in **cloud environments** (AWS, Azure, GCP).

