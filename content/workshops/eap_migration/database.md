---
title: Connecting to a Database
workshops: eap_migration
workshop_weight: 50
layout: lab
---

## Connecting to a Database

The purpose of this lab is to learn about JBoss EAP's database subsystem and create a sample connection to a database.

### Data Sources in JBoss EAP

Most Java EE applications involve a database that contains the information users need to access. A data source is a facility provided by an application server that is responsible for accessing databases without providing sensitive information, such as credentials and the database location, to an application. To connect to a database, the application uses a name bound to the data source via the application server. For a Java EE application server, the name is defined by the Java Naming and Directory Interface (JNDI) specification.

Data sources are configured through the Data Source Subsystem. Declaring a new data source consists of two separate steps:
1. Installing the JDBC driver for a particular database server.
2. Define a data source within the datasource subsystem of the configuration file.

### Configuring a JDBC Driver

There are two steps to installing a JDBC driver:

1. Adding the module
2. Adding the driver definition

#### Adding the Module

A JDBC driver is a component that Java applications use to communicate with a database. A JDBC driver is packaged in a JAR (Java Archive) file, and contains a class file that contains the driver definition. JDBC drivers are available from database vendors, such as from MySQL or PostgreSQL. In order to use a JDBC driver in JBoss EAP 7, it first needs to be installed as a module on
the server.

Adding the JDBC driver module can be done either manually or much more simply with the JBoss EAP CLI. The module add command from CLI requires the user to provide:
- Name: A name based on a Java package name that will be used by EAP to store the JAR file and a configuration file called module. It should be unique and cannot conflict with existing libraries available at `$JBOSS_HOME/modules` directory.
- Resources: Refers to the location that stores the JAR file.
- Dependencies: Identify which Java libraries are used by the JDBC driver and where they are located in JBoss EAP.

The syntax for the module add command is:

```
module add --name=<module_name> --resources=<JDBC_Driver> --dependencies=<library1>,< library2>,...
```

For example, to add a JDBC MySQL 5.5 module by using the file `mysql-connector-java.jar`, the command would be:

```
module add --name=com.mysql \
--resources=/opt/jboss-eap-7.0/bin/mysql-connector-java.jar \
--dependencies=javax.api,javax.transaction.api
```
After executing this command, a new directory is created at `$JBOSS_HOME/modules/com/mysql/main`. The new directory contains the provided JAR file as well as a `module.xml` that is generated based on the driver's given dependencies.

The following `module.xml` file defines a module for the MySQL JDBC driver:

```
<?xml version="1.0" ?>
    <module xmlns="urn:jboss:module:1.1" name="com.mysql">
    <resources>
        <resource-root path="mysql-connector-java.jar"/>
    </resources>
    <dependencies>
        <module name="javax.api"/>
        <module name="javax.transaction.api"/>
    </dependencies>
</module>
```
