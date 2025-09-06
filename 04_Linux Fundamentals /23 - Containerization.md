# Containerization
## What is Containerization?

**Containerization** is a method of packaging an application with all of its dependencies—such as libraries, configuration files, and system tools—into a single, runnable unit called a **container**.

*   **Core Idea:** Containers provide a consistent and portable environment. An application running in a container will behave exactly the same way, regardless of whether it's on a developer's laptop, a testing server, or in a production cloud environment.
*   **Analogy:** A container is like a portable, self-contained "stage pod" for a band. The pod has everything the band needs (instruments, lights, speakers) pre-configured. You can drop this pod onto any main stage (a host OS), and it will work perfectly without interfering with other bands' pods.

### Containers vs. Virtual Machines (VMs)
This is a critical distinction.
*   **Virtual Machines:** Each VM runs a **full guest operating system**, including its own kernel. They are heavyweight and provide strong hardware-level isolation.
*   **Containers:** Containers **share the host operating system's kernel**. They are much more lightweight, start up faster, and use significantly fewer resources. Their isolation is at the OS level, not the hardware level.

---

## 1. Docker

**Docker** is the most popular open-source platform for building, shipping, and running applications inside containers. It simplified containerization and made it accessible to a wide audience.

### Key Docker Concepts
*   **Dockerfile:** A text-based "recipe" or script that contains all the instructions needed to build a Docker image.
*   **Docker Image:** A read-only, lightweight, standalone, and executable template that includes everything needed to run an application. Images are built from a Dockerfile.
*   **Docker Container:** A running instance of a Docker image. It is the live, executable environment.
*   **Docker Hub:** A cloud-based public registry (like a library) for storing and sharing Docker images.

### The Docker Workflow
1.  **Write a `Dockerfile`:** Define the base OS, software to install, files to copy, and the command to run when the container starts.
2.  **Build the Image (`docker build`):** Use the `Dockerfile` to create a reusable Docker image.
    ```shell
    # Build an image and tag it with the name "fs_docker"
    docker build -t fs_docker .
    ```
3.  **Run the Container (`docker run`):** Start a new, running container from the image.
    ```shell
    # Run the container in the background (-d) and map host ports to container ports (-p)
    docker run -p 8080:80 -p 8022:22 -d fs_docker
    ```
    *(This maps port 8080 on the host to port 80 inside the container, and port 8022 on the host to port 22 inside the container).*

### Essential Docker Management Commands

| Command | Description |
| :--- | :--- |
| `docker ps` | Lists all **running** containers. `docker ps -a` lists all containers, including stopped ones. |
| `docker stop <container_id>` | Stops a running container gracefully. |
| `docker start <container_id>` | Starts a stopped container. |
| `docker rm <container_id>` | Removes a stopped container. |
| `docker rmi <image_id>` | Removes a Docker image. |
| `docker logs <container_id>` | Displays the logs (STDOUT/STDERR) from a running container. |

**Important Note:** Docker containers are **stateless** by default. Any changes made inside a running container are lost when it is stopped or removed. To persist data, you must use **Docker volumes**.

---

## 2. Linux Containers (LXC)

**LXC** is a lower-level, OS-level virtualization method. It is the underlying technology that Docker was originally built on top of.

*   **Core Idea:** LXC focuses on creating isolated Linux environments that behave like lightweight, full-fledged virtual machines. It is more of a "system container" technology.
*   **Isolation:** LXC uses Linux kernel features like **namespaces** (to isolate process IDs, networks, etc.) and **cgroups** (to limit resource usage like CPU and memory) to create this isolation.

### Docker vs. LXC

| Feature | Docker | LXC |
| :--- | :--- | :--- |
| **Focus** | **Application-centric.** Designed to run a single application or process per container. | **System-centric.** Designed to run a full Linux environment with multiple processes, like a lightweight VM. |
| **Ease of Use**| Very user-friendly with a simple CLI and a massive ecosystem (Docker Hub). | More powerful and flexible, but requires more in-depth Linux administration knowledge. |
| **Portability**| Excellent. Docker images are standardized and highly portable. | Less portable. Containers are more tightly coupled to the host system's configuration. |

### LXC Management Commands
*   **Install LXC:** `sudo apt-get install lxc lxc-utils -y`
*   **Create a container:** `sudo lxc-create -n <container_name> -t <template>` (e.g., `-t ubuntu`)
*   **List containers:** `sudo lxc-ls`
*   **Start/Stop a container:** `sudo lxc-start -n <name>` / `sudo lxc-stop -n <name>`
*   **Attach to a container's shell:** `sudo lxc-attach -n <name>`

### Security Implications
Both Docker and LXC provide strong isolation, but they are not perfect. Misconfigurations or kernel vulnerabilities can potentially lead to a **container escape**, where a process inside a container breaks out and gains access to the host operating system. This is a critical area of concern in container security.
