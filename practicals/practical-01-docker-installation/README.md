# Practical 01: Docker Installation and Verification

**Student:** Bhavya Gupta

---

## Aim

To install Docker on a local machine and verify its working by running a test container.

---

## Tools Used

- Docker Desktop
- Windows OS

---

## Steps Performed

1. Downloaded Docker Desktop from https://www.docker.com/products/docker-desktop
2. Installed Docker Desktop and restarted the system
3. Opened terminal (PowerShell / Command Prompt)
4. Verified Docker installation using `docker --version`
5. Ran the `hello-world` container to confirm Docker is working

---

## Commands Used

```bash
# Check Docker version
docker --version

# Run the hello-world test container
docker run hello-world

# Check Docker system info
docker info
```

---

## Output

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image.
 4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.
```

---

## Screenshot

![Docker Installation Output](output.png)

---

## Conclusion

Docker was successfully installed and verified on the local machine. The `hello-world` container ran without errors, confirming that Docker Engine is properly set up and able to pull images from Docker Hub and run containers.
