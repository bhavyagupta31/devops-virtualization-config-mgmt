# Practical 06: Docker Compose — Full-Stack Application (Node.js + Java + PostgreSQL)

**Student:** Bhavya Gupta

---

## Objective

To use Docker Compose to run a full-stack three-tier application consisting of a React/Node.js frontend, a Java Spring Boot backend, and a PostgreSQL database — all connected via Docker networking.

---

## Tools Used

- Docker Desktop
- Docker Compose
- Node.js 18 (frontend)
- OpenJDK 17 (backend)
- PostgreSQL 15 (database)

---

## Application Architecture

```
+------------------+       +------------------+       +------------------+
|   Frontend       |  -->  |   Backend        |  -->  |   Database       |
|   Node.js 18     |       |   Java (JDK 17)  |       |   PostgreSQL 15  |
|   Port: 3000     |       |   Port: 8080     |       |   Port: 5432     |
+------------------+       +------------------+       +------------------+
```

- The frontend communicates with the backend via `REACT_APP_API_URL`
- The backend connects to PostgreSQL using environment variables
- All three services share a Docker Compose-managed network

---

## Steps Performed

1. Created the `docker-compose.yml` file with three services: `frontend`, `backend`, `db`
2. Configured environment variables for inter-service communication
3. Set up a named volume for PostgreSQL data persistence
4. Used bind mounts to mount local source code into containers for development
5. Defined service dependencies to ensure correct startup order
6. Started all services with `docker compose up -d`
7. Verified all three containers were running
8. Tested frontend at `http://localhost:3000` and backend at `http://localhost:8080`

---

## docker-compose.yml

```yaml
version: "3.9"

services:
  frontend:
    image: node:18
    container_name: frontend
    working_dir: /app
    volumes:
      - ./frontend:/app
    command: npm start
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://backend:8080
    depends_on:
      - backend

  backend:
    image: openjdk:17
    container_name: backend
    working_dir: /app
    volumes:
      - ./backend:/app
    command: ["java", "-jar", "app.jar"]
    ports:
      - "8080:8080"
    environment:
      - DB_HOST=db
      - DB_PORT=5432
      - DB_NAME=mydb
      - DB_USER=postgres
      - DB_PASSWORD=postgres
    depends_on:
      - db

  db:
    image: postgres:15
    container_name: postgres_db
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_DB=mydb
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

---

## Commands Used

```bash
# Start all services
docker compose up -d

# Check all running services
docker compose ps

# View logs for all services
docker compose logs

# View logs for a specific service
docker compose logs backend

# Access the PostgreSQL database shell
docker exec -it postgres_db psql -U postgres -d mydb

# Restart a specific service
docker compose restart backend

# Rebuild and restart (after code changes)
docker compose up -d --build

# Stop all services
docker compose down

# Stop and remove volumes (full cleanup)
docker compose down -v
```

---

## Environment Variables Explained

| Variable              | Service   | Description                              |
|-----------------------|-----------|------------------------------------------|
| REACT_APP_API_URL     | frontend  | Backend API URL for React to call        |
| DB_HOST               | backend   | Hostname of the database service         |
| DB_PORT               | backend   | PostgreSQL port                          |
| DB_NAME               | backend   | Database name to connect to              |
| DB_USER               | backend   | Database username                        |
| DB_PASSWORD           | backend   | Database password                        |
| POSTGRES_DB           | db        | Database name to create on startup       |
| POSTGRES_USER         | db        | PostgreSQL superuser username            |
| POSTGRES_PASSWORD     | db        | PostgreSQL superuser password            |

---

## Output

- Frontend accessible at `http://localhost:3000`
- Backend API accessible at `http://localhost:8080`
- PostgreSQL running on port `5432`
- All three containers running and communicating via Docker's internal network

---

## Concepts Covered

| Concept                  | Description                                                  |
|--------------------------|--------------------------------------------------------------|
| Three-tier architecture  | Frontend, backend, and database as separate services         |
| Service communication    | Containers communicate using service names as hostnames      |
| Bind mounts              | Local source code mounted into containers for development    |
| Named volumes            | Persistent storage for PostgreSQL data                       |
| depends_on               | Controls startup order of services                           |
| Environment variables    | Injecting configuration into containers at runtime           |

---

## Conclusion

A full-stack three-tier application was successfully orchestrated using Docker Compose. The frontend, backend, and database services communicated seamlessly over Docker's internal network. This practical demonstrates how Docker Compose can be used to replicate a production-like environment locally for development and testing.
