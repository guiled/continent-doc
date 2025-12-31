---
layout: default
title: Installation Guide
---

# Installation Guide - Renaissance Project

This guide explains how to install and configure the Renaissance project locally for development.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Database Setup](#database-setup)
3. [Project Configuration](#project-configuration)
4. [Dependencies Installation](#dependencies-installation)
5. [Build Process](#build-process)
6. [Web Server Configuration](#web-server-configuration)
7. [Verification](#verification)
8. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Required Software

- **PHP**: Version 5.6.0 or higher
  - Required extensions:
    - `pdo_mysql` (MySQL PDO driver)
    - `mbstring` (Multibyte string support)
    - `json` (JSON support)
    - `gd` or `imagick` (Image processing, optional)
    - `zip` (For Composer)
    - `xml` (For Doctrine ORM)

- **MySQL**: Version 5.5 or higher
  - Database server running and accessible
  - User with CREATE, DROP, INSERT, UPDATE, DELETE, SELECT privileges

- **Composer**: PHP dependency manager
  - Download from: https://getcomposer.org/
  - Installation: `curl -sS https://getcomposer.org/installer | php`

- **Web Server**: Apache or Nginx
  - Apache with `mod_rewrite` enabled (recommended)
  - Or Nginx with proper rewrite rules

- **Node.js** (Optional): For CSS preprocessing if using Less.js
  - Version 6.0 or higher recommended

### Optional Tools

- **Phing**: PHP build tool (included via Composer)
- **Behat**: Behavior-driven testing (included via Composer)
- **Atoum**: Unit testing framework (included via Composer)

---

## Database Setup

### 1. Create Database

Create a MySQL database for the project:

```sql
CREATE DATABASE continent_renaissance_doctrine CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### 2. Create Database Users

Create users with appropriate privileges (see `database/user.sql` for reference):

```sql
-- User for general application access (read/write)
CREATE USER 'guest'@'localhost' IDENTIFIED BY 'your_password_here';
GRANT SELECT, INSERT, UPDATE, DELETE ON continent_renaissance_doctrine.* TO 'guest'@'localhost';

-- User for resolution process (full privileges)
CREATE USER 'resolution'@'localhost' IDENTIFIED BY 'your_resolution_password_here';
GRANT ALL PRIVILEGES ON continent_renaissance_doctrine.* TO 'resolution'@'localhost' WITH GRANT OPTION;
```

**Note**: Replace `your_password_here` and `your_resolution_password_here` with secure passwords.

### 3. Import Database Schema

The database schema is managed by Doctrine ORM. You can generate it using Doctrine CLI:

```bash
php cli.php orm:schema-tool:create
```

Or import the sample data:

```bash
mysql -u root -p continent_renaissance_doctrine < database/data.sql
```

**Note**: The `data.sql` file contains sample data. Use it for development/testing purposes only.

---

## Project Configuration

### 1. Copy Configuration Files

Several configuration files need to be created from sample files:

```bash
# Database connection configuration
cp php/Connection/AllPrivileges.sample.php php/Connection/AllPrivileges.php

# Core constants configuration
cp php/Core/constant.sample.php php/Core/constant.php

# Application configuration
cp configuration/configuration.sample.json configuration/configuration.json

# Behat testing configuration (optional)
cp php/Test/System/behat.sample.yml php/Test/System/behat.yml
```

### 2. Configure Database Connection

Edit `php/Connection/AllPrivileges.php`:

```php
<?php
namespace Blackhole\Continent\Connection;

class AllPrivileges extends Connection
{
    const HOST = 'localhost';  // Your MySQL host
    const DATABASE_NAME = 'continent_renaissance_doctrine';  // Your database name
    const USER = 'resolution';  // Database user with full privileges
    const PASSWORD = 'your_resolution_password_here';  // Database password
}
```

### 3. Configure Core Constants

Edit `php/Core/constant.php`:

```php
<?php
define('ROOT_PATH', str_replace('\\', '/', __DIR__) .'/../../');
define('HTTP_ROOT_PATH', rtrim(dirname($_SERVER['PHP_SELF']), '/') . '/');

const PRODUCTION_MODE = false;  // Set to true in production
const DEBUG_MODE = true && !PRODUCTION_MODE;
const USE_EPHEMERAL_SESSION = false && DEBUG_MODE;

date_default_timezone_set('Europe/Paris');  // Set your timezone
```

### 4. Configure Application Settings

Edit `configuration/configuration.json`:

```json
{
    "ANNEE_INITIALE": "600",
    "CYCLE_ACTUEL": "1",
    "NIVEAU_MAXIMUM_SCIENCE": "100",
    "NOMBRE_MAXIMUM_PEONS_PAR_TACHE_ET_PAR_CASE": "100",
    "NOMBRE_MINIMUM_PEONS_PAR_TACHE": "0",
    "NOMBRE_TOUR_PAR_CYCLE": "100",
    "NOMBRE_TYPES_SCIENCES_PAR_FACTION": "2",
    "RESOLUTION_EN_COURS": "0",
    "TAXE_MAXIMUM": "100",
    "TAXE_MINIMUM": "0",
    "TOUR_ACTUEL": "1",
    "TOUR_HIVER_FIN": "10"
}
```

Adjust these values according to your game configuration needs.

---

## Dependencies Installation

### 1. Install PHP Dependencies

Install all PHP dependencies using Composer:

```bash
composer install
```

This will install:
- Doctrine ORM and DBAL
- PHP-DI (Dependency Injection)
- Phing (Build tool)
- Behat (Testing framework)
- Atoum (Unit testing)
- Other required libraries

### 2. Verify Installation

Check that vendor directory was created:

```bash
ls -la vendor/
```

You should see directories like `doctrine/`, `php-di/`, `phing/`, etc.

---

## Build Process

### 1. Build Assets (Optional)

If you need to compile CSS or process JavaScript, use Phing:

```bash
# Build all assets
vendor/bin/phing

# Or build specific targets
vendor/bin/phing css
vendor/bin/phing javascript
```

**Note**: The project includes pre-compiled CSS files, so this step may not be necessary for basic setup.

### 2. Cache Directories

Ensure cache directories exist and are writable:

```bash
mkdir -p cache/dependencyInjection
mkdir -p cache/orm
mkdir -p cache/lastUpdateTime
chmod -R 775 cache/
```

### 3. Log Directories

Ensure log directories exist and are writable:

```bash
mkdir -p log/error
mkdir -p log/resolution
chmod -R 775 log/
```

---

## Web Server Configuration

### Apache Configuration

#### Option 1: Virtual Host (Recommended)

Create a virtual host configuration (e.g., `/etc/apache2/sites-available/renaissance.conf`):

```apache
<VirtualHost *:80>
    ServerName renaissance.local
    DocumentRoot /path/to/renaissance
    
    <Directory /path/to/renaissance>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    
    # PHP configuration
    php_admin_value upload_max_filesize 10M
    php_admin_value post_max_size 10M
    php_admin_value memory_limit 256M
    
    ErrorLog ${APACHE_LOG_DIR}/renaissance_error.log
    CustomLog ${APACHE_LOG_DIR}/renaissance_access.log combined
</VirtualHost>
```

Enable the site:

```bash
sudo a2ensite renaissance.conf
sudo systemctl reload apache2
```

Add to `/etc/hosts`:

```
127.0.0.1    renaissance.local
```

#### Option 2: Document Root

If using the project as document root, ensure `.htaccess` files are present:

- Root `.htaccess` (if needed)
- `php/.htaccess` (protects PHP files)
- `configuration/.htaccess` (protects configuration)
- `map/.htaccess` (protects map files)
- `log/.htaccess` (protects log files)

### Nginx Configuration

Example Nginx configuration:

```nginx
server {
    listen 80;
    server_name renaissance.local;
    root /path/to/renaissance;
    index htmlIndex.php;

    location / {
        try_files $uri $uri/ /htmlIndex.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_index htmlIndex.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    # Protect sensitive directories
    location ~ ^/(php|configuration|map|log|dump|cache)/ {
        deny all;
    }

    # Allow access to entry points
    location ~ ^/(htmlIndex|jsonIndex|cli)\.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

### PHP Built-in Server (Development Only)

For quick testing, you can use PHP's built-in server:

```bash
php -S localhost:8000 -t . htmlIndex.php
```

Access the application at: `http://localhost:8000`

**Warning**: This is for development only. Do not use in production.

---

## Verification

### 1. Check Database Connection

Test the database connection using Doctrine CLI:

```bash
php cli.php dbal:run-sql "SELECT 1"
```

If successful, you should see output confirming the connection.

### 2. Check Web Access

Open your browser and navigate to:

- `http://renaissance.local/` (or your configured URL)
- `http://localhost:8000/` (if using PHP built-in server)

You should see the application interface.

### 3. Check API Endpoints

Test JSON API endpoint:

```bash
curl http://renaissance.local/jsonIndex.php
```

### 4. Verify File Permissions

Ensure proper permissions:

```bash
# Cache directories
chmod -R 775 cache/

# Log directories
chmod -R 775 log/

# Map directory (if needed)
chmod -R 775 map/
```

---

## Directory Structure

Important directories and their purposes:

```
renaissance/
├── cache/              # Cache files (auto-generated)
│   ├── dependencyInjection/
│   ├── orm/
│   └── lastUpdateTime/
├── configuration/      # Configuration files
│   ├── configuration.json
│   ├── dependencyInjection.php
│   └── orm/           # Doctrine ORM mappings
├── database/          # Database scripts
│   ├── data.sql       # Sample data
│   └── user.sql       # User creation script
├── log/               # Log files
│   ├── error/
│   └── resolution/
├── map/               # Map binary files
├── php/               # PHP source code
│   ├── Connection/    # Database connections
│   ├── Core/          # Core utilities
│   ├── Entity/        # Doctrine entities
│   ├── Repository/    # Data repositories
│   ├── Service/       # Business logic services
│   └── Test/          # Tests
├── javascript/        # JavaScript/AngularJS code
├── css/               # CSS/Less stylesheets
├── view/              # HTML templates
├── image/             # Image assets
├── vendor/            # Composer dependencies
├── htmlIndex.php      # HTML entry point
├── jsonIndex.php      # JSON API entry point
└── cli.php            # CLI entry point (Doctrine commands)
```

---

## Development Workflow

### Running Tests

#### Unit Tests (Atoum)

```bash
vendor/bin/atoum
```

#### System Tests (Behat)

```bash
vendor/bin/behat
```

### Database Migrations

Doctrine ORM schema management:

```bash
# Generate schema from entities
php cli.php orm:schema-tool:update --dump-sql

# Apply schema changes
php cli.php orm:schema-tool:update --force

# Create schema from scratch
php cli.php orm:schema-tool:create
```

### Clearing Cache

Clear various caches:

```bash
# Clear dependency injection cache
rm -rf cache/dependencyInjection/*

# Clear ORM cache
rm -rf cache/orm/*

# Clear all caches
rm -rf cache/*
```

---

## Troubleshooting

### Common Issues

#### 1. Database Connection Errors

**Error**: `SQLSTATE[HY000] [2002] Connection refused`

**Solution**:
- Verify MySQL server is running: `sudo systemctl status mysql`
- Check connection credentials in `php/Connection/AllPrivileges.php`
- Verify database exists: `mysql -u root -p -e "SHOW DATABASES;"`

#### 2. Permission Denied Errors

**Error**: `Permission denied` when writing to cache/log directories

**Solution**:
```bash
chmod -R 775 cache/ log/
# Or change ownership
sudo chown -R www-data:www-data cache/ log/
```

#### 3. Composer Autoload Issues

**Error**: `Class not found` errors

**Solution**:
```bash
composer dump-autoload
```

#### 4. Doctrine ORM Errors

**Error**: Entity mapping errors

**Solution**:
- Verify ORM mapping files in `configuration/orm/`
- Clear ORM cache: `rm -rf cache/orm/*`
- Regenerate proxies: `php cli.php orm:generate-proxies`

#### 5. JavaScript/Angular Errors

**Error**: Angular modules not loading

**Solution**:
- Check browser console for errors
- Verify `javascript/Game/main.js` is loaded
- Check that all dependencies are included

#### 6. CSS Not Loading

**Error**: Styles not applied

**Solution**:
- Verify CSS files exist in expected locations
- Check web server configuration
- Rebuild CSS if using Less: `vendor/bin/phing css`

### Debug Mode

Enable debug mode in `php/Core/constant.php`:

```php
const PRODUCTION_MODE = false;
const DEBUG_MODE = true;
```

This will:
- Show detailed error messages
- Enable development logging
- Disable caching in some areas

### Log Files

Check log files for errors:

```bash
# Application errors
tail -f log/error/error.log

# Resolution process logs
tail -f log/resolution/resolution.log

# PHP error log (if configured)
tail -f /var/log/php_errors.log
```

---

## Production Deployment

### Security Checklist

Before deploying to production:

1. **Set Production Mode**:
   ```php
   const PRODUCTION_MODE = true;
   const DEBUG_MODE = false;
   ```

2. **Secure Configuration Files**:
   - Ensure `.htaccess` files protect sensitive directories
   - Verify `php/Connection/AllPrivileges.php` has correct permissions (600)
   - Never commit configuration files with real credentials

3. **Database Security**:
   - Use strong passwords
   - Limit database user privileges
   - Use separate users for application and resolution process

4. **File Permissions**:
   ```bash
   # Sensitive files
   chmod 600 php/Connection/AllPrivileges.php
   chmod 600 php/Core/constant.php
   chmod 600 configuration/configuration.json
   
   # Directories
   chmod 755 cache/ log/ map/
   ```

5. **Disable Directory Listing**:
   - Ensure `.htaccess` files prevent directory listing
   - Verify web server configuration

6. **Error Handling**:
   - Disable error display in production
   - Log errors to secure location
   - Don't expose stack traces to users

### Performance Optimization

1. **Enable OPcache** (PHP):
   ```ini
   opcache.enable=1
   opcache.memory_consumption=128
   ```

2. **Use Production Cache**:
   - Enable Doctrine query cache
   - Use filesystem cache for dependency injection
   - Enable browser caching for static assets

3. **Database Optimization**:
   - Add indexes as needed
   - Optimize queries
   - Use connection pooling

---

## Additional Resources

- **Documentation**: See `documentation/` directory
- **Doctrine ORM**: https://www.doctrine-project.org/
- **PHP-DI**: http://php-di.org/
- **Composer**: https://getcomposer.org/doc/
- **Phing**: https://www.phing.info/

---

## Support

For issues or questions:

1. Check the troubleshooting section above
2. Review log files for error messages
3. Check the documentation in `documentation/` directory
4. Review the original Continent project for reference implementations

---

*Last Updated: Based on project structure analysis*

