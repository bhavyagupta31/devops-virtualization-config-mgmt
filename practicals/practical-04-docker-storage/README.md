# 🐳 Practical 04: Docker Storage (Volumes)

**Student:** Bhavya Gupta

---

## 🎯 Objective

To understand Docker volumes and demonstrate data persistence across container lifecycles.

---

## 🧰 Tools Used

- Docker Desktop
- Ubuntu container

---

## 📌 Steps Performed

1. Created a Docker named volume using `docker volume create`
2. Ran an Ubuntu container with the volume mounted at `/data`
3. Created a file inside the container at the mounted path
4. Exited and removed the container
5. Started a new container with the same volume mounted
6. Verified that the previously created file still exists (data persisted)

---

## 📜 Commands Used

```bash
# Create a named volume
docker volume create my-volume

# Run a container with the volume mounted
docker run -it -v my-volume:/data ubuntu bash

# Inside the container — create a file
echo "Hello Volume" > /data/test.txt
exit

# Run a new container with the same volume
docker run -it -v my-volume:/data ubuntu bash

# Inside the new container — verify the file persists
cat /data/test.txt

# List all volumes
docker volume ls

# Inspect a volume
docker volume inspect my-volume

# Remove a volume (cleanup)
docker volume rm my-volume
```

---

## ✅ Output

```
Hello Volume
```

The file created in the first container was accessible in the second container, confirming data persistence via Docker volumes.

---

## 💡 Concepts Covered

| Concept | Description |
|---------|-------------|
| Docker Volumes | Named storage managed by Docker |
| Data Persistence | Data survives container removal |
| Volume Mounting | Attaching volumes to containers via `-v` flag |
| Container Storage | Difference between ephemeral and persistent storage |

---

## 📝 Conclusion

Docker volumes successfully demonstrated data persistence. Data written inside a container to a mounted volume remained available even after the container was stopped and removed, which is essential for stateful applications like databases.
