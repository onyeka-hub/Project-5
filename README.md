# CLIENT-SERVER ARCHITECTURE WITH MYSQL

Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server".

A machine that is trying to access a Web site using Web browser or simply ‘curl’ command is a client and it sends HTTP requests to a Web server (Apache, Nginx, IIS or any other) over the Internet.

If we extend this concept further and add a Database Server to our architecture, we can get this scenario:

Our Web Server has a role of a "Client" that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network).

## IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).

### TASK – Implement a Client Server Architecture using MySQL Database Management System (DBMS).

To demonstrate a basic client-server using MySQL Relational Database Management System (RDBMS), follow the below instructions

Create and configure two Linux-based virtual servers (EC2 instances in AWS).

> Server A name - `mysql server`

> Server B name - `mysql client`

On mysql server Linux Server install mysql Server software with the following command:

```
sudo apt update

sudo apt install mysql-server

sudo status mysql
```

![MySQL server active](https://github.com/onyeka-hub/Project-5/blob/main/images/mysql-server-active.JPG)

On the mysql client redhat server install mysql client software with the following commands:

```
sudo yum update

sudo yum install mysql
```

By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses.

Use mysql server's local IP address to connect from mysql client.

MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups.

For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

Get the private ip address of the mysql client from the command line by running this command:

```
hostname -i
```

Go to the security groug of mysql server and open port 3306 to the private ip address of the mysql client

You might need to configure mysql server to allow connections from remote hosts.

Change the Bind address from 127.0.0.1 to 0.0.0.0 so that it can connect from anywhere

```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

We need to create a new user in the mysql server which will be used to connect to this server from mysql client
 
Check the list of the users currently in the mysql server database with the command below

```
sudo mysql

select user,host from mysql.user;
```


![list of users in mysql server](https://github.com/onyeka-hub/Project-5/blob/main/images/list-user-mysql-server.JPG)

I am connected as a root user because of the sudo privileges

Create the new user and grant him privileges with the commands below :

```
CREATE USER 'onyeka'@'%' IDENTIFIED BY 'onyeka12345';

GRANT ALL PRIVILEGES ON *.* TO 'onyeka'@'% WITH GRANT OPTION;

FLUSH PRIVILEGES;

select user,host from mysql.user;
```

![list of users in mysql server](https://github.com/onyeka-hub/Project-5/blob/main/images/new-user.JPG)

From mysql client connect remotely to mysql server Database Engine without using SSH. You must use the mysql utility to perform this action.

Copy the private ip address of the mysql server and log into the redhat mysql client terminal

Do the following command to connect to the mysql server through mysql client:

```
mysql -h <private-ip-address-of-the-mysql-server> -u onyeka -p
```

> where -h is for the host

	> -u is for the user 

	> -p is to ask you for the password

To confirm , run the command below

```
select user,host from mysql.user;
```

![list of users in mysql server](https://github.com/onyeka-hub/Project-5/blob/main/images/users-from-client.JPG)

```
SHOW DATABASES;
```

![database](https://github.com/onyeka-hub/Project-5/blob/main/images/show-database.JPG)

## End of project 5
