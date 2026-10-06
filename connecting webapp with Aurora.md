<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a Web App with Aurora

**Project Link:** [View Project](https://nextwork.ai/projects/921d7b78-ffa4-5e41-a5b5-aed76c78efad)

**Author:** Ahmed Adel Fahmy  
**Email:** ahmed.hedia@outlook.com

---

![Image](https://nextwork.ai/amused_beige_adorable_sphinx/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_1709b26b)

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a relational database and it is useful because it's considered one of the most efficient databases when it comes it heavy workloads and traffic

### How I used Amazon Aurora in this project

In today's project, I used Amazon Aurora to connect with a EC2 that hosts a web application that takes info from the user and stores it in the database

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was being able to connect to database from the EC2 instance.

### This project took me...

this project took around 1 hour 

## Creating a Web App

![Image](https://nextwork.ai/amused_beige_adorable_sphinx/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_b7999168)

To connect to my EC2 instance, I used the key that that was created from the keypair genertor and used the following command:

$ ssh -i <keypair key> ec2-user@<public IP> 


To help me create my web app, I first installed the Apache web server: the most widely used web server in the world. A web server is a software that gets your content (e.g. web pages) to users via the internet.

PHP - a programming language used for writing beautiful app pages.

php-mysqli - a PHP library (i.e. a collection of pre-written code to help you save time) for establishing a MySQL connection to your database.

php-mysqli - a PHP library (i.e. a collection of pre-written code to help you save time) for establishing a MySQL connection to your database.

MariaDB - a relational database management system. Your Aurora database knows how to manage its data (e.g. how to add a new row or retrieve data), but your web server doesn't know how to send instructions to and understand the responses from your Aurora database. Your web server would need MySQL-compatible client libraries i.e. software designed for servers to communicate with a MySQL database. Installing MariaDB in your EC




## Connecting my Web App to Aurora

I set up my EC2 instance's connection details to my database by opening a file dbinc.info file using nano edited and gave it the following info about the database: 

<?php

define('DB_SERVER', 'nextwork-db-cluster.cluster-c3mmkk2wohtg.us-east-1.rds.amazonaws.com');
define('DB_USERNAME', 'admin');
define('DB_PASSWORD', 'n3xtw0rk');
define('DB_DATABASE', 'sample');
?>


![Image](https://nextwork.ai/amused_beige_adorable_sphinx/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_1709b25b)

## My Web App Upgrade

Next, I upgraded my web app by creating the following script that changes the look of the webapp and also gives us the ability to the update, delete info from the database.

<?php include "../inc/dbinfo.inc"; ?>
<html>
<body>
<h1>Sample page</h1>
<?php

  /* Connect to MySQL and select the database. */
  $connection = mysqli_connect(DB_SERVER, DB_USERNAME, DB_PASSWORD);

  if (mysqli_connect_errno()) echo "Failed to connect to MySQL: " . mysqli_connect_error();

  $database = mysqli_select_db($connection, DB_DATABASE);

  /* Ensure that the EMPLOYEES table exists. */
  VerifyEmployeesTable($connection, DB_DATABASE);

  /* If input fields are populated, add a row to the EMPLOYEES table. */
  $employee_name = htmlentities($_POST['NAME']);
  $employee_address = htmlentities($_POST['ADDRESS']);

  if (strlen($employee_name) || strlen($employee_address)) {
    AddEmployee($connection, $employee_name, $employee_address);
  }
?>

<!-- Input form -->
<form action="<?PHP echo $_SERVER['SCRIPT_N

![Image](https://nextwork.ai/amused_beige_adorable_sphinx/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_2709b25b)

## Testing my Web App

To make sure my web app was working correctly, I installed mysql engine from their repo using the following command: 

$ sudo yum install https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm -y

and installed the client using the following command: 

$ sudo yum install mysql-community-client -y

Then I accessed the database using the following command: 

$ mysql -h nextwork-db-cluster.cluster-c3mmkk2wohtg.us-east-1.rds.amazonaws.com -P 3306 -u admin -p

then started to navigate through the database until I was able to check the sample database following the below steps:

$ SHOW DATABASES;
$ USE sample;
$ SHOW TABLES;
$ DESCRIBE EMPLOYEES;
$ SELECT * FROM EMPLOYEES;

![Image](https://nextwork.ai/amused_beige_adorable_sphinx/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_1409z22b)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/921d7b78-ffa4-5e41-a5b5-aed76c78efad)*
