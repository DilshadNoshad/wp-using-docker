Here's a sample `README.md` for your Docker services setup, detailing the configuration for the MySQL database, phpMyAdmin, and WordPress:

```markdown
# Docker Setup for WordPress with MySQL and phpMyAdmin

This repository contains a Docker setup for running a WordPress application with a MySQL database and phpMyAdmin for database management. The setup allows you to easily spin up a development environment using Docker.

## Services Overview

### 1. MySQL Database

- **Image**: `mysql:8.0`
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`: Set to `wordpress`
  - `MYSQL_DATABASE`: Set to `wordpress`
  - `MYSQL_USER`: Set to `wordpress`
  - `MYSQL_PASSWORD`: Set to `wordpress`
- **Volume**: 
  - `./db_data:/var/lib/mysql` (Persistent storage for database data)
- **Restart Policy**: Always restart unless explicitly stopped.

### 2. phpMyAdmin

- **Image**: `phpmyadmin`
- **Depends on**: MySQL database (`db`)
- **Environment Variables**:
  - `PMA_HOST`: Set to `db` (MySQL service name)
  - `MYSQL_ROOT_PASSWORD`: Set to `wordpress`
- **Ports**:
  - `8084:80` (Access phpMyAdmin at `http://localhost:8084`)
- **Restart Policy**: Always restart unless explicitly stopped.

### 3. WordPress

- **Image**: `wordpress:latest`
- **Depends on**: MySQL database (`db`)
- **Environment Variables**:
  - `WORDPRESS_DB_HOST`: Set to `db:3306` (MySQL host and port)
  - `WORDPRESS_DB_USER`: Set to `wordpress`
  - `WORDPRESS_DB_PASSWORD`: Set to `wordpress`
  - `WORDPRESS_DB_NAME`: Set to `wordpress`
- **Volumes**:
  - `./wp-content:/var/www/html/wp-content` (Persistent storage for WordPress content)
  - `./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini` (Configuration for file upload size and execution time)
- **Ports**:
  - `8083:80` (Access WordPress at `http://localhost:8083`)

## Getting Started

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/DilshadNoshad/wp-using-docker.git
   cd wp-using-docker
   ```

2. **Start the Services**:
   Use the following command to start all services in detached mode:
   ```bash
   docker-compose up -d
   ```

3. **Access the Applications**:
   - WordPress: [http://localhost:8083](http://localhost:8083)
   - phpMyAdmin: [http://localhost:8084](http://localhost:8084)

4. **Stopping the Services**:
   To stop the services, run:
   ```bash
   docker-compose down
   ```

## Notes

- The MySQL root password and user credentials are set to `wordpress`. Change these in a production environment for security.
- Persistent storage is configured to ensure your database and WordPress content are not lost when containers are restarted.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

```

### Explanation of Sections

- **Services Overview**: Describes each service, its purpose, and configuration details.
- **Getting Started**: Provides instructions on cloning the repository, starting the services, accessing the applications, and stopping them.
- **Notes**: Important considerations for security and data persistence.
- **License**: Indicates licensing information for the project.

Feel free to customize any part of the README to better fit your project's specifics!