# **Stage 02:** Build Docker Image

```groovy
stage('Build Docker Image') {
    steps {
        script {
            // Build the Docker image
            sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
        }
    }
}
```
**Description:** This stage builds a Docker image using the application's source code and a `Dockerfile`.


# Build Docker Image Stage
The Build Docker Image stage creates a Docker image containing the application, using the codebase and the `Dockerfile` located in the repository.

## Implementation
The `docker build` command is used to create the Docker image:
groovy
  ```bash
  sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
```
The ${DOCKER_IMAGE} and ${DOCKER_TAG} are environment variables that define the name and tag of the image.

**Key Considerations**:

•	Ensure that the Dockerfile is present and correctly configured in 	the repository.
•	Validate the base image and dependencies in the Dockerfile.
•	Confirm that the agent running the pipeline has Docker installed.