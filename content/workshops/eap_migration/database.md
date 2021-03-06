---
title: Connecting to a Database
workshops: eap_migration
workshop_weight: 50
layout: lab
---

## Connecting to a Database

The purpose of this lab is to learn about JBoss EAP's database subsystem and create a sample connection to a database.

### Data Sources in JBoss EAP

Most Java EE applications involve a database that contains the information users need to access. A data source is a facility provided by an application server that is responsible for accessing databases without providing sensitive information, such as credentials and the database location, to an application. There are also additional benefits like the ability to pool connections. To connect to a database, the application uses a name bound to the data source via the application server. For a Java EE application server, the name is defined by the Java Naming and Directory Interface (JNDI) specification.

Data sources are configured through the Data Source Subsystem. Declaring a new data source consists of two separate steps:
1. Installing the JDBC driver for a particular database server.
2. Configure a data source within the data source subsystem of the configuration file.

### Installing a JDBC Driver

There are two steps to installing a JDBC driver:

1. Deploying a JDBC Driver as a module.
2. Adding a driver definition in the data source subsystem.

#### Deploying a JDBC Driver as a Module

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
#### Adding the Driver Definition

After adding the driver as a module, the next step is to create a `<driver>` definition in the `<drivers>` section of the data source subsystem in the EAP configuration file.

A CLI operation can be used to create it easily, without touching the XML file. The following command can be executed on a standalone server:

```
/subsystem=datasources/jdbc-driver=<driver_name>:add\
(driver-module-name=<module_name>,driver-name=<unique_driver_name>)
```

In the driver definition command, the following fields are required:
- driver-name: A unique name for the driver.
- driver-module-name: The unique name from the module installed at `$JBOSS_HOME/modules` directory.

For example, the CLI command to define the MySQL driver looks like the following:

```
/subsystem=datasources/jdbc-driver=mysql:add\
(driver-module-name=com.mysql,driver-name=mysql)
```

#### Verifying the Driver Details

To verify the driver installation, execute the following command:

```
/subsystem=datasources/jdbc-driver=mysql:read-resource
```

The output should be as follows:

```
{
  "outcome" => "success",
  "result" => {
    "deployment-name" => undefined,
    "driver-class-name" => undefined,
    "driver-datasource-class-name" => undefined,
    "driver-major-version" => undefined,
    "driver-minor-version" => undefined,
    "driver-module-name" => "com.mysql",
    "driver-name" => "mysql",
    "driver-xa-datasource-class-name" => undefined,
    "jdbc-compliant" => undefined,
    "module-slot" => undefined,
    "profile" => undefined,
    "xa-datasource-class" => undefined
  
}
```

### Configuring a Data Source

Now that your driver is available in JBoss EAP, you can now configure a data source.

#### Data Source Definition

In JBoss EAP 7, a data source is configured in the server's configuration file (`domain.xml` or `standalone.xml`) within the data source subsystem.

The structure of the data source subsystem is as follows (Note: we will not be editing the XML directly):

```
TODO
```

A quick description of the different elements is below.

#### Creating a Data Source Using the Web Console

The JBoss EAP Management Console provides an easy way to create a data source using templates that are preconfigured for different database vendors. The following steps can be used to create a Non-XA data source with the management console in a standalone server.

1. Select Configuration from the top of the management console and select Subsystems and then Datasources to access the data source subsystem.
2. Click Non-XA and then click Add in order to open the Create Datasource wizard.
3. Select the database that should be used by the Java application and click Next. If none of them are valid, then select the Custom option and look for the JDBC driver documentation to complete the following steps.
4. After entering the Datasource Attributes, click Next to select the driver.
5. Click the Detected Driver option and select the mysql driver that was installed as a module and select Next.
6. On the final step, notice that the connection URL is formatted for the correct MySQL syntax. Click Done to finish creating the data source.

### Testing the Connection

The management console provides a Test Connection button to check that the connections from
a connection pool can access the database. It can be accessed clicking the data source name and
accessing the Test Connection button.

Likewise, the CLI can be used to test if the data source was correctly configured. To check it use
the following command:

```
/subsystem=datasources/data-source=[datasource_name]:test-connection-in-pool
```

