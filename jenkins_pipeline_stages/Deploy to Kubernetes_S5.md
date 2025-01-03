# Deploy to Kubernetes
---

### **`05-Deploy-to-Kubernetes.md`**

## Jenkins Pipeline - Deploy to Kubernetes Stage

```groovy
stage('Deploy to Kubernetes') {
    steps {
        script {
            // Set the Kubernetes context
            sh "kubectl config use-context ${KUBERNETES_CLUSTER_CONTEXT}"

            // Deploy the new Docker image to Kubernetes using kubectl
            sh """
                kubectl set image deployment/frontend ${IMAGE_NAME}=${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG} --namespace=${KUBERNETES_NAMESPACE}
                kubectl rollout status deployment/frontend --namespace=${KUBERNETES_NAMESPACE}
            """
        }
    }
}

#### **Title:** Deploy to Kubernetes Stage

#### **Description:**
This stage deploys the newly built and pushed Docker image to a Kubernetes cluster.

#### **Content for the `.md` file:**
```markdown
# Deploy to Kubernetes Stage

## Purpose
The Deploy to Kubernetes stage updates the Kubernetes deployment with the new Docker image.

## Implementation
- The Kubernetes context is set using:
  ```groovy
  sh "kubectl config use-context ${KUBERNETES_CLUSTER_CONTEXT}"
•	The kubectl set image command updates the deployment:

    sh "kubectl set image deployment/frontend ${IMAGE_NAME}=${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG} --namespace=${KUBERNETES_NAMESPACE}"

•	The rollout status is checked:
sh "kubectl rollout status deployment/frontend --namespace=${KUBERNETES_NAMESPACE}"

Key Considerations
	•	Ensure the Kubernetes context is configured correctly on the Jenkins agent.
	•	Verify that the Kubernetes namespace and deployment names are correct.
	•	Confirm that the agent has kubectl installed and sufficient permissions.