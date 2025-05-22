# Ghost CMS with Docker Compose

This project sets up a Ghost CMS using Docker Compose. It includes a MySQL database and the Ghost CMS application.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

### 1. Clone the repository

```bash
git clone git@github.com:flexyfile/panel.git
cd panel
```

### 2. Set up environment variables

Create a `.env.local` file based on the `.env.example` file and configure the necessary environment variables.

```bash
cp .env.example .env.local
```

Edit the `.env.local` file to set the appropriate values:

```bash
NODE_ENV=development
GHOST_HOST=http://localhost:2368
# Database configuration (use environment variables for sensitive data)
MYSQL_ROOT_PASSWORD=
MYSQL_DATABASE=
MYSQL_USER=
MYSQL_PASSWORD=
```

### 3. Start the services

```bash
docker-compose up -d
```

### 4. Access the Ghost CMS

Open your web browser and navigate to `http://localhost:2368` to access the Ghost CMS. You can also access the admin panel at `http://localhost:2368/ghost`.

### 5. Stop the services

To stop the services, run:

```bash
docker-compose down
```

### 6. Backup and Restore

To backup the Ghost CMS data, you can use the following command:

```bash
docker-compose exec ghost tar -czf /var/lib/ghost/ghost-backup.tar.gz /var/lib/ghost/content
```

### 7. Configuration

The docker-compose.yml file defines the services, networks, and volumes for the Ghost CMS application.

MySQL: The MySQL service uses the mysql:8.0 image and sets up the database environment.
Ghost CMS: The Ghost CMS service uses the ghost:5-alpine image and connects to the MySQL database.
Environment Variables
The following environment variables are used to configure the Ghost CMS:

- `NODE_ENV:` The environment in which the application is running (development or production).
- `GHOST_HOST:` The URL of the Ghost CMS
- `GHOST_DB_HOST:` The hostname of the MySQL database.
- `GHOST_DB_USER:` The username for the MySQL database.
- `GHOST_DB_PASSWORD:` The password for the MySQL database.
- `GHOST_DB_NAME:` The name of the MySQL database.
- `GHOST_ADMIN_EMAIL:` The email address for the Ghost CMS admin user.

Volumes
The following volumes are used to persist data:

- `db:` Stores the MySQL database data.
- `ghost_data:` Stores the Ghost CMS content.

## Security

Sensitive information such as database passwords should be stored in environment variables or Docker secrets, not directly in the docker-compose.yml file.
Ensure that the .env.local file is added to .gitignore to prevent it from being committed to the repository.
