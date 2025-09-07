# Application Web Server Creation

A docker-compose.yml file can be created to deploy a WordPress environment with Nginx and MariaDB using Docker Compose. This setup involves three services: wordpress, nginx, and mariadb.

1. Directory Structure:
```
.
├── docker-compose.yml
├── nginx.conf
└── www/
    └── (WordPress files will go here)
```

2. docker-compose.yml:
```
version: '1.0'

services:
  wordpress:
    image: wordpress:fpm-alpine # Using FPM-Alpine for a smaller image
    restart: always
    environment:
      WORDPRESS_DB_HOST: mariadb
      WORDPRESS_DB_NAME: wordpress_db
      WORDPRESS_DB_USER: wordpress_user
      WORDPRESS_DB_PASSWORD: your_db_password # Replace with a strong password
    volumes:
      - ./www/:/var/www/html/
    depends_on:
      - mariadb

  nginx:
    image: nginx:stable-alpine # Using Alpine for a smaller image
    restart: always
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf # Custom Nginx config
    depends_on:
      - wordpress

  mariadb:
    image: mariadb:latest
    restart: always
    environment:
      MARIADB_ROOT_PASSWORD: your_root_password # Replace with a strong password
      MARIADB_DATABASE: wordpress_db
      MARIADB_USER: wordpress_user
      MARIADB_PASSWORD: your_db_password # Replace with a strong password
    volumes:
      - db_data:/var/lib/mysql # Persistent storage for database data

volumes:
  db_data: # Define a named volume for MariaDB data
```

3. nginx.conf:
```
server {
    listen 80;
    server_name localhost; # Or your domain name

    root /var/www/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass wordpress:9000; # Connect to the WordPress FPM service
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

4. WordPress Files:
Download the latest WordPress archive from wordpress.org and extract its contents into the www directory.

5. Running the Setup:
Navigate to the directory containing docker-compose.yml in your terminal and execute:
```
docker-compose up -d
```

This command will build and start the services in detached mode. Once the containers are running, you can access your WordPress site by navigating to http://localhost in your web browser and completing the WordPress installation. 
