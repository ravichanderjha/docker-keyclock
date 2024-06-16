# Keycloak Installation with Docker

## Docker Run

### Installation Steps:

1. Pull the Keycloak Docker image if not already available locally:
   ```bash
   docker run -p 3001:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:25.0.0 start-dev
   ```

   - `docker run`: Command to start a Docker container.
   - `-p 3001:8080`: Maps port 8080 of the container to port 3001 on the host.
   - `-e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin`: Sets environment variables for Keycloak admin username and password.
   - `quay.io/keycloak/keycloak:25.0.0`: Docker image repository and tag for Keycloak version 25.0.0.
   - `start-dev`: Command passed to Keycloak to start in development mode.

2. Access Keycloak at http://localhost:3001.

### Explanation:

- This command initializes a Keycloak container named `keycloak` and exposes it on port 3001.
- The environment variables `KEYCLOAK_ADMIN` and `KEYCLOAK_ADMIN_PASSWORD` are crucial for initial admin login credentials.
- `start-dev` starts Keycloak in development mode, suitable for testing and development environments.

## Docker Compose

### Installation Steps:

1. Create a `docker-compose.yml` file with the following content:

   ```yaml
   version: '3.8'

   services:
     keycloak:
       image: quay.io/keycloak/keycloak:25.0.0
       container_name: keycloak
       environment:
         - KEYCLOAK_ADMIN=admin
         - KEYCLOAK_ADMIN_PASSWORD=admin
       ports:
         - "3001:8080"
       command: ["start-dev"]
   ```

   - `version: '3.8'`: Specifies the Docker Compose file format version.
   - `services`: Defines the services to be run, in this case, just one service named `keycloak`.
   - `image: quay.io/keycloak/keycloak:25.0.0`: Specifies the Docker image to use.
   - `container_name: keycloak`: Names the container as `keycloak`.
   - `environment`: Sets environment variables within the container.
   - `ports: - "3001:8080"`: Maps port 8080 of the container to port 3001 on the host.
   - `command: ["start-dev"]`: Specifies the command to run within the container (start-dev for development mode).

2. Run Keycloak using Docker Compose:
   ```bash
   docker-compose up -d
   ```

3. Access Keycloak at http://localhost:3001.

### Explanation:

- Docker Compose simplifies container orchestration by allowing you to define and manage multi-container Docker applications with a single YAML file (`docker-compose.yml`).
- The `keycloak` service defined in this file uses the Keycloak image (`quay.io/keycloak/keycloak:25.0.0`), sets the admin username and password via environment variables, and exposes Keycloak on port 3001.
- `command: ["start-dev"]` instructs Keycloak to start in development mode, similar to the Docker run command.

## Summary

Using Docker or Docker Compose to run Keycloak provides an easy and efficient way to deploy and manage the identity and access management solution in a containerized environment. Docker Compose, with its YAML-based configuration, offers additional benefits such as easier scaling and network configuration for more complex setups.

---

Feel free to adjust the instructions or details based on your specific environment or requirements.