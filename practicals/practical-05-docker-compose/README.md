# 🐳 Practical 05: Docker Compose (WordPress + MySQL)

**Student:** Bhavya Gupta

---

## 🎯 Objective

To use Docker Compose to define and run a multi-container application (WordPress with MySQL backend).

---

## 🧰 Tools Used

- Docker Desktop
- Docker Compose
- WordPress image
- MySQL 5.7 image

---

## 📌 Steps Performed

1. Created a `docker-compose.yml` file defining two services: `db` (MySQL) and `wordpress`
2. Configured environment variables for database credentials
3. Set up a named volume for MySQL data persistence
4. Ran the application using `docker compose up`
5. Accessed WordPress setup page at `http://localhost:8080`
6. Verified both containers were running

---

## 📄 docker-compose.yml

See [docker-compose.yml](docker-compose.yml)

---

## 📜 Commands Used

```bash
# Start all services in detached mode
docker compose up -d

# Check running containers
docker compose ps

# View logs
docker compose logs

# Stop all services
docker compose down

# Stop and remove volumes
docker compose down -v
```

---

## ✅ Output

- WordPress setup page was accessible at `http://localhost:8080`
- Both `wordpress-app` and `wordpress-db` containers were running
- MySQL data was persisted via the `db_data` volume

---

## 📸 Screenshots

### WordPress Setup Page
![WordPress](wordpress-output.png)

### Docker Compose Running
![Docker Compose](docker-compose-output.png)

---

## 💡 Concepts Covered

- Docker Compose file structure (`services`, `volumes`, `environment`)
- Multi-container application orchestration
- Service dependencies (`depends_on`)
- Port mapping
- Named volumes for persistence

---

## 📝 Conclusion

Docker Compose successfully orchestrated a multi-container WordPress application. The `docker-compose.yml` file made it easy to define, configure, and launch both the WordPress and MySQL containers with a single command.
