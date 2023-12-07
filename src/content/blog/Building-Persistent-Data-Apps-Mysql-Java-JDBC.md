---
title: 'Dynamic Web Development Environment Setup with MySQL, JDBC, and Ubuntu Server'
date: '2023-10-20'
tags: ['java', 'sql', 'fundamentals']
related: [js-closuresimprove-performance]
author: default
draft: false
summary: 'A quick introduction to java database connection (JDBC) and persistent data on web apps'
---

# Dynamic Web Development Environment Setup with MySQL, JDBC, and Ubuntu Server

## Step 1: Setting the Foundation

### A Clean Slate:

Before diving into the installation process, let’s ensure a fresh start. We’ll uninstall any existing database systems like MariaDB, making way for a smooth MySQL setup.

```bash
sudo apt remove --purge mariadb-*
sudo apt autoremove
```

### Bid Farewell to MySQL (if installed):

Clean up MySQL remnants if it’s already installed on your system.

```bash
sudo apt remove --purge mysql-*
sudo apt autoremove
```

### Clear Configurations:

Delete existing configurations to pave the way for a clean MySQL install.

```bash
sudo rm -rf /etc/mysql /var/lib/mysql
sudo apt clean
sudo apt autoclean
```

## Step 2: MySQL Server Installation

### Update and Install:

Ensure your system is up to date, then install MySQL Server.

```bash
sudo apt update
sudo apt install mysql-server
```

### Secure Your Installation:

Run the MySQL Secure Installation command to configure basic security settings.

```bash
sudo mysql_secure_installation
```

## Step 3: Allow Remote Connections

To connect to MySQL from another machine, tweak the MySQL configuration.

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Make sure the `bind-address` is either commented out or set to `0.0.0.0`. Restart MySQL after making changes.

```bash
sudo service mysql restart
```

## Step 4: Create User and Database

Login to MySQL and execute SQL commands to create a user and a database.

```bash
sudo mysql -u root -p
CREATE USER 'melaku'@'%' IDENTIFIED BY 'pass';
GRANT ALL PRIVILEGES ON *.* TO 'melaku'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

## Step 5: Create a Database and Table

Create a database and a sample table to test the setup. Let's also insert some user records.

```sql
CREATE DATABASE banco;
USE banco;

-- Create a table 'cliente'
CREATE TABLE cliente (
    clienteid INT,
    nombre VARCHAR(255),
    direccion VARCHAR(255),
    telefono VARCHAR(15),
    nacimiento DATE
);

INSERT INTO cliente (clienteid, nombre, direccion, telefono, nacimiento) VALUES
('3534534', 'Cacerolo Tontoñez', 'Almogía', '123456', '1963-04-08'),
('45678', 'Mota', 'Calle Falsa, 123', '555 444333', '1980-06-28'),
('555', 'Luis José', 'Larios, 10', '5555 234233', '2013-02-17'),
('65767', 'Pepito Lupiañez', 'Alhaurín', '867867867', '1992-01-10'),
('76859', 'ignacio', 'Periquito, 333', '555 325476', '1995-08-08'),
('789654', 'Yren', 'Calle Verdadera, 98', '555 98765', '1950-06-06'),
('873475933', 'Maria Sol', 'Calle Flor', '555 123456', '1945-01-01');
```

## Step 6: Test Communication Between Machines

Ensure there’s communication between machines using the ping command.

```bash
ping <remote_machine_ip>
```

## Step 7: Develop a Java Program with JDBC

Once we have the accessible database, the next step is to create a Java program to interact with the database. For this, we need to have a JDBC driver corresponding to the database management system we are using.

```java
Class.forName("com.mysql.cj.jdbc.Driver");
Connection connection = DriverManager.getConnection("jdbc:mysql://<remote_machine_ip>:3306/database_name", "user", "password");
Statement statement = connection.createStatement();
```

You should include this piece of code in your Java class to connect to the database, then go to the official Java API to learn the basics of Java.Sql.

## The Seamless Web Experience: A Deeper Look

### Browser Magic:

As users, we appreciate the simplicity of accessing databases online without worrying about installation hassles. But how does this magic happen?

### Client-Server Choreography:

In the world of client-server architecture, your web browser plays a crucial role as the client, rendering the interface and executing scripts. On the other side, the server manages databases and executes complex tasks.

### Keeping it Server-Side:

Here’s the secret sauce: the Database Management System (DBMS), such as MySQL, is strategically placed on the server such as Apache. This decision isn’t arbitrary — it’s a thoughtful design choice to enhance user experience. Imagine you had to install the DBMS for all sites you access on the internet.

### Beyond User Responsibility:

By keeping the DBMS on the server, developers ensure that end-users like you don’t need to install or maintain complex database systems locally. Your browser communicates with the server, but the intricacies of database management remain in the server’s domain.

### Bridging the Gap:

Behind the scenes, technologies like JDBC and ODBC act as essential bridges, facilitating seamless communication between the client and server. They enable your browser to send queries, and the server, with its DBMS, responds with the requested data.

## Conclusion:

So, the next time you log in on a web page, remember the well-orchestrated dance of client-server architecture. It’s the careful placement of the DBMS on the server that transforms the intricate into the intuitive, providing users with a seamless and enjoyable web experience. Happy browsing!
