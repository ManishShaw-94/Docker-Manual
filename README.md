# DOCKER MANUAL

> A **Docker** is an open source software used for containerised application (building, shipping, and running applications in isolated environments). 

> An **Image** is a lightweight, read-only template that contains everything needed to run an application. 

> A **Container** is a running instance of an image, packaged with its dependencies and isolated from the host system.

## Docker vs Virtual Machines

### Virtual Machines (VMs)

<img width="544" height="398" alt="image" src="https://github.com/user-attachments/assets/7e75f0ee-11c9-41a1-a676-78dd5e01c187" />

### Key Points: 
  1. Each VM includes a **full Guest OS**.
  2. The **Hypervisor virtualizes hardware** for each VM.
  3. Higher resource usage (memory, CPU, storage).
  4. Networking and storage are managed **per VM via the hypervisor**.

### Docker (Containers)

<img width="408" height="299" alt="image" src="https://github.com/user-attachments/assets/f1c139e2-6d41-434c-b7d0-c121f4d8d6b0" />

### Key Points:
  1. Containers **share the host OS kernel** (no separate OS per container).
  2. **Docker Engine** manages containers.
  3. Much **lighter and faster** than VMs.
  4. Networking and storage are **handled by Docker**, but shared more efficiently.
  5. A **Docker Image** is the blueprint used to create containers (not a runtime layer like an OS).


---------------------------

**Pre-requisite (Ubuntu): Install Docker:** sudo apt install docker.io

**Post-Installation Steps (Ubuntu)**

--------------------------

**1. Verify Docker Installation:**
sudo docker --version

**2. Start Docker Service:**
sudo systemctl start docker

**3. Enable Docker to Start on Boot:**
sudo systemctl enable docker

**4. Run Docker Without sudo (Optional but Recommended):**
sudo usermod -aG docker $USER

**5. Apply group changes:**
newgrp docker

**6. Test Docker Installation:**
docker run hello-world

---------------------------

### Basic Docker Commands

--------------------------

**1. docker pull {image_name}:**  Fetch an image from a registry (e.g., Docker Hub)

**2. docker iamages:**  List all locally available Docker images
   
**3. docker run {image_name}:**  Start a new container using the specified image

    a. docker run -it {image_name} : To keep the container running (Start a container in interactive mode and connect it to your terminal)

**4. docker ps:**  List all currently running containers

    a. docker ps -a : List all containers (including running, stopped, and exited ones)

