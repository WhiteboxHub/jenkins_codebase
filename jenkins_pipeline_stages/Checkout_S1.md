
## Jenkins Pipeline - Checkout

```groovy
stages {
    stage('Checkout') {
        steps {
            // Pull code from GitHub
            git url: "${GIT_REPO_URL}"
        }
    }
}


# Checout Stage 

This stage fetches the code from the GitHub repository to ensure the pipeline works with the latest version of the application code.

# Checkout Stage 


## Purpose
The purpose of the Checkout stage is to pull the latest version of the code from the specified GitHub repository. This ensures that the pipeline operates on the most up-to-date source code.

## Implementation
- The `git` step is used to clone the repository:
  ```groovy
  git url: "${https://github.com/WhiteboxHub/whiteboxLearning-wbl.git}"

•	The repository URL is defined as an environment variable for maintainability.

Key Considerations

•	Ensure that the Jenkins agent has network access to GitHub.
•	Ensure that the Jenkins agent has network access to GitHub.
•	If the repository is private, make sure appropriate credentials are configured in Jenkins.