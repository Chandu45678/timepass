Prerequisites

Make sure you have the following installed:

 Docker

 Docker Compose (or Docker with docker compose support)

 Internet connection (to pull Docker images)

You can verify installation:

docker --version
docker compose version   # or: docker-compose --version

Project Structure

We will create a simple project folder like this:

wordpress-mysql/
└── docker-compose.yml


All our configuration will be inside docker-compose.yml.

Step 1: Create Project Directory

Open a terminal (Command Prompt, PowerShell, or Linux terminal) and run:

mkdir wordpress-mysql
cd wordpress-mysql


This will:

Create a folder named wordpress-mysql.

Move you inside that folder.

Step 2: Create docker-compose.yml

Inside the wordpress-mysql folder, create a file named:

docker-compose.yml


You can create and edit this file using:

Notepad (Windows)

VS Code

nano/vim (Linux/macOS)

Paste the following content into docker-compose.yml:

version: '3.8'

services:
  db:
    image: mysql:5.7
    container_name: wp-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wp-app
    restart: always
    ports:
      - "5050:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

volumes:
  mysql_data:


💡 You can change the passwords and database name if you like, but they must match between the db and wordpress services.

Step 3: Docker Compose File Explained

Let’s break down what the docker-compose.yml is doing.

3.1 db Service (MySQL)
db:
  image: mysql:5.7
  container_name: wp-mysql
  restart: always
  environment:
    MYSQL_ROOT_PASSWORD: rootpass
    MYSQL_DATABASE: wordpress
    MYSQL_USER: wpuser
    MYSQL_PASSWORD: wppass
  volumes:
    - mysql_data:/var/lib/mysql


image: Uses the official mysql:5.7 image.

container_name: Names the container wp-mysql.

environment:

MYSQL_ROOT_PASSWORD: Root password for MySQL.

MYSQL_DATABASE: Database name to be created (here: wordpress).

MYSQL_USER and MYSQL_PASSWORD: A non-root user for the database.

volumes:

mysql_data:/var/lib/mysql → Persists MySQL data in a named Docker volume so data survives container restarts.

3.2 wordpress Service
wordpress:
  image: wordpress:latest
  container_name: wp-app
  restart: always
  ports:
    - "5050:80"
  environment:
    WORDPRESS_DB_HOST: db:3306
    WORDPRESS_DB_USER: wpuser
    WORDPRESS_DB_PASSWORD: wppass
    WORDPRESS_DB_NAME: wordpress
  depends_on:
    - db


image: Uses the latest official wordpress image.

container_name: Names the container wp-app.

ports:

"5050:80" maps:

container port 80 → host port 5050

You will access WordPress at http://localhost:5050.

environment:

Tells WordPress how to connect to MySQL:

WORDPRESS_DB_HOST: db:3306 → service name db (internal Docker network) and MySQL port.

WORDPRESS_DB_USER: Same as MYSQL_USER.

WORDPRESS_DB_PASSWORD: Same as MYSQL_PASSWORD.

WORDPRESS_DB_NAME: Same as MYSQL_DATABASE.

depends_on:

Ensures that db (MySQL) starts before wordpress.

3.3 Volumes
volumes:
  mysql_data:


Defines a named volume called mysql_data.

Used to store MySQL data persistently.

Step 4: Start the Containers

In the wordpress-mysql directory (where docker-compose.yml resides), run:

docker compose up -d


Or, if your Docker uses the older syntax:

docker-compose up -d


up: Creates and starts the containers.

-d: Runs them in detached mode (in the background).

Docker will:

Pull the mysql:5.7 image (if not already present).

Pull the wordpress:latest image.

Create the wp-mysql and wp-app containers.

Create the mysql_data volume.

Step 5: Verify Container Status

To check if the containers are running:

docker ps


You should see something like:

A container named wp-mysql (MySQL)

A container named wp-app (WordPress)

If they are not running, check logs:

docker compose logs db
docker compose logs wordpress


(Or docker-compose logs ... depending on your system.)

Step 6: Access WordPress in Browser

Once containers are running, open your browser and visit:

http://localhost:5050


You should see the WordPress installation screen, something like:

Welcome to the famous five-minute WordPress installation process!
Please provide the following information...

If you see this page, your multi-container Docker setup is working correctly.

Step 7: Complete WordPress Installation

On the WordPress setup page, fill in the details:

Site Title

Example: My Docker WP Site or anything you like.

Username

This will be your admin login username.

Example: admin, bob, testuser.

Password

WordPress may generate a strong password automatically.

You can keep it or change it to something you remember.

Store it somewhere safe.

Your Email

Enter a valid email (used for password resets and notifications).

Search Engine Visibility (optional)

Option: "Discourage search engines from indexing this site".

For local development, this setting does not matter much.

Click the “Install WordPress” button.

If everything is correct, you will see a success message like:

Success! WordPress has been installed. Thank you, and enjoy!

Step 8: Log in to WordPress Admin Panel

After installation:

Go to the login page:

http://localhost:5050/wp-admin


Enter the Username and Password you configured earlier.

Click Log In.

You’ll now be inside the WordPress Dashboard where you can:

Create posts and pages.

Install themes and plugins.

Customize your site.

To view the front-end of your site (what visitors see), go to:

http://localhost:5050

Step 9: Stopping and Removing Containers
9.1 Stop Containers (But Keep Data)

To stop the running containers:

docker compose down


(or docker-compose down)

This will:

Stop and remove the containers.

Keep the mysql_data volume (your database is safe).

9.2 Stop Containers and Delete Data

If you also want to remove the volume (delete the database):

docker compose down -v


(or docker-compose down -v)

This will:

Stop containers.

Remove containers.

Remove the mysql_data volume (data will be lost).

Troubleshooting
1. Port Already in Use

If another service (like Tomcat) is using port 5050 or 8080, you may get an error or see a different app.

Either stop the other service/container, or

Change the port in docker-compose.yml:

ports:
  - "5050:80"   # Change 5050 to another host port if needed


Example:

ports:
  - "9000:80"


Then restart:

docker compose down
docker compose up -d


And access:

http://localhost:9000

2. WordPress Cannot Connect to Database

If you see errors like “Error establishing a database connection”:

Make sure WORDPRESS_DB_HOST matches the service name (db):

WORDPRESS_DB_HOST: db:3306


Ensure the environment variables in wordpress and db match:

MYSQL_DATABASE ↔ WORDPRESS_DB_NAME

MYSQL_USER ↔ WORDPRESS_DB_USER

MYSQL_PASSWORD ↔ WORDPRESS_DB_PASSWORD

Restart containers:

docker compose down
docker compose up -d

3. Containers Not Starting

Check logs:

docker compose logs db
docker compose logs wordpress


Look for:

Incorrect environment variables

Wrong image names

Permission errors

Summary

In this guide, we:

Created a project folder: wordpress-mysql.

Wrote a docker-compose.yml file defining:

A MySQL container (db service).

A WordPress container (wordpress service).

A named volume for MySQL data.

Started both containers with:

docker compose up -d


Accessed WordPress at:

http://localhost:5050


Completed the WordPress installation.

Logged into the WordPress admin dashboard.

Learned how to stop and remove containers and volumes.

Covered common troubleshooting tips.