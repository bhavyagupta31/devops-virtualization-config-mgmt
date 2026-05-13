# Practical 02: Basic Docker Commands

**Student:** Bhavya Gupta

---

## Aim

To understand and execute basic Docker commands for managing containers and images.

---

## Tools Used

- Docker Desktop
- Windows OS / Terminal

---

## Steps Performed

1. Verified Docker version
2. Pulled and ran the `hello-world` container
3. Listed running containers
4. Listed all containers including stopped ones
5. Pulled an Ubuntu image and ran an interactive container
6. Stopped and removed containers
7. Managed Docker images

---

## Commands Used

### 1. Check Docker Version
```bash
docker --version
```

### 2. Run a Container
```bash
docker run hello-world
```

### 3. List Running Containers
```bash
docker ps
```

### 4. List All Containers (including stopped)
```bash
docker ps -a
```

### 5. Pull an Image
```bash
docker pull ubuntu
```

### 6. Run an Interactive Container
```bash
docker run -it ubuntu bash
```

### 7. Run a Container in Detached Mode
```bash
docker run -d --name my-nginx nginx
```

### 8. Stop a Container
```bash
docker stop <container_id>
```

### 9. Start a Stopped Container
```bash
docker start <container_id>
```

### 10. Remove a Container
```bash
docker rm <container_id>
```

### 11. List All Images
```bash
docker images
```

### 12. Remove an Image
```bash
docker rmi <image_name>
```

### 13. View Container Logs
```bash
docker logs <container_id>
```

### 14. Execute a Command Inside a Running Container
```bash
docker exec -it <container_id> bash
```

### 15. Inspect a Container
```bash
docker inspect <container_id>
```

---

## Output

Basic Docker commands were successfully executed. Containers were created, listed, stopped, and removed without errors.

---

## Screenshot

![Docker Basics Output](output.png)

---

## Conclusion

Basic Docker commands were successfully understood and executed. These commands form the foundation for working with Docker containers and images in any DevOps workflow. Understanding container lifecycle management (create, start, stop, remove) is essential before moving to more advanced topics like Dockerfiles and Docker Compose.
