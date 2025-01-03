<!-- # Install Jenkins using Docker Compose

This repository contains a Docker Compose configuration for a quick installation of Jenkins. This setup is not intended for production systems.

Credits: This approach is mostly based on the [offical instructions](https://www.jenkins.io/doc/book/installing/docker/) but takes advantage of Docker Compose (by using a `docker-compose.yml` file) to reduce the number of steps needed to get Jenkins up and running.

# Docker Installation

## Step 1

Install Docker locally (probably using Docker Desktop is the easiest approach).

## Step 2

Clone this repository or download it's contents. 

## Step 2

Open a terminal window in the same directory where the `Dockerfile` from this repository is located. Build the Jenkins Docker image:

```
docker build -t my-jenkins .
```

## Step 3

Start Jenkins:

```
docker compose up -d
```

## Step 4

Open Jenkins by going to: [http://localhost:8080/](http://localhost:8080/) and finish the installation process.

## Step 5

If you wish to stop Jenkins and get back to it later, run:

```
docker compose down
```

If you wish to start Jenkins again later, just run the same comand from Step 3.


# Removing Jenkins

Once you are done playing with Jenkins maybe it is time to clean things up.

Run the following comand to terminate Jenkins and to remove all volumes and images used:

```
docker compose down --volumes --rmi all 
``` -->


# Install Jenkins Using Docker Compose

This guide provides a step-by-step approach for installing Jenkins using Docker Compose. The setup is ideal for local environments and is not intended for production systems.

---

## **Step 1: Install Docker**

1. **Update your system's package index**:
   ```
   sudo apt update
    ```

    Install Docker:
    ```
   sudo apt install -y docker.io
   ```

   Start and enable Docker:

   ```sh
    sudo systemctl start docker
    sudo systemctl enable docker
    ``` 

    Verify Docker installation:

    ```sh
    docker --version
    ```

    Alternatively, you can install Docker Desktop for Windows or macOS:

    ```sh
   	Docker Desktop Installation
    ```
## **Step 2:  Install Docker Compose**

    If Docker Compose is not already installed, follow these steps:
	1.Download Docker Compose:
    sudo curl -L 

```bash
    "https://github.com/docker/compose/releases/download/v2.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

	2.Apply executable permissions:
```bash
    sudo chmod +x /usr/local/bin/docker-compose
```

    3.Verify Docker Compose installation:
```bash 
    docker-compose --version
    ```

## ** Step 3: Clone the Repository **

    Clone or download the contents of the repository containing the Dockerfile and docker-compose.yml files.

    For example:
```bash
    git clone https://github.com/WhiteboxHub/whiteboxLearning-wbl.git 
```
 ## **Step 4: Build the Jenkins Docker Image**

    In the directory where the Dockerfile is located, build the Docker image for Jenkins:
```bash
    docker build -t my-jenkins .
```
 ## **Step 5: Start Jenkins**

    Run the following command to start Jenkins using Docker Compose:
```bash
    docker compose up -d
```
    This command:
	•	Starts Jenkins in detached mode (background).
	•	Maps Jenkins to port 8080 (web interface) and port 50000 (agent communication).


 ## **Step 6: Access Jenkins**
	1.	Open your browser and go to:
    http://localhost:8080/
	2.	Follow the installation steps:
	•	Unlock Jenkins: Run this command to get the initial admin password:
```bash
     docker exec my-jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```
    Copy the password and paste it into the UI.

	•	Install Plugins: Select “Install Suggested Plugins” or customize the installation.
	•	Create an Admin User: Fill in your details and save.

	3.	Once completed, you will be redirected to the Jenkins dashboard.


## **Step 7: Stopping and Restarting Jenkins**

    Stopping Jenkins
    To stop Jenkins and free up resources, run:
```bash
     docker compose down
```
- **Restarting Jenkins**:
     To restart Jenkins later, use:
```bash 
     docker compose up -d
```  
     
## **Step 8: Removing Jenkins** 

    If you’re done with Jenkins and wish to remove all data, images, and containers, run:

    docker compose down --volumes --rmi all

- **This command will**:
	•	Stop the Jenkins container
	•	Remove all associated volumes (data)
	•	Remove all Docker images built for Jenkins

- **Important Notes**:
	•	Data Persistence: Jenkins stores all configurations and jobs in the volume jenkins_home. Removing volumes will delete this data permanently.
	•	Port Usage: Ensure port 8080 is not in use by other applications before starting Jenkins.






