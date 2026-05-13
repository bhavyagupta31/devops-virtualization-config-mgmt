# Practical 05: Docker Compose — WordPress + MySQL

**Student:** Bhavya Gupta

---

## Objective

To use Docker Compose to define and run a multi-container application consisting of WordPress (frontend) and MySQL (database backend).

---

## Tools Used

- Docker Desktop
- Docker Compose
- WordPress image (latest)
- MySQL 5.7 image

---

## What is Docker Compose?

Docker Compose is a tool for defining and running multi-container Docker applications. Using a single `docker-compose.yml` file, you can configure all your application's services, networks, and volumes, then start everything with one command.

Key concepts:
- **Services** — individual containers (e.g., web, db)
- **Networks** — how containers communicate with each other
- **Volumes** — persistent storage for containers
- **depends_on** — defines startup order between services

---

## Steps Performed

1. Created a `docker-compose.yml` file defining two services: `db` (MySQL) and `wordpress`
2. Configured environment variables for database credentials
3. Set up a named volume for MySQL data persistence
4. Ran the application using `docker compose up -d`
5. Accessed WordPress setup page at `http://localhost:8080`
6. Verified both containers were running with `docker compose ps`
7. Stopped the application using `docker compose down`

---

## docker-compose.yml

```yaml
version: '3.8'

services:
  db:
    image: mysql:5.7
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_DATABASE: wpdb
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
      MYSQL_ROOT_PASSWORD: rootpass
    volumes:
      - db-data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wpdb
    depends_on:
      - db

volumes:
  db-data:
```

---

## Commands Used

```bash
# Start all services in detached mode
docker compose up -d

# Check running containers
docker compose ps

# View logs for all services
docker compose logs

# View logs for a specific service
docker compose logs wordpress

# Stop all services (keeps volumes)
docker compose down

# Stop and remove volumes
docker compose down -v
```

---

## Output

- WordPress setup page was accessible at `http://localhost:8080`
- Both `wordpress-app` and `mysql-db` containers were running
- MySQL data was persisted via the `db-data` volume

---

## Screenshots

### WordPress Setup Page
![WordPress](wordpress-output.png)

### Docker Compose Running
![Docker Compose](docker-compose-output.png)

---

## Concepts Covered

| Concept                  | Description                                          |
|--------------------------|------------------------------------------------------|
| docker-compose.yml       | YAML file defining all services, volumes, networks   |
| Multi-container apps     | Running multiple containers as a single application  |
| Service dependencies     | `depends_on` ensures db starts before wordpress      |
| Port mapping             | `"8080:80"` maps host port 8080 to container port 80 |
| Named volumes            | Persistent storage for MySQL data                    |
| Environment variables    | Passing config to containers at runtime              |

---

## Conclusion

Docker Compose successfully orchestrated a multi-container WordPress application. The `docker-compose.yml` file made it easy to define, configure, and launch both the WordPress and MySQL containers with a single command, demonstrating the power of container orchestration for multi-service applications.
