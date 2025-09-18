# Laravel Docker Starter Kit

A reusable Docker setup for Laravel projects with **PHP 8.4**, **Nginx**, and all essential PHP extensions pre-configured.


> ⚠️ **Note:**  
> This container only includes the dependencies required to run Laravel or any PHP application.  
> You can modify the Dockerfile to fit your needs.  
> The goal is to keep it lightweight for quickly running Laravel/PHP applications, especially APIs without a frontend, and to make deployment on **AWS EC2** or **AWS Fargate**, using **AWS ECS**.

---

## 📌 Roadmap (TODO)

- Separate Dockerfiles for production deployment:
  - One for serving APIs
  - One for running the scheduler
  - One for running Horizon

---

## ✨ Features

- **PHP 8.4** with FPM
- **Nginx** web server
- **Composer** pre-installed
- **Essential PHP Extensions** for Laravel:
  - PDO MySQL
  - GD (with JPEG and FreeType support)
  - BCMath, PCNTL, OPCache
  - cURL, GMP
  - SOAP
  - Redis and MongoDB
  - Intl, MBString
  - And more required extensions

---

## 📋 Prerequisites

- Docker
- Docker Compose
- Git

---

## 🚀 Quick Start

### 1. Clone and Setup

```bash
# Clone this repository or copy the files to your project
git clone <your-repo-url>
```

### 2. Configure Environment

Set port for container docker-compose.yml:

```yaml
ports:
      - "8000:80"
```

### 3. Start the Container

```bash
# Build and start the container
docker compose up -d --build
```

### 4. Install Laravel

Once the container is running, install Laravel using Composer:

```bash
# Access the container
docker compose exec app bash

# Install Laravel (choose one method)
# Method 1: Create new Laravel project
composer create-project laravel/laravel .

# Method 2: If you have an existing Laravel project, just install dependencies
composer install
```

### 5. Fix Laravel Permissions (if needed)

```bash
# Set proper permissions
chown -R www-data:www-data /var/www
chmod -R 755 /var/www/storage
chmod -R 755 /var/www/bootstrap/cache
```

## Changing php version 

If you want to use PHP 8.3 instead of 8.4, update the `.docker/Dockerfile`:
```dockerfile
# From this
FROM php:8.4-fpm-alpine

# To this
FROM php:8.3-fpm-alpine
```

## Run Other PHP Applications

- Copy your code into the `src` folder at the project root.
- Update the Nginx config in `.docker/nginx/nginx.conf` depending on where your `index.php` is located:

```nginx
# If your index.php is inside a public folder
root /var/www/public;

# If your index.php is directly inside src/
root /var/www;
```

---

## Run Artisan or Other Commands from App Root

To run `php artisan` commands or any other commands from the app root:
```bash
# Access the container shell
docker compose exec app bash
```

```bash
# Run artisan or other commands inside the container
php artisan migrate
php artisan config:cache
composer update
```