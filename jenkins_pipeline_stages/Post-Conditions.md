# **`Post-Conditions.md`**

## Jenkins Pipeline - Post Actions

```groovy
post {
    success {
        echo 'Deployment to Kubernetes was successful!'
    }
    failure {
        echo 'Something went wrong during the deployment.'
    }
}
```

## **Description:**
This section outlines actions taken after the pipeline execution, whether it succeeds or fails.

## Purpose
Post conditions define the steps to execute after the pipeline run, depending on the outcome (success or failure).

## Implementation
- If the pipeline succeeds:
  ```groovy
  echo 'Deployment to Kubernetes was successful!'
  	
•	If the pipeline fails:
  echo 'Something went wrong during the deployment.'

## **Key Considerations**
-	Ensure that notifications or additional actions (e.g., sending emails or Slack messages) are configured in this section as needed.
- Logs from each stage can be reviewed to diagnose failures.
