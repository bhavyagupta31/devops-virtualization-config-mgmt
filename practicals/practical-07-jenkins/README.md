# 🐳 Practical 07: Jenkins CI/CD Pipeline

**Student:** Bhavya Gupta

---

## 🎯 Objective

To implement a CI/CD pipeline using Jenkins running inside a Docker container.

---

## 🧰 Tools Used

- Jenkins (LTS Docker image)
- Docker

---

## 📌 Steps Performed

1. Pulled and ran the Jenkins LTS container using Docker
2. Accessed the Jenkins dashboard at `http://localhost:8081`
3. Retrieved the initial admin password from the container
4. Completed the Jenkins setup wizard and installed suggested plugins
5. Created a new Pipeline job
6. Defined the pipeline using a `Jenkinsfile` (Declarative Pipeline syntax)
7. Executed the pipeline and verified all stages passed

---

## 📜 Commands Used

```bash
# Run Jenkins container
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

## 📄 Jenkinsfile

See [Jenkinsfile](Jenkinsfile)

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

## ✅ Output

Pipeline executed successfully with all stages passing:
- ✅ Checkout
- ✅ Build
- ✅ Test
- ✅ Deploy

---

## 📸 Screenshots

### Jenkins Dashboard
![Dashboard](dashboard.png)

### Pipeline Stages Output
![Stages](stages.png)

---

## 💡 Concepts Covered

| Concept | Description |
|---------|-------------|
| CI/CD | Continuous Integration and Continuous Delivery |
| Jenkins Pipeline | Declarative pipeline using Groovy DSL |
| Stages | Logical grouping of pipeline steps |
| Post Actions | Actions on pipeline success/failure |
| Docker + Jenkins | Running Jenkins as a Docker container |

---

## 📝 Conclusion

A CI/CD pipeline was successfully implemented using Jenkins running inside a Docker container. The Declarative Pipeline syntax made it easy to define stages for checkout, build, test, and deploy — demonstrating the core concepts of automated software delivery.
