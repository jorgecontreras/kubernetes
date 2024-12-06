# Docker Basics

Docker is a containerization platform that allows you to build, ship, and run applications inside lightweight, portable containers. Understanding Docker is crucial for working with Kubernetes, as Pods use containers to encapsulate applications.

---

## **Key Docker Concepts**

1. **Image**:
   - A template used to create containers, consisting of application code, dependencies, and system tools.
   - Example:
     ```bash
     docker pull nginx
     ```

2. **Container**:
   - A running instance of a Docker image.
   - Example:
     ```bash
     docker run -d nginx
     ```

3. **Dockerfile**:
   - A script defining the steps to create a Docker image.
   - Example:
     ```Dockerfile
     FROM nginx:latest
     COPY index.html /usr/share/nginx/html
     ```

---

## **Common Commands**

1. **Manage Images**:
   - List images:
     ```bash
     docker images
     ```
   - Remove an image:
     ```bash
     docker rmi <image-id>
     ```

2. **Manage Containers**:
   - List running containers:
     ```bash
     docker ps
     ```
   - Start/stop a container:
     ```bash
     docker start <container-id>
     docker stop <container-id>
     ```
   - Remove a container:
     ```bash
     docker rm <container-id>
     ```

3. **Run a Container**:
   - Run interactively:
     ```bash
     docker run -it ubuntu bash
     ```
   - Run in detached mode:
     ```bash
     docker run -d nginx
     ```

---

## **References**
- [Docker Documentation](https://docs.docker.com/)
