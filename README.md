# DOCKER MANUAL

> A **Docker** is an open source software used for containerised application (building, shipping, and running applications in isolated environments). 

> An **Image** is a lightweight, read-only template that contains everything needed to run an application. 

> A **Container** is a running instance of an image, packaged with its dependencies and isolated from the host system.

> A **Dockerfile** is a file that contains instructions to build a Docker image.

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

**2. docker images:**  List all locally available Docker images
   
**3. docker run {image_name}:**  Start a new container using the specified image

    a. docker run -it {image_name} : To keep the container running (Start a container in interactive mode and connect it to your terminal)

**4. docker ps:**  List all currently running containers

    a. docker ps -a : List all containers (including running, stopped, and exited ones)

    b. docker ps -aq : List all containers id only

**5. docker stop {container_id}:**  Stop a running container (This can be done from the host terminal without entering the container).

**6. docker start {container_id}:**  Restart a stopped container

**7. docker rm {container_id} :** Remove a stopped container

    a. docker rm $(docker ps -aq) : Remove all containers (running + stopped)

**8. docker rmi {image_id} :** Remove a Docker image

    a. docker image ls dangling=true : List all dangling images (unused images with no tag)

    b. docker image prune: Remove all dangling images

    c. docker rmi $(docker images -q) -f : This command removes ALL images, including those used by containers. Warning! - Containers depending on these images may break.

**9. docker run -it -p {external_port}:{internal_port} {image_name} :**  Port mapping (maps a port from the local machine to a port inside the Docker container)

**10. docker build -t {image_name}:{tag_name} . :** Create a Docker image using the Dockerfile in the current directory and assign it a tag

    a. docker build -t {image_name}:{tag_name} -f {dockerfile_name} . : Build a Docker image using a specific Dockerfile instead of the default `Dockerfile`
  
```bash
#Step 1: Use a base image for your docker file
#FROM python
FROM python:3.8-alpine

# Option 1: Simple execution
#Step 2: Add/Copy file into container which you want to execute followed by destination
#ADD app.py .
#COPY app.py .
#ADD app.py /tree/app1.py
COPY app.py /tree/app1.py

#Step 3: Run the application
#CMD ["python", "app.py"]
CMD ["python", "/tree/app1.py"]

# Option 2: Using WORKDIR + ENTRYPOINT
FROM python:3.8-alpine

#Set working directory
WORKDIR /tree

# IF you need to add multiple file in the directory
#ADD app.py .
#ADD names.txt .
#ADD . .
COPY . .

#CMD ["python", "app.py"]
ENTRYPOINT [ "python" ]
CMD [ "app.py" ]
```

**11. docker compose up:** Build (if needed) and start all services defined in a docker-compose.yml file. Docker compose manages multi-container applications (build, run, and stop services) defined in a docker-compose.yml file

```bash
version: '3.6'

services:

  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile-backend
    hostname: backend-host
    volumes: 
      - ./backend:/app1
    ports:
      - "8000:8000"
    networks:
      - ms-network

  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile-frontend
    hostname: frontend-host
    volumes:
      - ./frontend:/app2
    environment:
      - BACKEND_URL=http://backend-host:8000/api
    ports:
      - "3000:3000"
    links:
      - backend
    depends_on:
      - backend
    networks:
      - ms-network

networks:
  ms-network: {}
```

**12. docker tag {source_image} {target_image} :**  Assign a new name and tag to an existing image (useful before pushing to a registry)

**13. docker push {image_name}:{tagname} :**  Push a Docker image to a container registry (e.g., Docker Hub)

**14. docker login :**  Log in to a Docker registry using your credentials

**15. docker logs {container_id}:**  View the logs of a container

**16. docker exec -it {container_id} {command_name}:**  Run a command inside an already running container from the host system (local terminal)

**17. docker inspect {container_id}:** Display detailed information about a container. Note: This shows container-level details (configuration, state, networking, etc.), not full application-level logs or internal behavior
