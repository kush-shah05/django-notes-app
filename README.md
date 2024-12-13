# Django App Deployment Automation

This repository contains a bash script, `deploy_django_app.sh`, which automates the deployment of a Django application. It simplifies the setup process by managing code cloning, dependency installation, system configurations, and Docker-based deployment.

---

## Features

- **Code Cloning**: Automatically clones the Django app from a GitHub repository if not already present.
- **Dependency Management**: Installs essential dependencies, including Docker, Nginx, and Docker Compose.
- **Error Handling**: Handles errors at every step to ensure a reliable deployment process.
- **Dockerized Deployment**: Builds and deploys the Django app using Docker and Docker Compose.
- **System Configuration**: Configures permissions and ensures services like Docker and Nginx are ready for use.

---

## Prerequisites

Before running the script, ensure you have the following:
1. A machine running Ubuntu (or a compatible Linux distribution).
2. Root or sudo access for installing packages and configuring services.
3. Network access to clone the GitHub repository and download dependencies.

---

## How to Use

1. **Clone this Repository**:
   ```bash
   git clone https://github.com/<your-repo-name>.git
   cd <your-repo-name>
   ```

2. **Make the Script Executable**:
   ```bash
   chmod +x deploy_django_app.sh
   ```

3. **Run the Script**:
   ```bash
   ./deploy_django_app.sh
   ```

4. **Verify Deployment**:
   - Check Docker containers to ensure the app is running:
     ```bash
     docker ps
     ```
   - Access the app in your browser using the public IP or localhost on the specified port (default: 8000).

---

## Script Overview

### Functions in the Script:

1. **`code_clone`**:
   - Clones the Django app from the repository `https://github.com/LondheShubham153/django-notes-app.git`.
   - Skips cloning if the directory already exists.

2. **`install_requirements`**:
   - Installs Docker, Docker Compose, and Nginx.

3. **`required_restarts`**:
   - Configures Docker permissions (`docker.sock`) for the current user.

4. **`deploy`**:
   - Builds the Docker image for the Django app.
   - Deploys the app using Docker Compose.

5. **Error Handling**:
   - Stops execution on errors with meaningful messages.
   - Includes a placeholder for notifying admins via email in case of deployment failure.

---

## Deployment Details

- **Dependencies Installed**:
  - Docker
  - Docker Compose
  - Nginx
- **Deployment Method**:
  - Builds a Docker image using the `Dockerfile` in the project.
  - Starts the app using `docker-compose.yml`.

---

## Troubleshooting

- **Permissions Error**:
  Ensure the current user has appropriate permissions for `docker.sock`:
  ```bash
  sudo chown $USER /var/run/docker.sock
  ```

- **Failed Dependency Installation**:
  Re-run the script or manually install dependencies:
  ```bash
  sudo apt-get update && sudo apt-get install -y docker.io nginx docker-compose
  ```

- **App Not Running**:
  Check Docker logs:
  ```bash
  docker logs <container-id>
  ```

---

## Future Enhancements

- Add support for multiple environments (e.g., dev, staging, production).
- Implement email or Slack notifications for deployment failures.
- Include automated SSL certificate configuration using Let's Encrypt.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Author

**Your Name**  
[GitHub Profile](https://github.com/<kush-shah05>)
