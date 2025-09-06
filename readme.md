# Laravel Docker Starting Kit

A reusable Docker setup for Laravel projects with PHP 8.4, Nginx, and all essential PHP extensions pre-configured.

## �� Features

- **PHP 8.4** with FPM
- **Nginx** web server
- **Composer** pre-installed
- **Essential PHP Extensions** for Laravel:
  - PDO MySQL
  - GD (with JPEG and FreeType support)
  - BCMath, PCNTL, OPCache
  - cURL, GMP
  - SOAP
  - Redis and MongoDB extensions
  - Intl, MBString
  - And more Laravel-required extensions

## 📋 Prerequisites

- Docker
- Docker Compose
- Git

## ��️ Quick Start

### 1. Clone and Setup

```bash
# Clone this repository or copy the files to your project
git clone <your-repo-url>

# Create environment file
cp .env.example .env
```

### 2. Configure Environment

Create a `.env` file in the root directory with the following variables:

```env
CONTAINER_NAME=laravel-app
CONTAINER_PORT=8000
```

### 3. Start the Container

```bash
# Build and start the container
docker-compose up -d --build
```

### 4. Install Laravel

Once the container is running, install Laravel using Composer:

```bash
# Access the container
docker-compose exec app bash

# Install Laravel (choose one method)
# Method 1: Create new Laravel project
composer create-project laravel/laravel .

# Method 2: If you have an existing Laravel project, just install dependencies
composer install
```

### 5. Configure Laravel

```bash
# Set proper permissions
chown -R www-data:www-data /var/www
chmod -R 755 /var/www/storage
chmod -R 755 /var/www/bootstrap/cache
```
