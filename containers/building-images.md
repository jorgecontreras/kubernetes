# Building Docker and Podman Images

Building custom images is a fundamental skill for deploying applications in containers. This involves creating a Dockerfile and using either Docker or Podman to build the image.

---

## Steps to Build an Image

1. **Create a Dockerfile**:
   - Example:
     ```Dockerfile
     FROM ubuntu:20.04
     RUN apt-get update && apt-get install -y curl
     CMD ["bash"]
     ```

2. **Build the Image**:
   - Docker:
     ```bash
     docker build -t my-image:1.0 .
     ```
   - Podman:
     ```bash
     podman build -t my-image:1.0 .
     ```

3. **Verify the Image**:
   - Docker:
     ```bash
     docker images
     ```
   - Podman:
     ```bash
     podman images
     ```

---

## Tagging Images
- Tag an image for a registry:
```bash
docker tag my-image:1.0 my-registry/my-image:1.0
```

## Push the image to a registry
```bash
docker push my-registry/my-image:1.0
```