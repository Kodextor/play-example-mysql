Summary
=======

This project shows how to set up your Play Framework application to:

  * use MySQL locally.
  * deploy to CloudBees and configure to use their MySQL database.
  

Local use of MySQL with Play
============================

To use MySQL locally, you must: (a) install the MySQL database, (b) set the root password, (c) create the database you want to use with your Play application, and (d) configure the Play application.  Let's look at each of these in turn.

Download and install MySQL
--------------------------

Install MySQL by downloading the [MySQL Community Server](http://dev.mysql.com/downloads/mysql/) following the [instructions](http://dev.mysql.com/doc/refman/5.6/en/installing.html).
You will need to create a free account. This project was tested using MySQL
Community Server 5.6.12 for Mac OS X version 10.7 (x86, 64 bit). 

Post-installation: set root password
------------------------------------

The most important thing to do following your local installation is to create a 
password for the root accounts.  The following commands show one way to do it:

    $ mysql -u root
    mysql> select User, Host, Password from mysql.user; 
    mysql> update mysql.user SET Password = PASSWORD('ReplaceWithGoodPassword') WHERE User = 'root';
    mysql> flush privileges;
    
See the [post-installation instructions](http://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)
for more details. For example, you might want to drop the "test" database, or restrict
anonymous use. 

Create user and password environment variables
----------------------------------------------

It is good to not put your MySQL username and password directly in your Play application files, as
that requires all developers to use the same username and password. A better way is to create 
standard environment variables that all developers must set locally with a user and password of their
own choosing. So, the next step is to define two environment variables with your 
username and password.  On Unix, you might edit ~/.profile to include:

    export PLAY_MYSQL_USER=root
    export PLAY_MYSQL_PASSWORD=ReplaceWithGoodPassword
    
If you choose to create a new MySQL user rather than using the root user, then 
you will need to be sure to grant that user privileges for the database
manipulated by the application. 

Create the database to be used with your Play application
---------------------------------------------------------

A significant difference between the default "H2" database application and MySQL
is that H2 will automatically create the database to be used with your Play
application, but you must manually create the MySQL database. 

For this application, we will call our database "playexamplemysql". Assuming we 
are using the root user, you can create it in MySQL with the following

    $ mysql -u root -p
    Enter password: <enter password here>
    mysql> create database playexamplemysql;
    Query OK, 1 row affected (0.00 sec)
    mysql> exit
    $
 



        

 


Screenshot
==========

![screenshot](https://raw.github.com/ics-software-engineering/play-example-mysql/master/doc/play-example-mysql-home.png)

  
   
  
 