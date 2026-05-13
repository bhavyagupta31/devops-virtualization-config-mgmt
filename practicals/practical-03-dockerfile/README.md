# 🐳 Practical 03: Dockerfile Implementation

**Student:** Bhavya Gupta

---

## 🎯 Objective

To create a custom Docker image using a Dockerfile and run a container from it successfully.

---

## 🧰 Tools & Technologies Used

- 🐳 Docker
- 💻 Git & GitHub

---

## 📌 Steps Performed

1. Created a `Dockerfile` with base image `ubuntu:latest`
2. Added `RUN` instruction to install `curl`
3. Added `CMD` instruction to print a message on container start
4. Built the Docker image using `docker build`
5. Ran the container from the built image
6. Verified the output message

---

## 📄 Dockerfile

```dockerfile
FROM ubuntu:latest

RUN apt update && apt install -y curl

CMD ["echo", "Hello from custom Docker image"]
```

---

## 📜 Commands Used

```bash
# Build the Docker image
docker build -t my-first-image .

# Run the container
docker run my-first-image

# List images to verify
docker images
```

---

## ✅ Output

```
Hello from custom Docker image
```

The container ran successfully and printed the expected message.

---

## 📸 Screenshot

![Dockerfile Output](output.png)

---

## 📝 Conclusion

A custom Docker image was successfully built using a Dockerfile. The image was based on Ubuntu, had `curl` installed, and printed a custom message when the container was run. This demonstrates the core concept of image creation in Docker.
