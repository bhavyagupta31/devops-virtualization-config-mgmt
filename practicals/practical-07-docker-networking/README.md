# Practical 07: Docker Networking

**Student:** Bhavya Gupta

---

## Objective

To understand Docker networking concepts and demonstrate how containers communicate with each other using different network types.

---

## Tools Used

- Docker Desktop
- Ubuntu and Nginx containers

---

## Docker Network Types

| Network Type | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| bridge       | Default network. Containers on the same bridge can communicate by IP.       |
| host         | Container shares the host's network stack directly.                         |
| none         | Container has no network access.                                            |
| overlay      | Used in Docker Swarm for multi-host networking.                             |
| custom bridge| User-defined bridge network — containers can communicate by container name. |

---

## Steps Performed

1. Listed existing Docker networks
2. Created a custom bridge network
3. Ran two containers on the same custom network
4. Verified containers can ping each other by container name (DNS resolution)
5. Ran a container on the `host` network
6. Ran a container with `--network none` to verify isolation
7. Inspected network details

---

## Commands Used

```bash
# List all Docker networks
docker network ls

# Inspect the default bridge network
docker network inspect bridge

# Create a custom bridge network
docker network create my-network

# Run container 1 on the custom network
docker run -d --name container1 --network my-network nginx

# Run container 2 on the custom network
docker run -it --name container2 --network my-network ubuntu bash

# Inside container2 — ping container1 by name (DNS works on custom networks)
apt update && apt install -y iputils-ping
ping container1

# Connect an existing container to a network
docker network connect my-network <container_id>

# Disconnect a container from a network
docker network disconnect my-network <container_id>

# Inspect the custom network
docker network inspect my-network

# Run a container with host networking
docker run --rm --network host nginx

# Run a container with no networking
docker run --rm --network none ubuntu bash

# Remove a custom network
docker network rm my-network

# Remove all unused networks
docker network prune
```

---

## Key Observations

| Scenario                                      | Result                                      |
|-----------------------------------------------|---------------------------------------------|
| Two containers on default bridge network      | Can communicate by IP only                  |
| Two containers on custom bridge network       | Can communicate by container name (DNS)     |
| Container on host network                     | Shares host IP, no port mapping needed      |
| Container on none network                     | Completely isolated, no network access      |

---

## Output

```
PING container1 (172.18.0.2): 56 data bytes
64 bytes from 172.18.0.2: icmp_seq=0 ttl=64 time=0.123 ms
64 bytes from 172.18.0.2: icmp_seq=1 ttl=64 time=0.098 ms
```

Containers on the same custom network successfully communicated using container names.

---

## Concepts Covered

| Concept              | Description                                                       |
|----------------------|-------------------------------------------------------------------|
| Bridge network       | Default isolated network for containers on the same host          |
| Custom bridge        | User-defined network with automatic DNS resolution by name        |
| Host network         | Container uses host's network directly                            |
| Network isolation    | `--network none` completely isolates a container                  |
| DNS in Docker        | Custom networks provide automatic service discovery by name       |
| Port publishing      | `-p host:container` exposes container ports to the host           |

---

## Conclusion

Docker networking was successfully explored. Custom bridge networks provide automatic DNS resolution between containers, making them ideal for multi-container applications. Understanding Docker networking is essential for building secure, well-connected containerized applications.
