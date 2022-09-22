<<<<<<< HEAD

# CLIENT-SERVER ARCHITECTURE WITH MYSQL


Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server".

A machine that is trying to access a Web site using Web browser or simply ‘curl’ command is a client and it sends HTTP requests to a Web server (Apache, Nginx, IIS or any other) over the Internet.

If we extend this concept further and add a Database Server to our architecture, we can get this scenario:

Our Web Server has a role of a "Client" that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), 

and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network).

## IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

### TASK – Implement a Client Server Architecture using MySQL Database Management System (DBMS).

To demonstrate a basic client-server using MySQL Relational Database Management System (RDBMS), follow the below instructions

Create and configure two Linux-based virtual servers (EC2 instances in AWS).

> Server A name - `mysql server`

> Server B name - `mysql client`

On mysql server Linux Server install mysql Server software with the following command:

	`sudo apt update`

	` sudo apt install mysql-server`

	`sudo status mysql`

![MySQL server active](./Project-5/images/mysql-server-active.jpg)

## On the mysql client redhat server install mysql client software with the following commands:

	`sudo yum update`

	`sudo yum install mysql`

#### By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses.

#### Use mysql server's local IP address to connect from mysql client.

#### MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups.

#### For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

#### Get the private ip address of the mysql client from the command line by running this command:

	`hostname -i`

#### Go to the security groug of mysql server and open port 3306 to the private ip address of the mysql client

#### You might need to configure mysql server to allow connections from remote hosts.

#### Change the Bind address from 127.0.0.1 to 0.0.0.0 so that it can connect from anywhere

	`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

#### We need to create a new user in the mysql server which will be used to connect to this server from mysql client
 
#### Check the list of the users currently in the mysql server database with the command below

	`sudo mysql`

	`select user,host from mysql.user;`


![list of users in mysql server](./Project-5/images/list-user-mysql-server.jpg)

#### I am connected as a root user because of the sudo privileges

### Create the new user and grant him privileges with the commands below :

	`CREATE USER 'onyeka'@'%' IDENTIFIED BY 'onyeka12345';

	`GRANT ALL PRIVILEGES ON *.* TO 'onyeka'@'% WITH GRANT OPTION;

	`FLUSH PRIVILEGES;`

	`select user,host from mysql.user;`


![list of users in mysql server2](./Project-5/images/new-user.jpg)



### From mysql client connect remotely to mysql server Database Engine without using SSH. You must use the mysql utility to perform this action.

#### Copy the private ip address of the mysql server and log into the redhat mysql client terminal

#### Do the following command to connect to the mysql server through mysql client:

	`mysql -h <private-ip-address-of-the-server> -u onyeka -p`

> where -h is for the host

	> -u is for the user 

	> -p is to ask you for the password

#### To confirm , run the command below

	`select user,host from mysql.user;`

![list of users in mysql server3](./Project-5/images/users-from-client.jpg)

	`SHOW DATABASES;

![database](./Project-5/images/show-database.jpg)

## End of project 5

=======
# CLIENT-SERVER ARCHITECTURE WITH MYSQL


### Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

### In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server".

###   A machine that is trying to access a Web site using Web browser or simply ‘curl’ command is a client and it sends HTTP requests to a Web server (Apache, Nginx, IIS or any other) over the Internet.

### If we extend this concept further and add a Database Server to our architecture, we can get this scenario:

### Our Web Server has a role of a "Client" that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network).

## IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

### TASK – Implement a Client Server Architecture using MySQL Database Management System (DBMS).

### To demonstrate a basic client-server using MySQL Relational Database Management System (RDBMS), follow the below instructions

## Create and configure two Linux-based virtual servers (EC2 instances in AWS).

> Server A name - `mysql server`
> Server B name - `mysql client`

## On mysql server Linux Server install mysql Server software with the following command:

	`sudo apt update`
	` sudo apt install mysql-server`
	`sudo status mysql`

![mysql-server-active](https://user-images.githubusercontent.com/83009045/160478610-16effbd8-a067-4b37-8b0d-4a8ff705992e.JPG)


## On the mysql client redhat server install mysql client software with the following commands:

	`sudo yum update`
	`sudo yum install mysql`

#### By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses.
#### Use mysql server's local IP address to connect from mysql client.
#### MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups.
#### For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

#### Get the private ip address of the mysql client from the command line by running this command:

	`hostname -i`

#### Go to the security groug of mysql server and open port 3306 to the private ip address of the mysql client

#### You might need to configure mysql server to allow connections from remote hosts.
#### Change the Bind address from 127.0.0.1 to 0.0.0.0 so that it can connect from anywhere

	`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

#### We need to create a new user in the mysql server which will be used to connect to this server from mysql client
 
#### Check the list of the users currently in the mysql server database with the command below

	`sudo mysql`

	`select user,host from mysql.user;`

![list-user-mysql-server](https://user-images.githubusercontent.com/83009045/160478961-3ec91b73-5373-4264-8c16-d6449e379264.JPG)

#### I am connected as a root user because of the sudo privileges

### Create the new user and grant him privileges with the commands below :

	`CREATE USER 'onyeka'@'%' IDENTIFIED BY 'onyeka12345';

	`GRANT ALL PRIVILEGES ON *.* TO 'onyeka'@'% WITH GRANT OPTION;

	`FLUSH PRIVILEGES;`

	`select user,host from mysql.user;`

![new-user](https://user-images.githubusercontent.com/83009045/160479144-22bb03f3-2228-456e-b333-1b81b97ad6b9.JPG)


### From mysql client connect remotely to mysql server Database Engine without using SSH. You must use the mysql utility to perform this action.

#### Copy the private ip address of the mysql server and log into the redhat mysql client terminal
#### Do the following command to connect to the mysql server through mysql client:

	`mysql -h <private-ip-address-of-the-server> -u onyeka -p`

> where -h is for the host
	> -u is for the user 
	> -p is to ask you for the password

#### To confirm , run the command below

	`select user,host from mysql.user;`

![users-from-client](https://user-images.githubusercontent.com/83009045/160479248-ca117bce-b382-4448-8fe6-3ea2c694bd7f.JPG)

	`SHOW DATABASES;

![show-database](https://user-images.githubusercontent.com/83009045/160479666-265cad2d-960e-498a-ac22-88a5ef3864d4.JPG)


## End of project 5
>>>>>>> 7311397119e688a9773bbaa2c314bb0552ab05fe
