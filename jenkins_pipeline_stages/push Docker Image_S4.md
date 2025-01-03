# Stage 04 : Push Docker Image Stage

```groovy
stage('Push Docker Image') {
    steps {
        sh "docker push ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
    }
}
```
## **Description:**
This stage uploads the tagged Docker image to Docker Hub or another specified Docker registry.

## Purpose
The Push Docker Image stage uploads the tagged Docker image to the configured Docker registry.

## Implementation
•  The pipeline logs into Docker Hub using credentials:
```groovy
    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
```
•	The image is pushed using:
```groovy
    sh "docker push ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
```
**Key Considerations**
- Ensure that valid Docker Hub credentials are configured in Jenkins.
- Verify that the pipeline agent has access to the Docker CLI.
- Confirm the registry is reachable and the image tag is unique (or set to overwrite).