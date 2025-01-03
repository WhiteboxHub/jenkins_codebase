pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'wblll-front-enddd19'  // Docker image name
        DOCKER_TAG = 'latest'  // Docker tag
        REGISTRY = 'docker.io'  // Docker registry (Docker Hub in this case)
        IMAGE_NAME = 'remote123/whiteboxlearning'  // Docker Hub image name
        KUBERNETES_CLUSTER_CONTEXT = 'cliuser-k8s'  // Kubernetes context name
        KUBERNETES_NAMESPACE = 'whiteboxlearning'  // Kubernetes namespace
        GIT_REPO_URL = 'https://github.com/WhiteboxHub/whiteboxLearning-wbl.git'  // GitHub repo URL
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git url: "${GIT_REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    // Tag the Docker image with the full registry name
                    sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"  // You need to configure these Jenkins credentials

                    // Push the Docker image to Docker Hub
                    sh "docker push ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
                }
            }
        }

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
    }

    post {
        success {
            echo 'Deployment to Kubernetes was successful!'
        }
        failure {
            echo 'Something went wrong during the deployment.'
        }
    }
}



// scripted pipeline 

node {
    // Define environment variables
    def DOCKER_IMAGE = 'wblll-front-enddd19'
    def DOCKER_TAG = 'latest'
    def REGISTRY = 'docker.io'
    def IMAGE_NAME = 'remote123/whiteboxlearning'
    def KUBERNETES_CLUSTER_CONTEXT = 'cliuser-k8s'
    def KUBERNETES_NAMESPACE = 'whiteboxlearning'
    def GIT_REPO_URL = 'https://github.com/WhiteboxHub/whiteboxLearning-wbl.git'

    try {
        
        stage('Checkout') {
            // Pull code from GitHub
            checkout scm
        }

        stage('Build Docker Image') {
            // Build the Docker image
            sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
        }

        stage('Tag Docker Image') {
            // Tag the Docker image with the full registry name
            sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
        }

        stage('Push Docker Image') {
            // Log in to Docker Hub
            sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"

            // Push the Docker image to Docker Hub
            sh "docker push ${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG}"
        }

        stage('Deploy to Kubernetes') {
            // Set the Kubernetes context
            sh "kubectl config use-context ${KUBERNETES_CLUSTER_CONTEXT}"

            // Deploy the new Docker image to Kubernetes using kubectl
            sh """
                kubectl set image deployment/frontend ${IMAGE_NAME}=${REGISTRY}/${IMAGE_NAME}:${DOCKER_TAG} --namespace=${KUBERNETES_NAMESPACE}
                kubectl rollout status deployment/frontend --namespace=${KUBERNETES_NAMESPACE}
            """
        }

    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    } finally {
        if (currentBuild.result == 'SUCCESS') {
            echo 'Deployment to Kubernetes was successful!'
        } else {
            echo 'Something went wrong during the deployment.'
        }
    }
}
