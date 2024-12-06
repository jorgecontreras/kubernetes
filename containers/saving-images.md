# Saving and Loading Images

In Kubernetes workflows, you might need to save and load container images, especially in air-gapped environments or when working offline.

---

## **Save an Image**

1. **Docker**:
   - Save an image to a file:
     ```bash
     docker save -o my-image.tar my-image:1.0
     ```

2. **Podman**:
   - Save an image to a file:
     ```bash
     podman save -o my-image.tar my-image:1.0
     ```

---

## **Load an Image**

1. **Docker**:
   - Load an image from a file:
     ```bash
     docker load -i my-image.tar
     ```

2. **Podman**:
   - Load an image from a file:
     ```bash
     podman load -i my-image.tar
     ```

---

## **References**
- [Docker Save and Load](https://docs.docker.com/engine/reference/commandline/save/)
- [Podman Save and Load](https://podman.io/getting-started/)