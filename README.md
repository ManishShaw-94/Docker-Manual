# DOCKER MANUAL

> A **Docker** is an open source software used for containerised application (building, shipping, and running applications in isolated environments). 

> An **Image** is a lightweight, read-only template that contains everything needed to run an application. 

> A **Container** is a running instance of an image, packaged with its dependencies and isolated from the host system.

## Docker vs Virtual Machines

**Virtual Machines (VMs)**
+--------------------------------------------------+
|   VM1   |   VM2   |        VM3                   |
|         |         |  +------------------------+  |
|         |         |  |     Application        |  |
|         |         |  +------------------------+  |
|         |         |  |        Guest OS        |  |
|         |         |  +------------------------+  |
+--------------------------------------------------+
|                 Hypervisor                       |
+--------------------------------------------------+
|               Host OS & Kernel                   |
+--------------------------------------------------+
|                   Hardware                      |
+--------------------------------------------------+

### Key Points: 
  1. Each VM includes a **full Guest OS**.
  2. The **Hypervisor virtualizes hardware** for each VM.
  3. Higher resource usage (memory, CPU, storage).
  4. Networking and storage are managed **per VM via the hypervisor**.

**Docker (Containers)**

+--------------------------------------------------+
|   D1    |   D2    |        D3                    |
|         |         |  +------------------------+  |
|         |         |  |     Application        |  |
|         |         |  +------------------------+  |
|         |         |  |   Container Runtime    |  |
|         |         |  | (from Docker Image)    |  |
|         |         |  +------------------------+  |
+--------------------------------------------------+
|               Docker Engine                      |
+--------------------------------------------------+
|               Host OS & Kernel                   |
+--------------------------------------------------+
|                   Hardware                      |
+--------------------------------------------------+

### Key Points:

Containers share the host OS kernel (no separate OS per container).
Docker Engine manages containers.
Much lighter and faster than VMs.
Networking and storage are handled by Docker, but shared more efficiently.
A Docker Image is the blueprint used to create containers (not a runtime layer like an OS).

---------------------------

**Basic Docker Commands**

--------------------------

**1. docker pull {image_name}:**  Fetch an image from a registry (e.g., Docker Hub)
   
**2. docker run {image_name}:**  Start a new container using the specified image
