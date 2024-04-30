# Introduction

This repository hosts a `docker-compose.yml` to facilitate the deployment of Zabbix using Docker. This setup leverages the official Zabbix Docker images for both the Zabbix server with PostgreSQL database support and the Zabbix frontend with Nginx. For more details on Zabbix Docker configurations, visit the [Zabbix official Docker guide](https://www.zabbix.com/documentation/current/manual/installation/containers).

## Repository Contents

This repository includes:

- **Docker Compose File**: A `docker-compose.yml` that orchestrates the setup of Zabbix server, web frontend, and a PostgreSQL database. Highlights include:
  - **Environment Customization**: Utilizes a `.env` file to configure environment variables for database connections.
  - **Persistent Data Storage**: Configures a Docker volume `postgres-data` mapped to `/var/lib/postgresql/data` to ensure data persistence across container restarts.

- **.env File**: Centralizes environment variable definitions to streamline your configuration process. You are encouraged to update the database credentials in this file to match your security requirements.

## Getting Started

### Important Preliminary Steps

Before deploying, please review and adjust the following:

1. **Database Credentials**: Update the `POSTGRES_USER`, `POSTGRES_PASSWORD`, and `POSTGRES_DB` in the `.env` file to secure your database access.

2. **Port Mapping Configuration**:
   - The `zabbix-server` is configured to be accessible from any network interface on the host (`0.0.0.0:10051`), allowing it to receive data from networked Zabbix agents.
   - The `zabbix-web` service is initially set to only be accessible locally (`127.0.0.1:10050:8080`). If you need to access the web interface from other machines on the network or externally, consider changing the binding to `0.0.0.0:10050:8080` to allow connections from any network interface.

3. **Optional: External Database**: If you prefer to use an existing PostgreSQL instance rather than the containerized version, remove the `postgres-zabbix` service from the `docker-compose.yml` and update the `DB_SERVER_HOST` environment variable in the Zabbix server and web services to point to your database host.

### Quick Setup

1. **Clone the Repository**:
   Clone this repository to your local machine using:
   ```bash
   git clone https://github.com/ramuyk/docker-zabbix.git
   cd docker-zabbix
   ```

2. **Launch Services**:
   Deploy your Zabbix stack using Docker Compose:
   ```bash
   docker-compose up -d
   ```

3. **Access Zabbix**:
   Open your web browser and navigate to `http://localhost:10050` to access the Zabbix web interface. Default admin login credentials:
   - **Username**: Admin
   - **Password**: zabbix

   It is highly recommended to change the default password immediately after your first login for security purposes.

