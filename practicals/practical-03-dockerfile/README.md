# Practical 03: Dockerfile Implementation

**Student:** Bhavya Gupta

---

## Objective

To create a custom Docker image using a Dockerfile and run a container from it successfully.

---

## Tools & Technologies Used

- Docker
- Git & GitHub

---

## What is a Dockerfile?

A Dockerfile is a text file containing a set of instructions that Docker uses to build a custom image. Each instruction in the Dockerfile creates a new layer in the image. Common instructions include:

| Instruction | Purpose |
|-------------|---------|
| FROM        | Sets the base image |
| RUN         | Executes a command during image build |
| COPY        | Copies files from host to image |
| ADD         | Like COPY but supports URLs and tar extraction |
| CMD         | Default command to run when container starts |
| ENTRYPOINT  | Configures the container to run as an executable |
| EXPOSE      | Documents the port the container listens on |
| ENV         | Sets environment variables |
| WORKDIR     | Sets the working directory inside the container |

---

## Steps Performed

1. Created a `Dockerfile` with base image `ubuntu:latest`
2. Added `RUN` instruction to update packages and install `curl`
3. Added `CMD` instruction to print a message on container start
4. Built the Docker image using `docker build`
5. Ran the container from the built image
6. Verified the output message
7. Listed images to confirm the new image was created

---

## Dockerfile

```dockerfile
FROM ubuntu:latest

RUN apt update && apt install -y curl

CMD ["echo", "Hello from custom Docker image"]
```

---

## Commands Used

```bash
# Build the Docker image and tag it
docker build -t my-first-image .

# Run the container
docker run my-first-image

# List images to verify
docker images

# View image details
docker inspect my-first-image

# Remove the image
docker rmi my-first-image
```

---

## Output

```
Hello from custom Docker image
```

The container ran successfully and printed the expected message.

---

## Screenshot

![Dockerfile Output](output.png)

---

## Conclusion

A custom Docker image was successfully built using a Dockerfile. The image was based on Ubuntu, had `curl` installed as an additional package, and printed a custom message when the container was run. This demonstrates the core concept of image creation in Docker — packaging an application and its dependencies into a portable, reproducible image.
