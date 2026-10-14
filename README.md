## Docker Compose Project Student ERP

Now we will setup database
Make database of Mariadb in AWS RDS
On our EC2 instance Jenkins-k8s do the installation for database
MariaDB Setup and Configuration Guide for Windows This guide explains how to set up MariaDB, create a database, and Create Database User

Installing MariaDB Installing MariaDB on Ubuntu
```sh
apt update && apt install mariadb-server -y
```


Securing MariaDB Open the Command Prompt as Administrator and run the following command to secure your installation:
mysql_secure_installation
Follow the prompts to: Set a root password. Remove insecure default users and test databases. Disable remote root login.

Setting Up the Database Open terminal and login to MariaDB:
```sh
mysql -h <rds endpoint > -uadmin -p 
Enter the root password when prompted.
```

Create a new database and user:
```sh
CREATE DATABASE student_db;
GRANT ALL PRIVILEGES ON springbackend.* TO 'username'@'localhost' IDENTIFIED BY 'your_password';
```

Replace username and your_password with your desired username and password.

You will need Database Credentials to Connect Backend with Database
DB_HOST
DB_USER
DB_PASS
DB_PORT
DB_NAME
```sh
USE student_db;
```

```sh
CREATE TABLE `students` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `email` varchar(255) DEFAULT NULL,
  `course` varchar(255) DEFAULT NULL,
  `student_class` varchar(255) DEFAULT NULL,
  `percentage` double DEFAULT NULL,
  `branch` varchar(255) DEFAULT NULL,
  `mobile_number` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=80 DEFAULT CHARSET=latin1 COLLATE=latin1_swedish_ci;
```

EXIT FROM DATABASE
```sh
EXIT;
```


For cloning the repo
```sh
git clone https://github.com/Manasipatil4/EASY_CRUD_DOCKER_COMPOSE.git
```

For Frontend
Copy paste the rds endpoint in backend/src/main/resources/application properties in Git Repo

```sh
server.port=8080

spring.datasource.url=jdbc:mariadb://database-1.cv8e4sqis5mc.eu-north-1.rds.amazonaws.com:3306/student_db?sslMode=trust
spring.datasource.username=admin
spring.datasource.password=redhat123

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```


Now for frontend 
```sh
cd frontend
```

```sh
nano .env
```
paste your EC2 public ip its hould look like this 
VITE_API_URL=http://13.61.5.219:8080/api


Now cd..

Go to EasyCRUD-Updated 

Install Docker Engine using below link 
```sh
https://docs.docker.com/engine/install/ubuntu/
```
```sh
docker compose build 
docker images
docker compose up -d
docker ps
```
Now using publicip check on browser


