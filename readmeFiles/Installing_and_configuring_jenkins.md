# Installing and Configuring Jenkins

## Installation

You can install Jenkins on various platforms like:
- **Windows**
- **macOS**
- **Linux**
- **Docker**

### Installation Steps:
1. Install using `.war` file or system packages.
2. Start Jenkins server.

### Configuration:
- Initial Admin setup.
- Managing users and roles.
- Plugin installation to extend Jenkins functionality.

After installation, you can access Jenkins at `http://localhost:8080`.

## Setup Jenkins with Docker

Before starting Jenkins setup, ensure that Docker is installed on your system.

### Validate Docker Setup:
Run the following commands:
```bash
docker --version
```
```bash
docker-compose --help
```

Launch Jenkins Container:
docker-compose up -d


Access Jenkins:
```bash
Visit http://IPADDRESS:8080 to access Jenkins UI.
```

Fetch Initial Admin Password:
docker-compose logs jenkins
Copy the password from the logs and paste it into the UI to unlock Jenkins.


User Setup:
Once logged in, create an admin user and finish the configuration steps.

Stopping, Starting, and Resetting Jenkins
To stop Jenkins: docker-compose down

To restart Jenkins: docker-compose up -d

To reset the environment, delete the volumes: docker-compose down -v

This removes volumes shared between Jenkins and Docker, resetting the environment.