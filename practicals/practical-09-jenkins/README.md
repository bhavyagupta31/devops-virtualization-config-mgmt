# Practical 09: Jenkins CI/CD Pipeline

**Student:** Bhavya Gupta

---

## Objective

To implement a CI/CD pipeline using Jenkins running inside a Docker container, with a Declarative Pipeline defined in a Jenkinsfile.

---

## Tools Used

- Jenkins (LTS Docker image)
- Docker

---

## What is Jenkins?

Jenkins is an open-source automation server used to implement CI/CD pipelines. It supports building, testing, and deploying applications automatically. Jenkins pipelines can be defined using a `Jenkinsfile` which uses Groovy-based Declarative or Scripted syntax.

Key concepts:
- **Pipeline** — a series of automated steps to build, test, and deploy code
- **Stage** — a logical grouping of steps (e.g., Build, Test, Deploy)
- **Step** — a single task within a stage
- **Agent** — the machine or container that runs the pipeline
- **Post** — actions to run after the pipeline completes (success/failure)

---

## Steps Performed

1. Pulled and ran the Jenkins LTS container using Docker
2. Accessed the Jenkins dashboard at `http://localhost:8081`
3. Retrieved the initial admin password from the container
4. Completed the Jenkins setup wizard and installed suggested plugins
5. Created a new Pipeline job
6. Defined the pipeline using a `Jenkinsfile` (Declarative Pipeline syntax)
7. Executed the pipeline and verified all stages passed

---

## Commands Used

```bash
# Run Jenkins container with persistent volume
docker run -d \
  -p 8081:8080 \
  -p 50000:50000 \
  --name jenkins-server \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts

# Get the initial admin password
docker exec jenkins-server cat /var/jenkins_home/secrets/initialAdminPassword

# Check container logs
docker logs jenkins-server

# Stop Jenkins
docker stop jenkins-server

# Start Jenkins again
docker start jenkins-server
```

---

## Jenkinsfile

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
```

---

## Output

Pipeline executed successfully with all stages passing:
- Checkout — passed
- Build — passed
- Test — passed
- Deploy — passed

---

## Screenshots

### Jenkins Dashboard
![Dashboard](dashboard.png)

### Pipeline Stages Output
![Stages](stages.png)

---

## Concepts Covered

| Concept              | Description                                                    |
|----------------------|----------------------------------------------------------------|
| CI/CD                | Continuous Integration and Continuous Delivery                 |
| Jenkins Pipeline     | Declarative pipeline using Groovy DSL                          |
| Stages               | Logical grouping of pipeline steps                             |
| Post Actions         | Actions triggered on pipeline success or failure               |
| Docker + Jenkins     | Running Jenkins as a Docker container with persistent storage  |
| Jenkinsfile          | Pipeline-as-code stored in the repository                      |

---

## Conclusion

A CI/CD pipeline was successfully implemented using Jenkins running inside a Docker container. The Declarative Pipeline syntax made it easy to define stages for checkout, build, test, and deploy. Storing the pipeline as a `Jenkinsfile` in the repository enables version control of the pipeline itself, which is a best practice in modern DevOps workflows.
