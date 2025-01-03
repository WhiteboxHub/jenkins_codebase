# Jenkins Pipeline

A Jenkins Pipeline is a suite of plugins that supports building, deploying, and automating projects.

Selecting the Pipeline Source:

Blue Ocean supports various SCM systems like Git, GitHub, and Bitbucket.
Provide the necessary credentials to access your repository.

Configuring the Pipeline:

Blue Ocean will scan your repository and detect any existing Jenkinsfiles.
Use the visual pipeline editor to create a new pipeline if no Jenkinsfile is found.

Saving and Running the Pipeline:

Define the pipeline stages and steps.
Save the pipeline configuration.
Run the pipeline.

Pipeline Dashboard:
View the progress and status of the pipeline.
Real-time pipeline status updates.
Detailed information about stage and step execution.
Pipeline run history.


Troubleshooting and Debugging:
Identify the stage or step where the failure occurred.
View associated logs and take necessary actions to resolve the problem.
Best Practices for Pipeline Creation and Visualization:
Keep pipeline stages and steps concise and focused.
Use meaningful names for stages and steps.
Leverage the visual pipeline editor.
Regularly review and update pipelines.
Monitor pipeline status and address any failures promptly.



## Types of Pipelines:
1. **Declarative Pipeline**: Structured approach using a domain-specific language (DSL).
2. **Scripted Pipeline**: Flexible Groovy-based DSL for full control over the pipeline.

## Example: Deploy Application to Kubernetes

Here’s a simple pipeline definition for deploying an application to Kubernetes:

Prerequisites:
Jenkins is set up and running.
Kubernetes cluster is running.
Docker installed on the Jenkins node.
Jenkins has access to the Kubernetes cluster.
Docker registry credentials configured in Jenkins.


### Declarative Pipeline Example:
```groovy
pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'wblll-front-enddd19'
        DOCKER_TAG = 'latest'
        REGISTRY = 'docker.io'
        IMAGE_NAME = 'remote123/whiteboxlearning'
        KUBERNETES_CLUSTER_CONTEXT = 'cliuser-k8s'
        KUBERNETES_NAMESPACE = 'whiteboxlearning'
        GIT_REPO_URL = 'https://github.com/WhiteboxHub/whiteboxLearning-wbl.git'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: "${GIT_REPO_URL}"
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }
        stage('Push Docker Image') {
            steps {
                sh "docker push ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh "kubectl set image deployment/frontend ${IMAGE_NAME}=${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
                sh "kubectl rollout status deployment/frontend"
            }
        }
    }
}


Scripted Pipeline Example:

node {
    def DOCKER_IMAGE = 'wblll-front-enddd19'
    def DOCKER_TAG = 'latest'
    def REGISTRY = 'docker.io'
    def IMAGE_NAME = 'remote123/whiteboxlearning'
    def KUBERNETES_CLUSTER_CONTEXT = 'cliuser-k8s'
    def KUBERNETES_NAMESPACE = 'whiteboxlearning'
    def GIT_REPO_URL = 'https://github.com/WhiteboxHub/whiteboxLearning-wbl.git'

    try {
        stage('Checkout') {
            checkout scm
        }
        stage('Build Docker Image') {
            sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
        }
        stage('Push Docker Image') {
            sh "docker push ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
        }
        stage('Deploy to Kubernetes') {
            sh "kubectl set image deployment/frontend ${IMAGE_NAME}=${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    } finally {
        if (currentBuild.result == 'SUCCESS') {
            echo 'Deployment was successful!'
        } else {
            echo 'Something went wrong.'
        }
    }
}