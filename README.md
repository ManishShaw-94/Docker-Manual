# DOCKER MANUAL

> A **Docker** is an open source software used for containerised application (building, shipping, and running applications in isolated environments). 

> An **Image** is a lightweight, read-only template that contains everything needed to run an application. 

> A **Container** is a running instance of an image, packaged with its dependencies and isolated from the host system.

## Docker vs Virtual Machines

**Virtual Machines (VMs)**

### Key Points: 
  1. Each VM includes a **full Guest OS**.
  2. The **Hypervisor virtualizes hardware** for each VM.
  3. Higher resource usage (memory, CPU, storage).
  4. Networking and storage are managed **per VM via the hypervisor**.

**Docker (Containers)**

### Key Points:
  1. Containers **share the host OS kernel** (no separate OS per container).
  2. **Docker Engine** manages containers.
  3. Much **lighter and faster** than VMs.
  4. Networking and storage are **handled by Docker**, but shared more efficiently.
  5. A **Docker Image** is the blueprint used to create containers (not a runtime layer like an OS).

---------------------------

**Basic Docker Commands**

--------------------------

**1. docker pull {image_name}:**  Fetch an image from a registry (e.g., Docker Hub)
   
**2. docker run {image_name}:**  Start a new container using the specified image
