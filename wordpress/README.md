# WordPress with MySQL Docker Setup

This guide will walk you through setting up WordPress and MySQL using Docker containers.

## Prerequisites

- Docker installed on your machine. You can download and install Docker from [here](https://www.docker.com/get-started).

### Run the following Docker command to start WordPress and MySQL containers

1. Launch MySQL Container:

Setting Variables
```bash
export mysql_root_password=redhat
export mysql_user=redhat
export mysql_password=redhat
export mysql_db=redhat
```

Use the docker run command to start a MySQL container. Make sure to specify a root password using the MYSQL_ROOT_PASSWORD environment variable and expose the MySQL port if you want to access it from outside the container.

```bash
docker run -itd --name mysql \
-e MYSQL_ROOT_PASSWORD=${mysql_root_password} \
-e MYSQL_USER=${mysql_user} \
-e MYSQL_PASSWORD=${mysql_password} \
-e MYSQL_DATABASE=${mysql_db} \
-p 3306:3306 mysql:5.7
```
2. Launch WordPress Container:

Use the docker run command to start a WordPress container. Link it to the MySQL container using the --link option and provide the necessary environment variables like WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD, and WORDPRESS_DB_NAME.

```bash
docker run -itd --name wordpress \
-e WORDPRESS_DB_HOST=mysql \
-e WORDPRESS_DB_USER=${mysql_user} \
-e WORDPRESS_DB_PASSWORD=${mysql_password} \
-e WORDPRESS_DB_NAME=${mysql_db} \
-p 8080:80 wordpress
```

3. Access WordPress
Once both containers are running, you can access WordPress by navigating to http://localhost:8080 in your web browser.


That's it! You've launched WordPress application with MySQL Database
