
# **`Stage 03-Tag-Docker-Image`**

```groovy
stage('Tag Docker Image') {
    steps {
        script {
            // Tag the Docker image with the full registry name
            sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
        }
    }
}
```

## **Description:**
This stage tags the built Docker image with a specific name and pushes it to the Docker registry.

## Purpose
The Tag Docker Image stage adds a registry-specific tag to the Docker image, preparing it for upload to the Docker registry.

## Implementation
- The `docker tag` command assigns a new tag:
  ```groovy
  sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"

## **Key Considerations**

•	Ensure that the registry name, image name, and tag are configured correctly.
•	Confirm that the image name follows the Docker Hub naming conventions.