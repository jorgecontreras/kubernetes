# Podman Basics

Podman is a container engine similar to Docker but daemonless and designed for security and rootless container management. It’s an alternative to Docker that can be used in Kubernetes workflows.

---

## **Key Podman Features**
1. **Daemonless**:
   - Runs without a centralized daemon, reducing overhead and improving security.
2. **Rootless Mode**:
   - Allows users to run containers without requiring root privileges.
3. **Docker-Compatible Commands**:
   - Podman supports Docker-compatible commands, making migration easier.

---

## **Common Commands**

1. **Manage Images**:
   - List images:
     ```bash
     podman images
     ```
   - Pull an image:
     ```bash
     podman pull nginx
     ```

2. **Manage Containers**:
   - Run a container:
     ```bash
     podman run -d nginx
     ```
   - List containers:
     ```bash
     podman ps
     ```
   - Remove a container:
     ```bash
     podman rm <container-id>
     ```

3. **Rootless Containers**:
   - Start a rootless container:
     ```bash
     podman run --name rootless-container -d nginx
     ```

---

## **References**
- [Podman Documentation](https://podman.io/)
