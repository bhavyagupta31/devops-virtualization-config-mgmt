# Practical 04: Docker Storage (Volumes)

**Student:** Bhavya Gupta

---

## Objective

To understand Docker storage options and demonstrate data persistence across container lifecycles using Docker volumes.

---

## Tools Used

- Docker Desktop
- Ubuntu container

---

## Docker Storage Types

Docker provides three main storage options:

| Type         | Description                                                  | Use Case                        |
|--------------|--------------------------------------------------------------|---------------------------------|
| Volumes      | Managed by Docker, stored in Docker's storage area          | Databases, persistent app data  |
| Bind Mounts  | Maps a host directory directly into the container           | Development, config files       |
| tmpfs Mounts | Stored in host memory only, not persisted to disk           | Sensitive/temporary data        |

---

## Steps Performed

1. Created a Docker named volume using `docker volume create`
2. Ran an Ubuntu container with the volume mounted at `/data`
3. Created a file inside the container at the mounted path
4. Exited and removed the container
5. Started a new container with the same volume mounted
6. Verified that the previously created file still exists (data persisted)
7. Demonstrated bind mount as an alternative approach

---

## Commands Used

```bash
# Create a named volume
docker volume create my-volume

# List all volumes
docker volume ls

# Inspect a volume (shows mount path on host)
docker volume inspect my-volume

# Run a container with the volume mounted
docker run -it -v my-volume:/data ubuntu bash

# Inside the container — create a file
echo "Hello Volume" > /data/test.txt
cat /data/test.txt
exit

# Remove the container
docker rm <container_id>

# Run a NEW container with the same volume — data should still be there
docker run -it -v my-volume:/data ubuntu bash

# Inside the new container — verify the file persists
cat /data/test.txt

# Bind mount example — mount current host directory into container
docker run -it -v $(pwd):/workspace ubuntu bash

# Remove a volume (cleanup)
docker volume rm my-volume

# Remove all unused volumes
docker volume prune
```

---

## Output

```
Hello Volume
```

The file created in the first container was accessible in the second container, confirming data persistence via Docker volumes.

---

## Concepts Covered

| Concept             | Description                                                  |
|---------------------|--------------------------------------------------------------|
| Docker Volumes      | Named storage managed by Docker daemon                       |
| Data Persistence    | Data survives container stop, restart, and removal           |
| Volume Mounting     | Attaching volumes to containers via the `-v` flag            |
| Bind Mounts         | Mapping host directories directly into containers            |
| Volume Lifecycle    | Create, inspect, list, and remove volumes                    |

---

## Conclusion

Docker volumes successfully demonstrated data persistence. Data written inside a container to a mounted volume remained available even after the container was stopped and removed. This is critical for stateful applications like databases, where data must survive container restarts and upgrades.
